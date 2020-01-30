+++
title = "Customize Deepin Desktop for Archlinux"
description = ""
featured_image = ""
date = 2019-02-05T18:28:41+08:00
categories = ["coding"]
tags = ["tools", "linux"]
comment = true
+++

> 在英文环境中打开日历的农历显示？<sup>[1]</sup>

- 创建配置文件：`~/.config/deepin/dde-calendar.conf`

- 在其中添加 `EnableLunar=true`

> 修改窗口的标题栏宽度？<sup>[2]</sup>

- 创建配置文件：

  `~/.local/share/deepin/themes/deepin/light/titlebar.ini`(_If you use light theme_)

  或 `~/.local/share/deepin/themes/deepin/dark/titlebar.ini` (_If you use dark theme_)

- 在其中添加

      ```
      [Active]
      height=25

      [Inactive]
      height=25
      ```

注：仅对 deepin-kwin 生效，对 deepin-wm 无效。

> Reference

1. https://bbs.deepin.org/forum.php?mod=viewthread&tid=154593&extra=&page=2
2. https://github.com/linuxdeepin/developer-center/issues/1210
