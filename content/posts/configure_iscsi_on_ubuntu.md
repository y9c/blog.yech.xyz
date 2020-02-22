+++
title = "Configure iSCSI on Ubuntu"
description = ""
featured_image = ""
date = 2019-02-26T19:05:50+08:00
categories = ["geek"]
tags = ["net", "linux"]
comment
+++

iSCSI (Internet Small Computer System Interface) is a protocol that allows SCSI commands to be transmitted over a network.

The SCSI communicates with devices such as hard disks through the SCSI controller, and the SCSI controller is called the **Target**.
While the client application that initiates the access is called the **Initiator**.

- Assumed that you already have an iSCSI target on your local network

- Install open-iscsi package in Ubuntu server, and configure it into an iSCSI initiator.

  ```bash
  sudo apt install open-iscsi
  ```

- Check which targets are available through a target IP address on your network.

  Add an eth devicde on your server, and configure the IP address into `192.168.253.199`.

  ```bash
  sudo iscsiadm -m discovery -t st -p 192.168.253.200
  ```

  _change 192.168.253.200 into the target IP address on your network._

- Login and mount the target device

  ```bash
  iscsiadm -m node -T iqn.1997-12.cn.chinaserver:alias.tgt0000.20000001555b42ee -p 192.168.253.200 --login
  sleep 6
  mount -o usrquota,grpquota /dev/sdb1 /storage
  ```
