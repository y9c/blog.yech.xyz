+++
title = "治好了键盘的一个毛病"
description = ""
featured_image = "/img/anne_keyboard.jpg"
date = 2019-02-25T02:05:02+08:00
tags = ["coding", "hardware"]
categories = ["geek"]
comment = true
+++

困扰了两年的键盘小 bug 解决了。

## 起因

机械键盘为了防止游戏玩家误触 `WIN` 键，专门加入了 `WIN_LOCK` 模式，由 `Fn+WIN` 触发。
这对编程来说简直是噩梦，一旦用到了需要触发 `WIN` 和 `Fn` 的组合键，例如 `WIN+箭头`，这时 `WIN` 键位就给锁上了。

<!--more-->

## 解决方案

1. **安装 `dfu-util`**

```bash
sudo pacman -S dfu-util
```

1. **下载 [V1.40.02 固件](http://en.obins.net/firmware#1J)**

1. 按住 `Esc` 键不放，戳键盘背后的 Reset 按钮，释放 `Esc` 键。
   (注意，此处的 `Esc` 是原先的 `Esc` 键位，不是修改后的 `Esc` 键。
   键盘和电脑用 USB 线保持连接，不是断开。)

1. **写入固件**

```bash
dfu-util --alt 0 --intf 0 --download xxx_NoWinLock.dfu
```

1. 戳键盘背后的 Reset 按钮，退出 dfu 模式。

1. 通过蓝牙手机 APP 重设键位。
   这时候 `WIN_L` 依然会对应 WIN_LOCK，只是因为 APP 的原因，键盘已经生效。
