title: node.js学习笔记(三)
date: 2015-12-23 14:42:59
tags: [coding,tech,javascript]
---

# 用node的express插件创建应用

- 创建项目环境

```bash
$ mkdir myapp
$ cd myapp
$ npm install express --save
$ vim app.js
```

- 编写javascript脚本

```javascript
//app.js 内容

var express = require('express')
var app = express()

app.get('/', function (req, res) {
  res.send('Hello World!')
  })

var server = app.listen(3000, function () {
  var host = server.address().address
  var port = server.address().port
  console.log('Example app listening at http://%s:%s', host, port)
})
```

- 启动服务,监听3000端口
```bash
node app.js
```
