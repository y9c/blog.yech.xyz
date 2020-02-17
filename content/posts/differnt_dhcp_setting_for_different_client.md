+++
title = "为不同客户端设置不同 DHCP"
description = "Customize DHCP settings for each client under the lan of OpenWrt router"
featured_image = ""
date = 2020-02-15T16:10:42+08:00
categories = ["coding"]
tags = ["geek", "net", "gfw"]
comment = true
+++

通过在路由器下面挂载树莓派（“旁路由”），并将其他客户端的流量通过树莓派转发出去，可以无缝实现透明代理[^1]，并实现 DNS 服务器的功能。

将其他客户端的流量转发至“旁路由”有三种方式：

1. 在路由器中转发 LAN 口的流量至“旁路由”。
2. 设置 LAN 口客户端以 DHCP 获取的 gateway 及 DNS。

   _注：第 2 种配置方式中，路由器为客户端指定默认的 gateway 及 DNS，而且客户端也有权限自主修改，自由度更高_

OpenWrt 中的 DHCP 可以由 dnsmasq 来实现[^2]，以 OpenWrt 为例，第 2 种方法设置方式如下：

- 在 `/etc/config/dhcp` 文件中添加以下配置文件[^2]:

  _设置所有客户端_

  ```
  config dhcp 'lan'
      option interface 'lan'
      option leasetime '48h'
      option ndp 'relay'
      option ra 'server'
      option dhcpv6 'relay'
      list dhcp_option '3,192.168.2.1'
      list dhcp_option '6,192.168.2.1'
  ```

  _设置某一个客户端_

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

  其中，`option mac` 为客户端的网卡地址，用于静态地址绑定；**`option tag`为配置加上`classifier`标签**[^3]，用于进一步的配置。
  `list dhcp_option '3,192.168.1.2'` 是指定 gateway;
  `list dhcp_option '6,192.168.1.2'` 是指定 DNS。

- 最后重启 dnsmasq 服务：

  ```bash
  /etc/init.d/dnsmasq restart
  ```

> Reference

[^1]: 若采用 V2ray，可参考这个[教程](https://toutyrater.github.io/app/tproxy.html)。
[^2]: 查阅[文档](https://openwrt.org/start?id=docs/guide-user/base-system/dhcp)。
[^3]: 官方文档似乎没有详细描述这个用法，而且中文版的文档还是过时的，最后是通过[这个案例](https://sites.google.com/site/virtualdesktoplinkboxbox/home/computing/electronics/routers/openwrt?tmpl=%2Fsystem%2Fapp%2Ftemplates%2Fprint%2F&showPrintDialog=1)试出来的。
