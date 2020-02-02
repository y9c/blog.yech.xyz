+++
title = "Open Resource for 2019-NCoV"
description = "collections of open access data and open source code for 2019-NCoV"
featured_image = "/img/Wuhan_seafood_market_pneumonia_virus_map.svg"
date = 2020-01-30T19:07:54+08:00
tags = ["biology", "virus"]
categories = ["sci"]
comment = true
+++

## 🧬 Genomic sequence

### Reference genome

**Genebank ID** (NCBI):

[MN908947](https://www.ncbi.nlm.nih.gov/nuccore/MN908947)

![Genome map](/img/Wuhan_seafood_market_pneumonia_virus_map.svg)

### Genome resource

**NCBI 官方整理数据**：

[GeneBank](https://www.ncbi.nlm.nih.gov/genbank/2019-ncov-seqs/)

**中科院 2019 新型冠状病毒资源库**（[NGDC](https://bigd.big.ac.cn/ncov#progress)）:

example

| 病毒株名                    | 序列号         | 数据来源 | 相关 ID        | 序列完整度         |
| --------------------------- | -------------- | -------- | -------------- | ------------------ |
| 2019-nCoV WHU01             | MN988668       | GenBank  | EPI_ISL_406716 | Complete           |
| 2019-nCoV/USA-CA1/2020      | MN994467       | GenBank  | EPI_ISL_406034 | Complete           |
| 2019-nCoV/USA-CA2/2020      | MN994468       | GenBank  | EPI_ISL_406036 | Complete           |
| BetaCoV/Foshan/20SF207/2020 | EPI_ISL_406534 | GISAID   |                | Complete           |
| BetaCoV/Foshan/20SF210/2020 | EPI_ISL_406535 | GISAID   |                | Complete           |
| ...                         |                |          |                |                    |
| 2019-nCoV_HKU-SZ-007c_2020  | MN975268       | GenBank  |                | Partial/gene level |
| 2019-nCoV_HKU-SZ-007c_2020  | MN975265       | GenBank  |                | Partial/gene level |

[more info](/dat/Released_2019-nCoV_Genome_Sequences.csv) (update in 2020-02-02 03:14)

### DNA sequence donwload

Collected by YC, [read more](/posts/phylogenetic_analysis_for_2019-ncov/)

## 🦠 Epide genome

### Data source

- https://3g.dxy.cn/newh5/view/pneumonia

  来自“丁香园”的实时数据。

- https://news.qq.com/zt2020/page/feiyan.htm

  来自“腾讯新闻”的实时数据。

- https://activity.peopleapp.com/broadcast/

  来自“人民日报”的实时数据。

- https://sa.sogou.com/new-weball/page/sgs/epidemic

  来自“搜狗搜索”的实时数据。

- https://bnonews.com/index.php/2020/01/the-latest-coronavirus-cases/

  来自 BNO 的数据整理。**和国内一系列网站相比，每条数据均提供了数据来源的链接，看起来最为严谨。**

### Achieved data

- https://raw.githubusercontent.com/BlankerL/DXY-2019-nCoV-Data/master/DXYArea.csv

  Time series date by area.
  同时，开放了实时获取的 API：[![API Status](https://img.shields.io/website?url=https%3A%2F%2Flab.isaaclin.cn)](https://lab.isaaclin.cn/nCoV/)

- https://github.com/globalcitizen/2019-wuhan-coronavirus-data

  分时段保存了 DXY 和 BNO 的数据。

**二次接口**:

- https://service-f9fjwngp-1252021671.bj.apigw.tencentcs.com/release/pneumonia

  实时获取“丁香园”的数据接口

**Map**:
![Geo map](/img/2019-NCoV-animation.gif)
