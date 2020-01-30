+++
title = "随手记录点vim技巧(五)"
description = ""
featured_image = "/img/nvim_custom_config.png"
date = 2020-01-30T14:50:30+08:00
categories = ["coding"]
tags = ["vim", "editor"]
comment = true
+++

> Q: 怎么查看 vim 启动时加载的脚本？
> (启动 vim 时怎么 debug？)

查看 vim 加载时执行了哪些脚本（加载了那些插件）:

```vim
:scriptnames
' or `:scr` for short
```

查看每一个脚本/插件的耗时：

```bash
vim --startuptime start_time.log filename
```

不加载插件启动：

```bash
# vim
vim --clean
# neovim
nvim --noplugin
```

指定从另外的配置文件启动：

```bash
vim -u min.vim filename
```

> Reference

- http://www.wepeng.net/article/detail/100518128.html
