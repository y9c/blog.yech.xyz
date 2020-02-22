+++
title = "Proxy Gitea as Caddy Subpath"
description = ""
featured_image = ""
date = 2019-02-26T03:04:42+08:00
categories = ["coding"]
tags = ["web", "git", "caddy"]
comment = true
+++

Using Caddy with a Sub-path as a reverse proxy.

Gitea and Caddy are on different server.

<!--more-->

Caddyfile (on caddy server)

```json
example.com {
  proxy /git http://x.x.x.x:3000 {
    without /git
  }
}
```

custom/conf/app.ini (on gitea server)

```toml
[server]
ROOT_URL = http://example.com/git/
```

> Reference

1. https://docs.gitea.io/en-us/reverse-proxies/
