---
title: 我知道的JS-继承
date: 2018-04-10 22:49:21
tags: [JavaScript]
categories: ["Javascript"]
cover_img: https://ws3.sinaimg.cn/large/006tNbRwly1fy1m17r3gyj30qe0ipwrf.jpg
---

# 继承

继承可以使得子类具有父类的各种属性和方法

## ES5 中的继承

```javascript
function Human(name) {
  this.name = name;
}
Human.prototype.run = function() {
  console.log("i can run");
};
function Man(name) {
  Human.call(this, name);
  this.gender = "男";
}
Man.prototype.fight = function() {
  console.log("fight");
};
//如果 Man.prototype.__proto__ = Human.prototype就实现了继承
// 但是这样写是不允许的
var f = function() {};
f.prototype = Human.prototype;
Man.prototype = new f();
```

<!--more-->

## ES6 中的继承

```javascript
class Human {
  constructor(name) {
    this.name = name;
  }
  run() {
    console.log("i can run");
  }
}
class Man extends Human {
  constructor(name) {
    super();
    this.gender = "男";
  }
  fight() {
    console.log("fight");
  }
}
```
