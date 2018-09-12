---
title: 我知道的JS-防抖和节流
date: 2018-04-05 22:34:16
tags: [JavaScript]
---

# 防抖和节流

之前一直不明白或者弄混两者，也是因为没有遇到这种需求
作用：都是防止函数多次调用
区别：防抖动是将多次执行变为最后一次执行(将多个信号合并为一个信号)，节流是将多次执行变成每隔一段时间执行。

<!--more-->

## 防抖(debounce)

使用场景
input 输入的格式验证
在一个滚动事件中做一些复杂计算或者实现一个按钮的防二次点击操作

延迟执行的防抖函数

```javascript
// func是用户传入需要防抖的函数
// wait是等待时间
const debounce = (func, wait = 50) => {
  // 缓存一个定时器id
  let timer = 0;
  // 这里返回的函数是每次用户实际调用的防抖函数
  // 如果已经设定过定时器了就清空上一次的定时器
  // 开始一个新的定时器，延迟执行用户传入的方法
  return function(...args) {
    if (timer) clearTimeout(timer);
    timer = setTimeout(() => {
      func.apply(this, args);
    }, wait);
  };
};
// 不难看出如果用户调用该函数的间隔小于wait的情况下，上一次的时间还未到就被清除了，并不会执行函数
```

## 节流(throttle)

使用场景
用在比 input,keyup 触发更频繁的事件中，比如，resize,touchmove,scroll 等
适合用于动画相关的场景
