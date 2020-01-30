+++
title = "ArchLinux 系统中的字体配置"
description = ""
featured_image = ""
date = 2020-02-19T16:59:41+08:00
categories = ["coding"]
tags = ["fonts", "linux", "desktop"]
comment = true
+++

Linux 系统中多采用 Fontconfig 对字体进行管理和配置。
其配置文件[^1]为 XML 的格式，可以通过对字体进行映射来实现“重命名”的效果。

> 为什么安装了 Noto 的中文字体，但是依然没法在网页中正常调用？

ArchLinux 中的 noto-fonts-cjk 字体包会安装`Noto Serif CJK TC`、`Noto Serif CJK KR`、`Noto Serif CJK SC` 等字体文件，但是网页中的 Noto 中文字体调用多为`Noto Serif SC`这样的命名，导致安装字体后不起作用。因此可以对`Noto Serif SC`字体的调用进行映射：

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
    <match target="pattern">
        <test qual="any" name="family">
            <string>Noto Serif SC</string>
        </test>
        <edit name="family" mode="assign" binding="same">
            <string>Noto Serif CJK SC</string>
        </edit>
    </match>
    <match target="pattern">
        <test qual="any" name="family">
            <string>Noto Serif TC</string>
        </test>
        <edit name="family" mode="assign" binding="same">
            <string>Noto Serif CJK TC</string>
        </edit>
    </match>
</fontconfig>
```

- `fc-cache -fv` 重新生成字体配置的缓存。
- `fc-list` 查看系统中的字体文件信息，但配置中的字体印射不在结果中显示。
- `fc-match "mono"` 测试系统字体的调用。

[^1]: Fontconfig 2.10.1 版本后的用户配置位于 `$XDG_CONFIG_HOME/fontconfig/fonts.conf` 和 `$XDG_CONFIG_HOME/fontconfig/conf.d/xxx.conf`，一般也就是`~/.config/fontconfig/fonts.conf`文件中，或是`~/.config/fontconfig/conf.d/` 文件夹中的配置文件中。
