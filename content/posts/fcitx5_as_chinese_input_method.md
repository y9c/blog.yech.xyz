+++
title = "Fcitx5 as Chinese Input Method"
description = "Fcitx is a lightweight input method framework aimed at providing environment independent language support for Linux."
featured_image = "/img/fcitx5_input_method.png"
date = 2020-02-06T17:13:56+08:00
categories = ["coding"]
tags = ["chinese", "linux", "archlinux"]
comment = true
+++

> 安装 Archlinux 最后一件事往往是安装搜狗输入法，这也是最困难的一件事。
>
> - 从 AUR 编译源码需要花费大量的时间（_低配置的 Laptop 上需要半天_）。
> - 为了兼容 QT4, QT5, GTK4, GTK5, XIM 等框架的应用，需要各种调试。
> - 搜狗输入法带有 bug，经常无法调出输入法，或是输入皮肤不显示。
>
> 这直到 fcitx5 发布，一切终于有了转机会。
> 若非进行大量的中文写作，fcitx5 完全可以胜任日常的中文输入。

fcitx5 安装及配置步骤也非常简单，而且稳定性出奇的好。大致步骤如下：

1. **安装 fcitx5**：

   从 AUR 安装[^1]：

   ```bash
   yay -S fcitx5-git fcitx5-qt5-git fcitx5-gtk-git fcitx5-chinese-addons-git
   ```

   若配置了 ArchlinuxCN[^2]，从 ArchlinuxCN 安装：

   ```bash
   pacman -S fcitx5-git fcitx5-qt5-git fcitx5-gtk-git fcitx5-chinese-addons-git
   ```

2. **设置 fcitx5 的开启**：

   基于 Xorg 的桌面环境，添加配置到 ~/.xprofile：

   ```
   export GTK_IM_MODULE=fcitx5
   export XMODIFIERS="@im=fcitx"
   export QT_IM_MODULE=fcitx5
   fcitx5 > /dev/null &
   ```

   基于 Wayland 的桌面环境，添加配置到 ~/.pam_environment：

   ```
   GTK_IM_MODULE DEFAULT=fcitx5
   QT_IM_MODULE DEFAULT=fcitx5
   XMODIFIERS DEFAULT=@im=fcitx5
   ```

3. **配置 fcitx5**：

   (**配置时需要关闭 fcitx !!!**)

   - 在 `~/.config/fcitx5/profile` 中添加：

   ```
   [Groups/0]
   # Group Name
   Name=Default
   # Layout
   Default Layout=us
   # Default Input Method
   DefaultIM=pinyin

   [Groups/0/Items/0]
   # Name
   Name=keyboard-us
   # Layout
   Layout=

   [Groups/0/Items/1]
   # Name
   Name=pinyin
   # Layout
   Layout=

   [GroupOrder]
   0=Default
   ```

   - 下载主题[^3]：

   ```
   git clone https://github.com/weearc/fcitx5-skin-simple-blue.git ~/.local/share/fcitx5/themes/simple-blue
   ```

   **开启 fcitx5 然后关闭，让其自动生成配置文件。**

   - 启用主题并设置字体：

   在 `~/.config/fcitx5/conf/classicui.conf` 中添加：

   ```
   # True, if you want a vertical candidate list
   Vertical Candidate List=False
   # Use Per Screen DPI
   PerScreenDPI=True
   # Font for Chinese and English, then font size
   Font="Noto Sans CJK SC Regular Noto Sans Regular 11"
   # Theme
   Theme=simple-blue
   ```

   其中，`Theme` 为下载的主题文件夹名称，`Font` 设置输入法的显示字体及字号。

   - 配置拼音输入法（针对 fcitx5-chinese-addons）：

   在 `~/.config/fcitx5/conf/pinyin.conf` 中修改，使得 `<`, `>` 键可以用于翻页：

   ```
   [PrevPage]
   0=minus
   1=Up
   2=comma

   [NextPage]
   0=equal
   1=Down
   2=period
   ```

   - 配置拼音输入法中的云拼音输入法（同样针对 fcitx5-chinese-addons）：

   > **尝试了很多次才知道配置参数为 `Backend` 而不是 `CloudPinyinBackend`，被代码的命名误导了。配置文件是独立的文件，而不是放在 `pinyin.conf` 里面**

   在 `~/.config/fcitx5/conf/cloudpinyin.conf` 中修改云拼音的来源从 Google 修改为 Baidu。

   ```
   # Minimum Pinyin Length
   MinimumPinyinLength=4
   # Backend
   Backend=Baidu
   ```

> Reference

[^1]: yaourt 已经停止维护了，用 yay [替代](https://zhuanlan.zhihu.com/p/42287487)。
[^2]: 从 [ArchlinuxCN](https://www.archlinuxcn.org/archlinux-cn-repo-and-mirror/) 下载预编译的安装包，可以省去编译的时间。
[^3]: 另外推荐两款皮肤：[adwaita-dark](https://github.com/escape0707/fcitx5-adwaita-dark.git) 和 [Material-Color](https://github.com/hosxy/Fcitx5-Material-Color.git)。
