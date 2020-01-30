---

title: "在R语言中使用并行"
keywords: []
description: ""
author: ""
date: 2018-01-31T00:11:14+08:00
lastmod: 2018-01-31T00:11:14+08:00
draft: false
tags: ["coding", "R"]
categories: ["Coding"]

weight: 0

comment: false
toc: false
autoCollapseToc: false
contentCopyright: false
reward: false
mathjax: false
mathjaxEnableSingleDollar: false
contentCopyright: '<a rel="license noopener" href="https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License" target="_blank">Creative Commons Attribution-ShareAlike License</a>'

---

R语言天生具有数据框处理的优势，这种优势掩盖了R中循环体的劣势，这间接导致了R并行难度大，各种包良莠不齐。

<!--more-->

这个文章整理了目前R语言并行运算常用的包，只讲入门demo和少许原理，不会深入。

