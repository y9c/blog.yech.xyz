+++
title = "Beckman流式细胞仪数据lmd格式转fcs格式"
date = "2015-12-28T19:26:56+08:00"
tags = []

+++


# 方法一: R语言包flowcore

```R
# install
source("http://bioconductor.org/biocLite.R")
biocLite("flowCore")

# convert
library(flowCore)
x <- read.FCS(in.fname) #in.fname=xxx.lmd
write.FCS(x,out.fname) #in.fname=xxx.fcs

```

```R
#批量lmd转化为fcs
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
