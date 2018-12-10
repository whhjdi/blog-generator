---
title: 我知道的JS-深浅拷贝
date: 2018-04-15 8:07:49
tags: [JavaScript]
categories: ["Javascript"]
cover_img: https://ws3.sinaimg.cn/large/006tNbRwly1fy1m07rhyej30zk0k0atc.jpg
---

# 深浅拷贝

对于简单类型的数据来说，赋值就是深拷贝
对于复杂类型的数据（对象）来说，才要区分浅拷贝和深拷贝

## 赋值

传递对象的引用而已,原始列表 a 改变，被赋值的 b 也会做相同的改变

<!-- more -->

```javascript
var a = { name: "muxue" };
var b = a;
b.name = "b";
a.name === "b"; // true
```

## 浅拷贝

拷贝父对象，不会拷贝对象的内部的子对象。即拷贝 a 里面的一级元素的内存地址，不拷贝 a 里的小列表里的元素的内存地址。所以有时候我们需要引入深拷贝来解决这个问题

Object.assign

```javascript
var a = { name: "muxue", age: [18, 19] };
var b = Object.assign({}, a);
b.name = "b";
b.age[0] = 20;
a.name === "b"; //false
a.age[0] === 20; //true
```

展开运算符(...)

```javascript
var a = { name: "muxue", age: [18, 19] };
var b = { ...a };
b.name = "b";
b.age[0] = 20;
a.name === "b"; //false
a.age[0] === 20; //true
```

## 深拷贝

通常使用 JSON.parse(JSON.stringify(object))来进行深拷贝，但是这个方法有缺陷

1. 会忽略 undefined
2. 不能序列化函数
3. 不能解决循环引用的对象

```javascript
var a = { name: "muxue", age: [18, 19] };
var b = JSON.parse(JSON.stringify(a));
b.name = "b";
b.age[0] = 20;
a.name === "b"; //false
a.age[0] === 20; //false
```

递归拷贝

```javascript
function clone(object) {
  var object2;
  if (!(object instanceof Object)) {
    return object;
  } else if (object instanceof Array) {
    object2 = [];
  } else if (object instanceof Object) {
    object2 = {};
  } else if (object instanceof Function) {
    object2 = eval(object.toString());
  }
  for (let key in Object) {
    object2[key] = clone(object[key]);
  }
  return object2;
}
```
