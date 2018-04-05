title: node.js学习笔记(一) 
date: 2015-12-21 14:01:05
tags: [coding, nodejs, tech]
---

# 运行环境

> 两种,类似python

- 命令行交互

```bash
$ node
```

```javascript
> console.log("Hello World");
```

- 文件运行(无需编译)

```bash
$ echo 'console.log("Hello World")' > helloworld.js
$ node helloworld.js
```
---

# 函数传递

```javascript
function say(world){
 console.log(world);
}

function execute(someFunction, value){
 someFunction(value)
}

execute(say,"Hello YC");
```

等价于

```javascript
function execute(someFunction, value){
 someFunction(value)
}

execute(function(word){console.log(word)},"Hello YC");
```
其中say()函数不需要命名,作为匿名函数

# 模块调用

## server.js

```javascript
var http = require("http");

function start() {
 function onRequest(request, response) {
  console.log("Request received.");
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello YC");
  response.end();
 }

 http.createServer(onRequest).listen(8888);
 console.log("Server has started.");
}

exports.start = start;
```

## index.js

```javascript
var server = require("./server");

server.start();
```

直接node index.js 运行，会调用server.js
