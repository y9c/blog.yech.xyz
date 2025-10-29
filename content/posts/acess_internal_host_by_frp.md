+++
title = "打造“可溯源”的ssh转发：解决 frp + Fail2ban 无法获取真实 IP 的问题"
description = ""
featured_image = ""
date = 2025-10-29T06:18:42+08:00
categories = ["coding"]
tags = ["frp", "net", "server", "ssh", "fail2ban"]
comment = true
+++

# 背景

FRP是访问内网服务器的常用手段。 但将内网服务器的 `ssh` 端口转发到公网时，一个严重的安全问题常被忽略：
内网服务器上的 `sshd` 服务（可查看 `/var/log/auth.log`）显示，所有的连接尝试都来自 `127.0.0.1`。这是因为 `frpc` 客户端在本地（`127.0.0.1`）接收了来自 frps 的流量，然后再转发给本地的 `sshd` 22 端口。
这导致安全策略，例如 fail2ban 完全失效。它无法根据源 IP 来封禁恶意的暴力破解者。同时如果 fail2ban 错误地封禁了 127.0.0.1，那么整个 `frp` 转发服务都会中断。
我需要一种方法，让 `sshd` 服务能“看透”FRP，获取到发起 `ssh` 连接的真实客户端 IP，使整个 `ssh` 转发链路变得**“可溯源”**。

# 解决方案

`frp` 的 v2 版本支持在 TCP 转发时发送 PROXY protocol 头部信息，这个头部中包含了原始客户端的真实 IP。
那么解决方案就是在 `frpc` 和 `sshd` 之间插入一个 proxy，用于接收 `frpc` 带有 PROXY 头部的数据包。

**go-mmproxy** 是一个支持 PROXY protocol 的轻量级代理，可以解析出真实客户端 IP (例如 A.B.C.D)，并利用 Linux 的 ip rule 和 ip route 路由表技巧，“伪造”一个源 IP 为 A.B.C.D 的新连接，去访问本地的 `sshd` 服务。
这样，`sshd` 就认为连接是直接来自 A.B.C.D，fail2ban 也就能正常工作了。

`go-mmproxy` 的工作原理是：

```
流量架构[客户端 (A.B.C.D)]
       |
       v
[FRPS (公网服务器)]
       |
       v
[`frpc` (内网服务器)] -> (携带 PROXY v2 头部)
       |
       v
[`go-mmproxy` (监听 127.0.0.1:33322)] -> (解析 IP，伪造源 IP)
       |
       v
[`sshd` (监听 127.0.0.1:22)] -> (日志中记录 A.B.C.D)
       |
       v
[Fail2ban (监控 `sshd` 日志)] -> (封禁 A.B.C.D)
```

# 🛠️ 工具安装 (基于 Ubuntu)

假设你使用的是 Ubuntu 服务器。无需安装 Go 语言环境，我们直接下载预编译好的二进制文件。

1. 安装 `frp` (下载二进制)

   `frp` 下载: https://github.com/fatedier/frp/releases

```bash
# 下载 `frp` (v0.65.0, linux-amd64)
# (如果你的架构不同 e.g., arm64, 请去 GitHub 页面替换链接)
wget https://github.com/fatedier/frp/releases/download/v0.65.0/frp_0.65.0_linux_amd64.tar.gz
tar -zxvf frp_0.65.0_linux_amd64.tar.gz
sudo mv ./frp_0.65.0_linux_amd64/frpc /usr/local/bin/
sudo chmod +x /usr/local/bin/frpc
```

2. 安装 `go-mmproxy` (下载二进制)

   `go-mmproxy` 下载: https://github.com/kzemek/go-mmproxy/releases

(_我们使用 kzemek 维护的 `go-mmproxy` fork，它提供了更新的预编译版本。_)

```bash
# 下载 v2.3.0, linux-amd64
# (同样，请根据你的架构检查 GitHub 页面)
wget https://github.com/kzemek/go-mmproxy/releases/download/v2.3.0/go-mmproxy-v2.3.0-linux-amd64
# 移动并重命名为 go-mmproxy
sudo mv ./go-mmproxy-v2.3.0-linux-amd64 /usr/local/bin/go-mmproxy
sudo chmod +x /usr/local/bin/go-mmproxy
```

3. 安装 fail2ban

   使用 apt 安装 fail2ban：

```bash
sudo apt update
sudo apt install fail2ban
```

# 🔧 具体配置

1. 配置 `go-mmproxy` (systemd)

   `go-mmproxy` 必须在 `frpc` 之前启动，并且需要 ip rule 权限来配置路由表。

   创建 `/etc/systemd/system/go-mmproxy.service`:

```toml
[Unit]
Description=`go-mmproxy` Service for SSH
After=network.target

[Service]
Type=simple
# 监听 33322 端口，转发到 22 端口
ExecStart=/usr/local/bin/go-mmproxy -l 127.0.0.1:33322 -4 127.0.0.1:22 --allowed-subnets /etc/frp/path-prefixes.txt
ExecStop=/usr/bin/pkill go-mmproxy
# --- 关键：配置策略路由 ---
# 允许 mmproxy "伪造" 源 IP
ExecStartPost=/sbin/ip rule add from 127.0.0.1/8 iif lo table 123
ExecStartPost=/sbin/ip route add local 0.0.0.0/0 dev lo table 123
ExecStartPost=/sbin/ip -6 rule add from ::1/128 iif lo table 123
ExecStartPost=/sbin/ip -6 route add local ::/0 dev lo table 123
# 服务停止时清理规则
ExecStopPost=/sbin/ip rule del from 127.0.0.1/8 iif lo table 123
ExecStopPost=/sbin/ip route del local 0.0.0.0/0 dev lo table 123
ExecStopPost=/sbin/ip -6 rule del from ::1/128 iif lo table 123
ExecStopPost=/sbin/ip -6 route del local ::/0 dev lo table 123
Restart=on-failure
RestartSec=10s

[Install]
WantedBy=multi-user.target
```

2. 配置 `frpc` (frpc.toml)

   修改 `frpc` 的配置文件，让 `ssh` 代理不指向 `sshd` (22)，而是指向 `go-mmproxy` (33322)。

   编辑 `/etc/frp/frpc.toml`:

```toml
serverAddr = "frp.your-domain.com" # 你的FRP服务器
serverPort = 7000
auth.method = "token"
auth.token = "your_token" # 你的Token 需要修改

[[proxies]]
name = "ssh-proxy"
type = "tcp"
localIP = "127.0.0.1"
# 关键 (1): 公网访问端口 (需要自行修改)
remotePort = 6001
# 关键 (2): localPort 指向 go-mmproxy
localPort = 33322
# 关键 (3): 启用 PROXY v2 协议
transport.proxyProtocolVersion = "v2"
```

3. 配置 `frpc` (systemd)

   确保 frpc.service 在 go-mmproxy.service 启动之后才启动。

   编辑 `/etc/systemd/system/frpc.service`:

```toml
[Unit]
Description = `frp` Client Service
# 关键：确保 mmproxy 先于 `frpc` 启动
Requires=go-mmproxy.service
After=network.target syslog.target go-mmproxy.service
Wants=network.target

[Service]
Type = simple
User = nobody # 建议使用低权限用户
Restart = on-failure
RestartSec = 5s
ExecStart = /usr/local/bin/`frpc` -c /etc/frp/frpc.toml
LimitNOFILE = 1048576

[Install]
WantedBy = multi-user.target
```

4. 配置 Fail2ban (jail.local)

   fail2ban 不需要任何特殊配置。因为 `sshd` 日志现在记录的是真实 IP，fail2ban 默认的 `sshd` jail 就可以直接工作。

   确保 `/etc/fail2ban/jail.local` 中 `sshd` 是启用的（如果文件不存在，请创建它）：

```toml
[DEFAULT]
# 确保你的常用IP在白名单中
# ignoreip = 127.0.0.1/8 ::1 192.168.1.0/24 YOUR_OFFICE_IP

[sshd]
enabled = true

# 其他配置（maxretry, bantime 等）按需设置
```

# 验证

1. 重载 systemd 并启动服务：

```bash
sudo systemctl daemon-reload
sudo systemctl restart go-mmproxy.service
sudo systemctl restart frpc.service
# fail2ban 已经在安装时启动了，重启一下以加载 jail.local
sudo systemctl restart fail2ban.service
```

2. 检查服务状态：

```bash
sudo systemctl status go-mmproxy frpc fail2ban
```

（确保它们都是 active (running)）

3.  模拟攻击：从一个外部IP（例如手机热点，不要使用白名单IP）尝试连接你的FRP公网端口：

```bash
ssh some_fake_user@frp.your-domain.com -p 6001
```

故意输错几次密码。

4. 检查日志：在内网服务器上查看 `sshd` 日志：

```bash
sudo journalctl -u sshd -n 20
# 或
# sudo tail /var/log/auth.log
```

你应该能看到类似 Failed password for invalid user ... from [你的手机IP] 的记录，而不是 127.0.0.1。

5. 检查 Fail2ban：

```bash
sudo fail2ban-client status sshd
```

你应该能在 Banned IP list 中看到你的手机IP。
