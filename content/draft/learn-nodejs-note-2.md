title: node.js学习笔记(二)
date: 2015-12-22 00:09:42
tags: [coding,nodejs,tech]
---

# 网页端的javascript和服务端的nodejs的区别

网页端
---

```javascript
>  var a = 1;
<. 1
>  a
<. 1
>  window.a
<. 1
>  global.a
<. **Uncaught ReferenceError: global is not defined(…)**
```

服务端
---

```javascript
>  var a = 1;
<. 1
>  a
<. 1
>  window.a
<. ReferenceError: window is not defined
>  global.a
<. 1
```
