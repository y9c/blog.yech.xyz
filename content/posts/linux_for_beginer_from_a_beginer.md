+++
title = "linux for beginer from a beginer"
date = "2015-12-22T13:47:48+08:00"
tags = ["coidng", "server", "linux"]
categories = ["geek"]
draft = false
+++


> 这不是一份系统的教程, 也不是科学的入门方案, 只是希望能让刚接触linux的人少点困惑.

linux是一个操作系统, 和windows一样. 所以windows下能实现的, linux基本也能实现. 反过来也是一样的.

*不过,别问我linux怎么上QQ, 基本没有很好的方案.*

# 文件操作
windows下做得最多的文件操作无非是"打开","复制","粘贴","重命名".
linux下的对应关系

```
"打开文件夹" == "ls"
```
- 例子一: 打开当前文件夹

![打开](/images/linux_b1.png)

```
"复制+粘贴" == "cp"
```
- 例子二: 复制hehe.txt文件,并粘贴为haha.txt

![复制](/images/linux_b2.png)

```
"重命名/移动" == "mv"
```
- 例子三: 将haha.txt重命名为hello.txt

![重命名](/images/linux_b3.png)

虽然这些命令都是两个字符能搞定的, 但是后面得输入很长的一串文件名, 熟练使用windows的人一定会觉得效率太低.
不过这里面涉及到linux的哲学: **"一切都是对象"**, 可以勉强的理解为所有的东西都是可以操作的, 这是linux和windows比较大的区别. 因为这里说的 **"一切"** 包括了复制粘贴命名本身. 看下面这里例子基本可以说明问题.

- 例子四: 批量添加前缀
```bash
#很多人在windows下有过这样的体验, 给一个文件夹中几十个文件一个个手动添加前缀或者是后缀, 十几分钟一直在重复右键,重命名,修改,确定...
#在linux系统, 因为重命名本身是可以被操作的, 所以你就可以用一个循环来实现重命名, 甚至对重命名命令本身进行修改
#为了方便理解可以用如下命令, *事实上linux有更方便的命令来实现这个事情*, 十几分钟的事情可以在十几秒内完成.
for i in *.txt; do mv $i "beginer-"$i;done
```
![批量操作](/images/linux_b4.png)
