+++
title = "Fix Chrome Emoji Rendering Issue"
date = 2019-03-07T02:44:14+08:00
tags = ["web", "coding"]
categories = ["geek"]
draft = false
+++

Chrome/Chromium 下部分 emoji 符号显示出来怎么是小方块？而同样的字符在 Firefox 能正常显示。

<!--more-->

原因是系统缺少了 emoji 字体。Chrome 渲染网页的时候，根据 CSS 样式，先查找网页的字体文件，如果找不到再到系统字库里面找。

而 Firefox 本身就打包了 emoji 字符，所以虽然系统没有 emoji 字体，也能正常显示。

- 解决方案：

安装`noto-fonts-emoji`字体

> ArchLinux

```bash
sudo pacman -S noto-fonts-emoji
```

> Ubuntu

```bash
sudo apt install fonts-noto-color-emoji
```

Restart Chrome, or restart PC.
