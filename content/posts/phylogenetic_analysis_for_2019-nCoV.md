+++
title = "Phylogenetic Analysis for 2019-NCoV"
description = ""
featured_image = ""
date = 2020-02-02T16:48:18+08:00
categories = ["bio"]
tags = ["evolution", "DNA"]
comment = true
hide = true
+++

Data source:

| Sampele_Name                     | Query_ID<sup>[1]</sup>                                                                                                                                                            | Completeness           |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| BetaCoV/Wuhan/IPBCAMS-WH-01/2019 | [GWHABKF00000000](ftp://download.big.ac.cn/gwh/Viruses/Betacoronavirus_IPBCAMS-WH-01_GWHABKF00000000/GWHABKF00000000.genome.fasta.gz)                                             | Complete               |
| BetaCoV/Wuhan/IPBCAMS-WH-02/2019 | [GWHABKG00000000](ftp://download.big.ac.cn/gwh/Viruses/Betacoronavirus_IPBCAMS-WH-02_GWHABKG00000000/GWHABKG00000000.genome.fasta.gz)                                             | Complete               |
| BetaCoV/Wuhan/IPBCAMS-WH-03/2019 | [GWHABKH00000000](ftp://download.big.ac.cn/gwh/Viruses/Betacoronavirus_IPBCAMS-WH-03_GWHABKH00000000/GWHABKH00000000.genome.fasta.gz)                                             | Complete               |
| BetaCoV/Wuhan/IPBCAMS-WH-04/2019 | [GWHABKI00000000](ftp://download.big.ac.cn/gwh/Viruses/Betacoronavirus_IPBCAMS-WH-04_GWHABKI00000000/GWHABKI00000000.genome.fasta.gz)                                             | Complete               |
| BetaCoV/Wuhan/IPBCAMS-WH-05/2020 | [GWHABKJ00000000](ftp://download.big.ac.cn/gwh/Viruses/Betacoronavirus_IPBCAMS-WH-05_GWHABKJ00000000/GWHABKJ00000000.genome.fasta.gz)                                             | Complete               |
| WIV02                            | [GWHABKK00000000](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN996527&conwithfeat=on&withparts=on&hide-cdd=on) | Complete               |
| WIV04                            | [GWHABKL00000000](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN996528&conwithfeat=on&withparts=on&hide-cdd=on) | Complete               |
| WIV05                            | [GWHABKM00000000](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN996529&conwithfeat=on&withparts=on&hide-cdd=on) | Complete               |
| WIV06                            | [GWHABKN00000000](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN996530&conwithfeat=on&withparts=on&hide-cdd=on) | Complete               |
| WIV07                            | [GWHABKO00000000](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN996531&conwithfeat=on&withparts=on&hide-cdd=on) | Complete               |
| TG13                             | [GWHABKP00000000](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN996532&conwithfeat=on&withparts=on&hide-cdd=on) | Complete               |
| Wuhan-Hu-1                       | [MN908947 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN908947&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| 2019-nCoV_HKU-SZ-002a_2020       | [MN938384 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN938384&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| 2019-nCoV_HKU-SZ-005b_2020       | [MN975262 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN975262&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| 2019-nCoV/USA-WA1/2020           | [MN985325 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN985325&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| 2019-nCoV WHU01                  | [MN988668 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN988668&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| 2019-nCoV WHU02                  | [MN988669 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN988669&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| 2019-nCoV/USA-IL1/2020           | [MN988713 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN988713&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| 2019-nCoV/USA-CA1/2020           | [MN994467 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN994467&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| 2019-nCoV/USA-CA2/2020           | [MN994468 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN994468&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| 2019-nCoV/USA-AZ1/2020           | [MN997409 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN997409&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| BetaCoV/Australia/VIC01/2020     | [MT007544 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MT007544&conwithfeat=on&withparts=on&hide-cdd=on)       | Complete               |
| BetaCoV/Wuhan/WH-01/2019         | [NMDC60013002-01](http://www.nmdc.cn/SProject/virus/NMDC10013002/NMDC60013002-01.fasta)                                                                                           | Complete               |
| BetaCoV/Wuhan/WH-03/2019         | [NMDC60013002-03](http://www.nmdc.cn/SProject/virus/NMDC10013002/NMDC60013002-03.fasta)                                                                                           | Complete               |
| BetaCoV/Wuhan/WH-04/2019         | [NMDC60013002-04](http://www.nmdc.cn/SProject/virus/NMDC10013002/NMDC60013002-04.fasta)                                                                                           | Complete               |
| BetaCoV/Wuhan/WH19002/2019       | [NMDC60013002-05](http://www.nmdc.cn/SProject/virus/NMDC10013002/NMDC60013002-05.fasta)                                                                                           | Complete               |
| BetaCoV/Wuhan/WH19008/2019       | [NMDC60013002-06](http://www.nmdc.cn/SProject/virus/NMDC10013002/NMDC60013002-06.fasta)                                                                                           | Complete               |
| BetaCoV/Wuhan/YS8011/2020        | [NMDC60013002-07](http://www.nmdc.cn/SProject/virus/NMDC10013002/NMDC60013002-07.fasta)                                                                                           | Complete               |
| BetaCoV/Wuhan/WH19001/2019       | [NMDC60013002-08](http://www.nmdc.cn/SProject/virus/NMDC10013002/NMDC60013002-08.fasta)                                                                                           | Complete               |
| BetaCoV/Wuhan/WH19004/2020       | [NMDC60013002-09](http://www.nmdc.cn/SProject/virus/NMDC10013002/NMDC60013002-09.fasta)                                                                                           | Complete               |
| BetaCoV/Wuhan/WH19005/2019       | [NMDC60013002-10](http://www.nmdc.cn/SProject/virus/NMDC10013002/NMDC60013002-10.fasta)                                                                                           | Complete               |
| 2019-nCoV_HKU-SZ-001_2020        | [MN938385 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN938385&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-004_2020        | [MN938386 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN938386&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-001_2020        | [MN938387 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN938387&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-002b_2020       | [MN938388 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN938388&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-004_2020        | [MN938389 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN938389&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-005_2020        | [MN938390 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN938390&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| SI200040-SP                      | [MN970003 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN970003&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| SI200121-SP                      | [MN970004 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN970004&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-007a_2020       | [MN975263 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN975263&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-007b_2020       | [MN975264 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN975264&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-007c_2020       | [MN975265 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN975265&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-007a_2020       | [MN975266 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN975266&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-007b_2020       | [MN975267 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN975267&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019-nCoV_HKU-SZ-007c_2020       | [MN975268 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MN975268&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019 nCoV/Italy-INMI1            | [MT008022 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MT008022&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| 2019 nCoV/Italy-INMI2            | [MT008023 ](https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?tool=portal&save=file&log$=seqview&db=nuccore&report=fasta&id=MT008023&conwithfeat=on&withparts=on&hide-cdd=on)       | Partial/gene level     |
| BetaCoV/Wuhan/WH-02/2019         | [NMDC60013002-02](http://www.nmdc.cn/SProject/virus/NMDC10013002/NMDC60013002-02.fasta)                                                                                           | Partial/scaffold level |

- [1]: _With download link, click for downlaod fasta file._
- [2]: _GISAID data is not public available._
