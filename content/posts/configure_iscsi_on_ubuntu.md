+++
title = "Configure iscsi on ubuntu"
date = 2019-02-26T19:05:50+08:00
tags = ["net"]
categories = ["geek"]
draft = false
+++

local eth address `192.168.253.199`

```bash
iscsiadm -m node -T iqn.1997-12.cn.chinaserver:alias.tgt0000.20000001555b42ee -p 192.168.253.200 --login
sleep 6
mount -o usrquota,grpquota /dev/sdb1 /storage
```
