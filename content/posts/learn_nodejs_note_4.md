+++
title = "node.js 学习笔记(四)"
date = 2015-12-23T14:42:59+08:00
tags = ["coding", "nodejs"]
categories = ["geek"]
draft = false
+++

# 用 node 的 express 插件创建应用

- 创建项目环境

```bash
$ mkdir myapp
$ cd myapp
$ npm install express --save
$ vim app.js
```

- 编写 javascript 脚本

```javascript
//app.js 内容

var express = require("express");
var app = express();

app.get("/", function(req, res) {
  res.send("Hello World!");
});

var server = app.listen(3000, function() {
  var host = server.address().address;
  var port = server.address().port;
  console.log("Example app listening at http://%s:%s", host, port);
});
```

- 启动服务,监听 3000 端口

```bash
node app.js
```
