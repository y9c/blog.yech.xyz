+++
title = "How to use bioawk"
description = ""
featured_image = "/img/bioawk.png"
date = 2018-01-29T10:58:08+08:00
categories = ["coding"]
tags = ["bio","linux"]
comment = true
+++

在 Linux 命令行处理文件过程中,合并文件是一个最基本的操作。

例如有 file1，file2，file3 几个文件，想合并成一个大文件 fileall，这个几乎有个标准答案：

```bash
cat file1 file2 file3 > fileall
```

简单再说两点,

- `cat`是 concatenate 的缩写，本身就是串联的意思。用`cat`来 print out 文件反而不是这个单词本身的含义。

- 如果是 bash 下，且文件名称是连续的，`cat file{1..3} > fileall`应该是逼格更高的写法。

而实际需求很少是上面这么直接，更常见的需求是要文件名也放到最终文件中，以区别不同的样品类型，数据来源之类的。这时候就需要拿出`awk`，代码实现也非常直接：

```bash
# 将文件名作为输出数据的第一列
awk '{FILENAME,$0}' file{1..3} > fileall
```

awk 基本可以实现大部分的文件操作。
网上会把 sed 和 awk 放在一起封神，而 sed 之于 awk，有如 emacs 至于 vim。
一个是神的工具，一个是工具之神。
linux 下有不是这样有趣的组合，前者功能强大，但学习成本略高，后者功能少了一点，但思路清晰，上手快。

在引出文章的主角`bioawk`之前，还要把需求再弄复杂一点。

如果文件是都 gzip 压缩的话，是否也能解决呢？

> 这个其实不少见，比如多个.bed.gz 文件合并，多个.fq.gz 文件合并...

把文件都解压后再操作是一个方法，不过这时候除了浪费空间外，还多了**两次**IO。

linux 下`zcat`命令可以进行 gzip 格式文件的读取，因而有类似的操作：

```bash
zcat file{1..3}.gz > fileall
```

但是`awk`不能读取 gzip 文件。能否用`zcat`加上`awk`来实现带上文件名的合并呢？
先试一下这个：

```bash
# test1
zcat file{1..3}.gz | awk '{FILENAME,$0}' > fileall
```

咦，文件名都去哪了？怎么都是'-'？

原因是 pipe 操作传输的是 stdout 给下一步，而 stdout 就是'-'。如果要把文件名也传过来怎么办呢？直接扔代码:

```bash
# test2
for i in file{1..3}.gz; do awk '{"'"$i"'",$0}' $i> fileall; done
```

两个 defect: 不优雅的 for 循环；4 层嵌套的引号狂魔。

这时候可以召唤主角了，liheng 大神的[bioawk](https://github.com/lh3/bioawk)，基于 C 语言，速度快，功能全，不是那些妖艳的脚本语言实现。

```bash
# test1
bioawk '{FILENAME,$0}' file{1..3}.gz > fileall
```

这不是可以支持 gzip 格式的 awk 么？有什么了不起的？

下面开始讲`bioawk`的了不起之处。

bioawk 是针对生物数据分析开发的软件，除了具有 awk 的功能外，还有针对特定格式的应用。
加`-c`参数加文件类型，可以让 bioawk 针对文件类型进行操作。
支持的文件格式有 bed，sam，vcf，gff，fastx(fastq/fasta)。

```bash
bioawk -c help

---

bed:
	1:chrom 2:start 3:end 4:name 5:score 6:strand 7:thickstart 8:thickend 9:rgb 10:blockcount 11:blocksizes 12:blockstarts
sam:
	1:qname 2:flag 3:rname 4:pos 5:mapq 6:cigar 7:rnext 8:pnext 9:tlen 10:seq 11:qual
vcf:
	1:chrom 2:pos 3:id 4:ref 5:alt 6:qual 7:filter 8:info
gff:
	1:seqname 2:source 3:feature 4:start 5:end 6:score 7:strand 8:frame 9:attribute
fastx:
	1:name 2:seq 3:qual 4:comment

```

如果要统计一个 fastq 文件的长度大于 200bp 的序列条数，用 awk 的实现如下：

```bash
awk 'NR%4==2{if(length($1)>200){a+=1}}END{print a}' file.fq
```

bioawk 实现如下：

```bash
bioawk -c fastx '{if(length($seq)>200){a+=1}}END{print a}' file.fq
```

可以看到，差别在于不用判定行数，bioawk 能自动提取序列。

如果文件是 fasta 格式，这种优势变得更加明显，因为 fasta 文件支持序列跨行，如果同时用 awk 还需要对“>”符号进行判断，合并序列成单行，才能进行后续的统计。
而 bioawk 没有这个问题，liheng 的`kseq.h`自带跨行读取支持。

再举一个例子，awk 可以将 sam 文件转成 fastq 文件，实现如下：

```bash
awk '{print "@"$1"\n"$10"\n+\n"$11}' file.sam > file.fq
```

用 awk 处理过 sam、vcf、gff 文件的，应该都要这样的体验。
每次要把文件头几行打出来，让后用手指着屏幕，一边数数，一边祈祷能一次过。
然而，实际情况都是要数几次才能数对，因为有些列支持置空，这样的空行会导致后面的列数数少了。
更严重的情况是，有些行是没有太大辨识度的数字，这样还不得不打开文档查文件的说明。

而`bioawk`的支持用文件名取列，这样上面的例子可以写成：

```bash
awk '{print "@"$qname"\n"$seq"\n+\n"$qual}' file.sam > file.fq
```

_当然也可以通过`bioawk -c help`查看说明文件，后用数值编号制定输出列。_

还有另一个小技巧，处理文件的时候经常要指定输入文件是 tab 分割，输出文件也用 tab 分割。`awk` 中用 `-F'\t' -v OFS="\t"` 参数来指定，而 bioawk 可以直接有 `-t` 满足一样的需求。

> 你在编程上遇到的问题，99%都已经解决了。剩下 1%中的 99%是你搞错问题了。
