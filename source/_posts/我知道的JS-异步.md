---
title: 我知道的JS-异步
date: 2018-04-09 15:40:17
tags: [JavaScript]
---

# 异步

## Promise

Promise 是 Es6 新增的语法，为了解决回调地狱的问题
Promise 有三种状态，pending(初始状态)，可以通过函数 resolve 和 reject 把状态变为 resolved 或者 rejected，状态只能改变一次

```javascript
function xxx(){
    return new Promise(function(resolve,reject){
        setTimeout(()=>{
            resolve()
            //或者
            //reject()
        },1000)
    })
}
xxx().then(......)
```

<!--more-->

## async/await

Es8 引入的 async 函数，可以更加方便的处理异步

一个函数如果加上 async ，那么该函数就会返回一个 Promise

```javascript
function returnPromise() {
  return new Promise(function(resolve, reject) {
    setTimeout(() => {
      console.log("finish");
      resolve("muxue");
    }, 3000);
  });
}

//之前我们可以这样写
// returnPromise().then(result => {
//     console.log(result)
// });

async function test() {
  let result = await returnPromise(); // 注意只有控制台支持顶级作用域的 await，JS 文件里的 await 只能写在 async 函数里
  console.log(result);
}
test();
```
