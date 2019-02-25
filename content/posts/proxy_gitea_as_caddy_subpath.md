+++
title = "Proxy_gitea_as_caddy_subpath"
date = 2019-02-26T02:53:35+08:00
tags = ["web"]
categories = ["geek"]
draft = false
+++

Using Caddy with a Sub-path as a reverse proxy.
Gitea and Caddy is not on the same machine.

<!--more-->

## conf

Caddyfile (in website server)

```
example.com {
  proxy /git http://x.x.x.x:3000 {
    without /git
  }
}
```

custom/conf/app.ini (in gitea server)

```
[server]
ROOT_URL = http://git.example.com/git/
```

## ref

[1] https://docs.gitea.io/en-us/reverse-proxies/
