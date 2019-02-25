+++
title = "Proxy gitea as caddy subpath"
date = 2019-02-26T03:04:42+08:00
tags = ["coding"]
categories = ["geek"]
draft = false
+++

Using Caddy with a Sub-path as a reverse proxy.
Gitea and Caddy are on different server.

<!--more-->

Caddyfile (on caddy server)

```
example.com {
  proxy /git http://x.x.x.x:3000 {
    without /git
  }
}
```

custom/conf/app.ini (on gitea server)

```
[server]
ROOT_URL = http://example.com/git/
```

## ref

[1] https://docs.gitea.io/en-us/reverse-proxies/
