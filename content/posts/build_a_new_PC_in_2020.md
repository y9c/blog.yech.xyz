+++
title = "Build a New PC in 2020"
description = ""
featured_image = "/img/pc_assembly_2020.jpg"
date = 2020-02-18T21:17:47+08:00
categories = ["geek"]
tags = ["tech", "hardware", "PC"]
comment = true
+++

## 需求

最近笔记本开始卡顿，加上不知不觉用台式机工作已经几年了，一下子手头没有台式机竟有点没习惯过来。
心想要不就自己组一台吧，也可以把自己的显卡和显示器利用起来。
盘算了一下，理想中的机子大概要符合这几个要求：

- 核心数越多越好，至少得 >8。
- 内存在 32 G 往上。
- ~~体型足够迷你，可以放桌面。~~ _(屈服于现实，最终这一点没能实现)_

## 配置

| Hardware | Spec.             | Price(￥)   |
| -------- | ----------------- | ----------- |
| CPU      | AMD R5 3600       | 1369        |
| 内存     | USCORSTAR DDR4    | 599x2       |
| 机箱     | PHANTEKS P418X    | 269         |
| 散热器   | JONSBO SHADOW 240 | 360         |
| 电源     | Huntkey 600S      | 309         |
| 显卡     | NVIDIA GTX1060    | ~2000(存货) |
| 显示器   | DELL P2415Q       | ~3000(存货) |
| 硬盘     | INTEL SSDSC2BW48  | ~1000(存货) |
| 硬盘     | KINGSTON SV300S3  | ~250(存货)  |
| 硬盘     | SEAGATE 2T        | ~750(存货)  |

## 坎坷历程

- 最先购置的是 MSI B450I 主版，买之前就担心 B450 不能兼容三代的锐龙。网页写明了可以支持 R5 3000 系列，后来与客服的沟通也确认了 9
  月份后的型号出厂即可支持，于是买了 12 月批号的板子。然而经过一天的折腾，依然进不去 BIOS，再次询问客服又改口了，说不一定能支持，得自行升级 BIOS，或是返厂升级。这样看来这个主版应该是旧的批次换了个新的盒子，考虑到二手东的作风，直接退货了。

- 然而 ITX 的主版选择又太少了，加上 X570 的板子多在促销，虽然有些性能过剩，但性价比绝对是高的，也就放弃了 ITX 主机的幻想了 😢，转为购买 Gigabit 的 X570 WiFi Pro。

- 装上 X570 的板子后，发现问题更加严重了，这次直接卡在了 DRAM
  的检测，也就是说内存出问题了。担心是双通道兼容性的问题，不同插槽进行组合，依然无法点亮。接着又用酒精进行擦拭，依然不能点亮，最后一条条排查，发现其中一条无论在哪个插槽都无法点亮，另一条只在某个插槽能识别。这意味着主板和内存都有点毛病。

- 勉强跳过 DRAM 的检测后，发现 VGA 和 BOOT 的检测灯来回闪，插上屏幕后也没图像。查说明书也没查出什么，问客服又让我送回去检测。最后在一个帖子上看到说主板首次进入系统前不支持 DP 线输出，后来换了 HDMI 线，果真还真进入了 BIOS 了，这是这么多天首次看到 BIOS 点亮了。

- 插上固态硬盘后，一波操作，终于把 Linux 系统给安上了。进入系统后各种升级，接着重启，发现卡 BIOS 了，硬盘也不见了。猜测是 SATA 口出了问题，又是各种排列组合。最后发现是个概率问题，只有一定概率能识别硬盘。再次换货 😢。_这里还有个小插曲，在拆机取内存的时候，手一滑，机箱玻璃碎了一地。_

- 等了快一周，新主板也拿到了，安上去的时候，发现彻底不亮。无奈之下，按了下 CPU 风扇，终于点亮了，不过看来~~新~~（_第三次换货的二手_）主板 CPU 的接口也有点毛病。

## 结论

没事的话少在 JD 买东西，尤其是在假期。