+++
title = "Illumina Sequencing Specification"
date = 2019-02-28T16:36:21+08:00
tags = ["bio", "tech"]
categories = ["sci"]
draft = false
+++

# Specification of illumna platform

| Platform    | Run_Cycle | Base_per_Reads(bp) | Read_per_Lane(M) | Lane_per_Cell | Cell_per_Run | Run_Reagent | Run_Time(h) | Q30(%) |
| ----------- | --------- | ------------------ | ---------------- | ------------- | ------------ | ----------- | ----------- | ------ |
| iSeq100     | SE36      | 36                 | 4                | 1             | 1            | -           | 9           | 85     |
| iSeq100     | SE50      | 50                 | 4                | 1             | 1            | -           | 9           | 85     |
| iSeq100     | SE50      | 75                 | 4                | 1             | 1            | -           | 10          | 80     |
| iSeq100     | PE50      | 150                | 4                | 1             | 1            | -           | 13          | 80     |
| iSeq100     | PE150     | 300                | 4                | 1             | 1            | -           | 17.5        | 80     |
| MiniSeq     | SE75      | 75                 | 22–25            | 1             | 1            | High        | 7           | 85     |
| MiniSeq     | PE75      | 150                | 22–25            | 1             | 1            | High        | 13          | 85     |
| MiniSeq     | PE150     | 600                | 22–25            | 1             | 1            | High        | 24          | 80     |
| MiniSeq     | PE150     | 600                | 7-8              | 1             | 1            | Mid         | 17          | 80     |
| MiSeq       | PE75      | 150                | 22–25            | 1             | 1            | v3          | 21          | 85     |
| MiSeq       | PE300     | 600                | 22–25            | 1             | 1            | v3          | 56          | 70     |
| NextSeq550  | SE75      | 75                 | 400              | 1             | 1            | High        | 11          | 80     |
| NextSeq550  | PE75      | 150                | 400              | 1             | 1            | High        | 18          | 80     |
| NextSeq550  | PE150     | 300                | 400              | 1             | 1            | High        | 29          | 75     |
| NextSeq550  | PE75      | 150                | 130              | 1             | 1            | Mid         | 15          | 80     |
| NextSeq550  | PE150     | 300                | 130              | 1             | 1            | Mid         | 26          | 75     |
| HiSeq2000   | PE150     | 300                |                  |               |              |             |             |        |
| HiSeq2500   | PE150     | 300                |                  |               |              |             |             |        |
| HiSeq3000   | PE150     | 300                |                  |               |              |             |             |        |
| HiSeq4000   | PE150     | 300                |                  |               |              |             |             |        |
| HiSeqX      | PE150     | 300                | 325-375          | 8             | 1/2          | -           | 70          | 75     |
| NovaSeq6000 | PE50      | 100                | 325-400          | 2             | 1/2          | SP          | 13          | 85     |
| NovaSeq6000 | PE150     | 300                | 325-400          | 2             | 1/2          | SP          | 25          | 75     |
| NovaSeq6000 | PE250     | 500                | 325-400          | 2             | 1/2          | SP          | 38          | 75     |
| NovaSeq6000 | PE50      | 100                | 650-800          | 2             | 1/2          | S1          | 13          | 85     |
| NovaSeq6000 | PE100     | 200                | 650-800          | 2             | 1/2          | S1          | 19          | 80     |
| NovaSeq6000 | PE150     | 300                | 650-800          | 2             | 1/2          | S1          | 25          | 75     |
| NovaSeq6000 | PE50      | 100                | 1650-2050        | 2             | 1/2          | S2          | 16          | 85     |
| NovaSeq6000 | PE100     | 200                | 1650-2050        | 2             | 1/2          | S2          | 25          | 80     |
| NovaSeq6000 | PE150     | 300                | 1650-2050        | 2             | 1/2          | S2          | 36          | 75     |
| NovaSeq6000 | PE100     | 200                | 2000-2500        | 4             | 1/2          | S4          | 36          | 80     |
| NovaSeq6000 | PE150     | 300                | 2000-2500        | 4             | 1/2          | S4          | 44          | 75     |

> note:

- paired end reads are regarded as one
- there are unreggle 4 lanes on MiSeq chip, thus treated as one
- 1/2 means single flow cell and dual flow cell are both supported
