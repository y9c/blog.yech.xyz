+++
title = "随手记录点vim技巧(六)"
description = "怎么查看 vim 中某个单词/高亮的 syntax 的类型？"
featured_image = "/img/nvim_custom_config.png"
date = 2020-02-22T01:16:22+08:00
categories = ["coding"]
tags = ["vim", "editor"]
comment = true
+++

> Q: 怎么查看 vim 中某个单词/高亮的 syntax 的类型？
> (想修改某一单词的高亮颜色（highlight）或是语法类型（syntax），但如何快速地判断当前被匹配上的类型？)

- 设置快捷键：

  其中，
  `synID` 获取 syntax 的 ID，参数分别为（行号，列号，TRUE/FALSE[^1]）;
  `synIDtrans` 获取 highlight 的 ID，参数分别为（行号，列号，TRUE/FALSE[^1]）;
  `synIDattr` 获取 ID 对应的 syntax 名称（"name"）。

  ```vim
  map <F10> :echo
              \ "hi<" . synIDattr(synID(line("."),col("."),1),"name") . ">
              \ trans<" . synIDattr(synID(line("."),col("."),0),"name") . ">
              \ lo<" . synIDattr(synIDtrans(synID(line("."),col("."),1)),"name") . ">"
              \ <CR>
  ```

- 光标定位至感兴趣的单词，按 F10 相似 syntax 和 highlight 的名称，例如：

  `hi<vimMap> trans<vimMap> lo<vimCommand>`

- 查看 syntax 的正则表达式：

  ```vim
  :syntax list
  ```

  在结果定位 syntax 名称的关键词。

- 查看文件并进行修改：

  ```vim
  :scriptnames
  ```

  查看加载的配置文件，并在这些文件中定位目标正则表达式，进行修改。

> Reference

- https://vim.fandom.com/wiki/Identify_the_syntax_highlighting_group_used_at_the_cursor
- https://superuser.com/questions/686241/how-do-i-tell-what-syntax-file-is-being-used

[^1]: When {trans} is |TRUE|, transparent items are reduced to the item that they reveal. When {trans} is |FALSE|, the transparent item is returned.
