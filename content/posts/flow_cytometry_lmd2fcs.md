+++
title = "Beckman流式细胞仪数据lmd格式转fcs格式"
date = 2015-12-28T19:26:56+08:00
categories = ["sci"]
tags = ["bio", "cell", "R"]
draft = false
+++

借助 R 语言包`flowcore`，将 Beckman 流式细胞仪数据从 lmd 格式转 fcs 格式，进而能被下游的工具读取。

<!--more-->

单个文件转换

```R
# install
source("http://bioconductor.org/biocLite.R")
biocLite("flowCore")

# convert
library(flowCore)
x <- read.FCS(in.fname) #in.fname=xxx.lmd
write.FCS(x,out.fname) #in.fname=xxx.fcs

```

批量 lmd 转化为 fcs

```R
library(flowCore)
library(tools)

files <- list.files("./")

lmd2fcs <- function(fi){
    x <- read.FCS(fi)
    write.FCS(x,paste0(file_path_sans_ext(fi),".fcs"))
    }

lapply(files, lmd2fcs)

lmd2csv <- function(fi){
    x <- read.FCS(fi)
    write.csv(summary(x),file=paste0(file_path_sans_ext(fi),".summary.csv"))
    }

lapply(files, lmd2csv)
```
