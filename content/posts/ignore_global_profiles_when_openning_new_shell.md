+++
title = "Ignore Global Profiles When Openning New Shell"
description = ""
featured_image = ""
date = 2021-02-19T02:49:55+08:00
categories = []
tags = []
comment = true
+++

登陆超算服务器时，由于系统配置了大量的启动脚本，位于 `/etc/profile.d/` 目录中。而普通用户并没有权限修改该目录中的文件，导致每创建一个新的窗口时都会卡顿。

通过设置 tmux 的启动命令，可以跳过全局文件的加载。

对于 zsh shell, 在 `tmux.conf` 中添加：

```bash
set -g default-command 'zsh -d'
```

对于 bash shell, 在 `tmux.conf` 中添加：

```bash
set -g default-command 'bash --noprofile --norc'
```
