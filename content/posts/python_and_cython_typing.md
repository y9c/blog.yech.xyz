+++
title = "Python and Cython Typing"
date = 2018-03-05T19:12:53+08:00
tags = ["cython", "python"]
categories = ["coding"]
draft = false
+++

- PEP 526
- Cython 0.27

Python 是一门充满活力的语言，除了相关的包在快速的增加以外，Python 自身的语法特性也在不断推进。
然而这种变化被 Python2 和 Python3 的差异所掩盖，人们往往只关注 Python3 中引入与 Python2 不兼容的部分，而忽视了 Python3 本身也在不断改进。
Python 3.5/3.6 推出不少新的语法特性。虽然都不是强制性的，但如果不主动遵循，几年后别人看你的代码，就好像现在写 Python3 的人看 Pyhton2 代码一般。

## 类型声明

Python 是动态语言，不需要像静态语言（C、java）那样声明变量类型。但这在写较大型的项目的时候反而会成为劣势，所以这几年 Python 试图引入统一的变量声明语法，这种改变好比 JavaScript 到 TypeScript 的变化。
[PEP 484](https://www.python.org/dev/peps/pep-0484/) 在注释中加入了 typing，而 Python 3.6 的 PEP 526 更为彻底，可以在代码中用类似 `var: type` 的格式添加类型注释。

[PEP 526](https://www.python.org/dev/peps/pep-0526/) 用到的注释方式和 Golang 类似，变量名在前，变量类型在后。
_似乎新生的语言 Rust，TypeScript 偏好这种模式，而传统的语言 C，Java 采用相反的模式。_

**之前的写法：**

```python

def fun(n):
    """Print the Fibonacci series up to n."""
    a = 0
    b = 1
    while b < n:
        a, b = b, a + b
    return b

```

**新的写法：**

```python

def fun(n: int) -> int:
    """Print the Fibonacci series up to n."""
    a: int = 0
    b: int = 1
    while b < n:
        a, b = b, a + b
    return b

```

## 静态编译

- Cython 通过静态编译来提升 Python 代码的性能，而加入 C 的类型声明后提升效果更为明显。
  只要稍微修改一些代码，就可以通过 Cython 获得大幅度的性能提升，在很多场景还是值得尝试的。

_Cython 不是唯一的方案, 还有 Swig 之类的，也可实现类似效果。_

- 通过 `pip install -U Cython`，安装最新版本 Cython。

_Cython 相关的知识就不赘述了，下面展示的都是关键函数的代码实现。_

**Cython 传统实现方式：**

```python

cdef int fun(int n):
    """Print the Fibonacci series up to n."""
    cdef int a
    cdef int b
    a = 0
    b = 1
    while b < n:
        a, b = b, a + b
    return b


def run(N: int) -> int:
    return fun(N)

```

## 新的尝试

但是既然 Python 新语法中有了类型声明（typing），那么是否可以就按着 Python 的方式加入 typing，这样代码更加 Pythonic。

Github 上有过这样的[提问](https://github.com/cython/cython/issues/1672)，而最终也在 Cython 0.27 版加入了类似的尝试。

Cython 0.27 Changlog 的第 3 点:

> Variable annotations are now parsed according to PEP 526. Cython types (e.g. `cython.int`) are evaluated as C type declarations and everything else as Python types. This can be disabled with the directive `annotation_typing=False`.

```python
import cython


@cython.cfunc  # cdef functions are faster but not callable from python
def fun(n: cython.int) -> cython.int:
    """Print the Fibonacci series up to n."""
    a: cython.int = 0
    b: cython.int = 1
    while b < n:
        a, b = b, a + b
    return b


def run(N: cython.int) -> cython.int:
    return fun(N)

```

## 性能比较

- 1 raw python
- 2 raw python with typing
- 3 build cythonize python
- 4 build cythonize python with typing
- 5 build cythonize python with cdef
- 6 build cythonize python with cython typing
