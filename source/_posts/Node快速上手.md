---
title: Node快速上手
date: 2019-03-31 10:28:00
tags: [Node]
cover_img: https://ws1.sinaimg.cn/large/006tKfTcly1g1lrun4j2oj31kw0sqgqf.jpg
feature_img:
description:
keywords: [Node]
---

# Node

> Node.js 是一个开源跨平台的运行环境，用来在浏览器外执行JavaScript代码
>
> Node是创建高拓展性，数据密集型和实时的后端服务的理想型 工具

##  起源 

2009年之前，浏览器是运行js的唯一环境，直到Ryan Dahl使用V8引擎，用c++实现了Node

无阻塞，异步的特性使得Node具有很高的拓展性

## global

不同于浏览器的全局的window,在Node中global是全局对象

```javascript
setTimeout()

clearTimeout()

setInterval()

clearInterval()
```

## 模块系统

声明的变量并不添加到global对象中，而是在当前文件中，每一个文件都可以看作一个模块。所以我们需要一种导入导出模块的机制


```javascript
function log(){
  console.log('log')
}
//1. 通过对象的形式导出
module.exports.log  = log 
//在另一个文件中就可以通过 require引入来调用
const logger = require('路径')
logger.log()

//2. 直接导出
module.exports = log 
//在另一个文件中就可以通过 require引入来调用
const logger = require('路径')
logger()
```
实际上，Node总是用一个包装函数来包裹模块中的代码
```javascript
(function (exports, require, module, __filename, __dirname) {
	//....
})
```

### path模块

打印一下

```javascript
const path = require('path');
var pathObj = path.parse(__dirname)
var pathObj2 = path.parse(__filename)
console.log(pathObj, pathObj2)


{ root: '/',
  dir: '/Users/muxue/Desktop',
  base: 'learn-node',
  ext: '',
  name: 'learn-node' 
} 
{ root: '/',
  dir: '/Users/muxue/Desktop/learn-node',
  base: 'app.js',
  ext: '.js',
  name: 'app' 
}
```

### OS模块

```javascript
const os = require('os')

var totalmem = os.totalmem()
var freemem = os.freemem()
console.log('totalmem: ' + totalmem, );
console.log('freemem: ' + freemem, );

totalmem: 8589934592
freemem: 414740480
```

### fs模块

```javascript
const fs = require('fs')
//同步
const files = fs.readdirSync('./')
console.log(files);
//异步
fs.readdir('./', (err, files) => {
  if (err) {
    console.log(err);
  } else {
    console.log(files);
  }
})

[ 'app.js', 'logger.js' ]
```

### events模块

```javacript
const EventEmitter = require('events')

const emitter = new EventEmitter()
emitter.on('messageLogged', (e) => {
  console.log(e);

})
emitter.emit('messageLogged', {
  id: 1,
  name: 'muxue'
})
```

```javascript
//app.js
const Logger = require('./logger')
const logger = new Logger()

logger.on('messageLogged', (e) => {
  console.log(e);
})

logger.log('message');

//logger.js
const EventEmitter = require('events')
class Logger extends EventEmitter {
  log(msg) {
    console.log(msg);
    this.emit('messageLogged', {
      id: 1,
      name: 'muxue'
    })
  }
}

module.exports = Logger
```



### http模块

```javascript
const http = require('http');

const server = http.createServer(function (req, res) {
  if (req.url === '/') {
    res.write('hello world')
    res.end();
  }
  if (req.url === '/api/name') {
    res.write(JSON.stringify([1, 2, 3]))
    res.end();
  }
})

server.listen(3000)
console.log('Listening on port 3000')
```











