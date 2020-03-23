+++
title = "Fix a Bug in Quickrun, a Vim Plugin"
description = "vim 的 quickrun 插件也可以方便地运行大多数编程语言，但是在运行 R 语言编写的脚步文件时，一直报 ‘file name is missing’ 的错误..."
featured_image = "/img/nvim_custom_config.png"
date = 2020-03-23T22:38:14+08:00
categories = ["coding"]
tags = ["vim", "R", "linux"]
comment = true
+++

Quickrun[^1]是一个整合了常用编程语言运行命令的 Vim Plugin，可以通过 `:Quickrun`
命令，或是自定义的映射，一键运行当前文件。

今天在 Vim 中运行一个 R 文件时，发现结果一直输出“file name is
missing”。查看错误日志，却发现一切正常; 用各种关键词搜索这个输出信息，均未能找到有用的信息;
查看插件的源码，也没看到这个报错的出处。

这时只能从文件入手，把文件（test.R）删到只剩下一句命令：

```r
#!/usr/bin/env Rscript
# -*- coding: utf-8 -*-

print('hello')
```

运行了一下，依然是相同的报错。
再次陷入了 **“越是容易上手的东西，越不容易使用”** 的魔咒。

---

无奈之下只好把文件头的注释也删了。
这时，惊奇地发现居然成功地看到了正常的输出。
也就是说是文件头（shebang）[^2]间接地触发了报错。
但是 Quickrun 是根据根据文件类型来触发运行命令的，理论上不应该受到文件注释的影响。
**唯一的解释是 Quickrun 中加入了对 shebang 的识别机制。**

再次翻看源码和文档，终于发现其中 R 语言的运行命令为：`%c %o --no-save --slave %a < %s`。
默认情况下 `%c` 会被替换为 `comand` 参数中的设定值，即 `R`。
但是在识别到 shebang 的时候，会将 `%c`（小写字母）替换为 `%C`（大些字母），而 `%C` 对应的是 shebang 中设定值，即 `Rscript`。
正常情况下，当前文件 `%s` 会被逐行输出（`<`）为 `R` 命令的标准输入，`R` 命令支持命令行模式。
但是 **`Rscript` 命令只支持文件名作为输入参数，因此触发了报错**。诡异的报错信息就是简单粗暴的 'file name is missing'（_R 相关的设计一直都很随意，大多数的文档和报错信息都云里雾里的。_）。
可以测试这个例子：

```bash
Rscript --no-save --slave < test.R
```

因此有两种修改思路，一是把 Quickrun 中 R 语言的运行命令修改为：`Rscript %s`
这样的形式；二是禁用 Quickrun 对 shebang
文件头的识别。最终采用了第二种方式，在 vim 的配置中加入

```vim
let g:quickrun_config.r = {
    \    'command': 'R',
    \    'exec': '%c %o --no-save --slave %a < %s',
    \    'hook/shebang/enable': 0,
    \}
```

成功解决。

[^1]: https://github.com/thinca/vim-quickrun
[^2]: Linux 下这种首行 #! 开头的注释叫 shebang，目的是让终端能使用正确的解析器来运行文件。
