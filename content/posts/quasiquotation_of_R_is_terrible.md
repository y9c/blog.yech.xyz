+++
title = "Quasiquotation of R is Terrible"
description = "The lazy evaluation mechanism of R language make metaprogramming work in a different way."
featured_image = ""
date = 2020-04-07T15:06:59+08:00
categories = ["coding"]
tags = ["R", "metaprogramming", "quasiquotations"]
comment = true
+++

Metaprogramming (元编程[^1]) 是指程序在运行前/时， **将代码自身作为数据进行处理**，从而获得了在更高的层面扩展了编程语法的表达力。
实现方式大致有两类（_不是很严格的分法_），一类是<ins>利用模板等在编译时替换代码</ins>（宏，Macro）；另一类是<ins>利用内置的函数在运行时动态转变代码</ins>（如, quasiquotation）。

Quasiquotation 中 `quasi-` 的中文翻译有「半-」、「准-」的含义。quotation 表面上是“添加引号”的意思， 包含了 quote 和 unquote 的两个相反的过程。
本质上是「将可执行的代码转变为 **unevaluated expression**」和「将 **unevaluated expression** 转变为代码来执行」这两个过程。
quasiquotation 在 1970 年中期即被 Lisp 语言所使用 (`` ` `` 符号)， 后来发明的很多语言都“抄”了 Lisp 的这个特性，如 Racket ( `` ` `` / `@`), Clojure (`` ` `` / `~`), and Julia (`:` / `@`) 等[^2]。
这些语言的 quasiquotations 都必须显式地（explicity）使用。

R 语言也是借鉴了 Lisp 的 quasiquotation，然而与大多数语言都不同的是，
如果巧妙利用 R 语言中函数， quasiquotation 在 R 可以通过隐式地（**implicitly**）调用。这也是 R 语言作为统计学工具的强大支持，也是 R 作为一门编程语言最“丑陋”[^3]的一面。

---

和所有的编程语言一样，符号（Symbol）和字符串（String）是不一样的，调用符号输出的是符号背后对应的变量。
例如可以通过以下定义的函数(`f1()`)测试一下：
输入符号 `x`，输出的是 `[1] hello`；
而输入字符串 `"x"`，输出的是 `[1] x`。

```R
f1 <- function(x) {
    print(x)
}

x <- "hello"
f1(x)
f1("x")
```

但是可以通过定义以下的函数（`f2()`），在类似的测试中，却得到了完全相反的输出：
输入符号 `x`，输出的是 `[1] x`；
而输入字符串 `"x"` ，输出的是 `[1] hello`。

```R
f2 <- function(x) {
    if (is.name(substitute(x))) {
        print(as.character(substitute(x)))
    } else {
        print(eval(as.name(x), envir = .GlobalEnv))
    }
}


x <- "hello"
f2(x)
f2("x")
```

R 语言就是个黑箱子，用户不查看源码的话，完全不会知道一个函数到底得输入什么，又会输出什么。
对于开发者来说， R 语言是强大的，一切都是可变的，不变的是一脸懵逼的用户。

[^1]: `Meta-` 这个前缀的含义比较复杂，既有 「**...之后**」、「**高于...**」的意味 (eg. metacarpus 表示腕骨后面的骨，即掌骨，)， 又有「**状态改变**」的含义 (eg. metamorphosis 为变态发育)，同时还有「**关于...自身的...**」(eg. metaphysics, 其中 meta 有 self-referential 的含义，即关于物理学的物理学，国内翻译为“形而上学”)。**Meta-programming** 似乎这三个层面的含义都有涉及。 所以有翻译成後設编程的，也有翻译成譯超編程的，都能大体反映出单词的含义，但却不够全面。然而要把这几层意思都表达出来，估计这名字得有一句话那么长。所以倒是国内翻译成「**元**编程」较为巧妙，毕竟中国汉字这个`「元」`字也有无数层的含义，硬掰的话似乎还能全涵盖英语中`Meta-`所表达出的意思。
[^2]: https://adv-r.hadley.nz/quasiquotation.html
[^3]: R 语言是真的丑，没有加引号的必要。
