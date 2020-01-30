+++
title = "在浏览器中登陆terminal"
date = 2015-12-26T17:50:49+08:00
tags = ["net", "server"]
categories = ["coding"]
draft = false
+++

chrome 的应用 `secure shell` 能非常方便的实现 SSH 客户端的功能，并且能像修改网页属性那样修改应用的外观。

安装和配置都非常简单。

<!--more-->

## 安装

```
https://chrome.google.com/webstore/detail/secure-shell/pnhechapfaindjhompbnflcldabbghjo/related?utm_source=chrome-app-launcher-info-dialog
```

## 配置

```
{
   "magic":"nassh-prefs",
   "version":2,
   "nassh":{
      "profile-ids":[
         {
            "id":"c509",
            "json":{
               "description":"yc@172.22.49.95:22",
               "username":"yc",
               "hostname":"172.22.49.95",
               "port":22
            }
         }
      ]
   },
   "hterm":{
      "default":{
         "background-color":"rgba(0, 43, 54, 1)",
         "cursor-color":"rgba(238, 232, 213, 0.5)",
         "color-palette-overrides":{
            "0":"#073642",
            "1":"#dc322f",
            "2":"#859900",
            "3":"#b58900",
            "4":"#268bd2",
            "5":"#d33682",
            "6":"#3aa198",
            "7":"#eee8d5",
            "8":"#002b36",
            "9":"#cb4b16",
            "10":"#586e75",
            "11":"#657b83",
            "12":"#839496",
            "13":"#6c71c4",
            "14":"#93a1a1",
            "15":"#fdf6e3"
         },
         "font-family":"\"DejaVu Sans Mono\", 'Droid Sans Mono for Powerline', PowerlineSymbols",
         "foreground-color":"rgba(238, 232, 213, 1)",
         "user-css":"https://cdn.rawgit.com/JayXon/powerline-web-fonts/master/DroidSansMono.css"
      }
   }
}
```
