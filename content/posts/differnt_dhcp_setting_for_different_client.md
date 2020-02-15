+++
title = "为不同客户端设置不同 DHCP"
description = "Customize DHCP settings for each client under the lan of OpenWrt router"
featured_image = ""
date = 2020-02-15T16:10:42+08:00
categories = ["coding"]
tags = ["geek", "net", "gfw"]
comment = true
+++

通过在路由器下面挂载树莓派（“旁路由”），并将其他客户端的流量通过树莓派转发出去，可以无缝实现透明代理<sup>[1]</sup>。

将其他客户端的流量转发至“旁路由”有三种方式：

1. 在 OpenWrt 路由器中转发路由器的流量。
2. 在 Lan 口 DHCP 中设置所有客户端获取的 gateway 及 DNS。
3. 为特定客户端指定 gateway 及 DNS。

   _注：2， 3 的配置方式中，客户端有权限自主修改 gateway 及 DNS，自由度更高_

其中第三种方法，即“为特定客户端指定 gateway 及 DNS”的设置方式如下：

在 `/etc/config/dhcp` 文件中添加以下配置文件<sup>2</sup>:

```
config host
    option name 'my-PC'
    option mac 'XX:XX:XX:XX:XX:XX'
    option ip '192.168.1.100'
    option tag 'vpn'

config tag 'vpn'
    list dhcp_option '3,192.168.1.2'
    list dhcp_option '6,192.168.1.2'
    option force '1'
```

其中，`option mac` 为客户端的网卡地址，用于静态地址绑定；`option tag`为配置加上`classifier`标签，用于进一步的配置。
`list dhcp_option '3,192.168.1.2'` 是指定 gateway;
`list dhcp_option '6,192.168.1.2'` 是指定 DNS。

最后重启 dnsmasq 服务：

```bash
/etc/init.d/dnsmasq restart
```

> Reference

1. https://toutyrater.github.io/app/tproxy.html
2. https://openwrt.org/start?id=docs/guide-user/base-system/dhcp
3. https://sites.google.com/site/virtualdesktoplinkboxbox/home/computing/electronics/routers/openwrt?tmpl=%2Fsystem%2Fapp%2Ftemplates%2Fprint%2F&showPrintDialog=1
