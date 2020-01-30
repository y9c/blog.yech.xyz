+++
title = "Personal Website by Caddy"
description = ""
featured_image = ""
date = 2020-01-30T18:53:20+08:00
categories = ["coding"]
tags = ["website", "server", "blog"]
comment = true
+++

Download hugo:

```bash
mkdir hugo_binary
cd hugo_binary
wget https://github.com/gohugoio/hugo/releases/download/v0.63.2/hugo_extended_0.63.2_Linux-64bit.tar.gz
tar xvf hugo_extended_0.63.2_Linux-64bit.tar.gz
mv hugo /usr/local/bin/
cd ..
rm -r hugo_binary
chmod +x /usr/local/bin/hugo
hugo version
```

Downlaod caddy:

```bash
wget https://github.com/caddyserver/caddy/releases/download/v2.0.0-beta.13/caddy2_beta13_linux_amd64 -O /usr/local/bin/caddy
curl https://getcaddy.com | bash -s personal http.git http.authz http.minify
chmod +x /usr/local/bin/caddy
caddy version
```

Run caddy:

```bash
groupadd --system caddy
useradd --system --gid caddy --create-home --home-dir /var/lib/caddy --shell /usr/sbin/nologin --comment "Caddy web server" caddy

wget https://raw.githubusercontent.com/caddyserver/dist/master/init/caddy.service -O /etc/systemd/system/caddy.service
vim /etc/systemd/system/caddy.service

mkdir -p /etc/caddy
vim /etc/caddy/Caddyfile

# for markdown blog
mkdir -p /var/www/caddy
chown -R caddy:caddy /var/www/caddy
# for caddy log
mkdir -p /var/log/caddy
chown -R caddy:caddy /var/log/caddy

systemctl daemon-reload
systemctl enable caddy.service
systemctl start caddy.service
systemctl status caddy.service
```
