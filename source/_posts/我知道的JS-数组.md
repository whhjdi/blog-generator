---
title: 我知道的JS-数组
date: 2018-04-20 21:44:56
tags: [JavaScript]
---

# 数组

## 数组去重

方法真的特别多，好好总结一下
正整数去重
缺点：得到的数组里的都是字符串,无法区分 1 和“1”

```javascript
var a = [1, 2, 1, 3, 4, 6, 5, 2];
function unique(arr) {
  var hash = {};
  for (let i = 0; i < arr.length; i++) {
    if (!(arr[i] in hash)) {
      hash[arr[i]] = true;
    }
  }
  return Object.keys(hash);
}
unique(a); //["1", "2", "3", "4", "5", "6"]
```

<!-- more -->

Set 去重(ES6) 推荐 喜欢这个

```javascript
var a = [1, "2", 1, 3, 4, 6, 5, 2];
Array.from(new Set(a));
//[1, "2", 3, 4, 6, 5, 2]
```

sort
先排序然后比较和前后的元素比较

```javascript
var a = [1, "2", 1, 3, 4, 6, 5, 2];
function unique(array) {
  return array
    .concat() //复制一个数组，为了不改变原数组
    .sort()
    .filter(function(item, index, arr) {
      return !index || item !== arr[index - 1];
    });
}
unique(a);
//[1, "2", 2, 3, 4, 5, 6]
```

filter 和 indexOf
indexOf 始终返回第一次找到匹配该元素的索引
这个也非常巧妙

```javascript
var a = [1, "2", 1, 3, 4, 6, 5, 2];
function unique(arr) {
  return arr.filter(function(item, index, array) {
    return array.indexOf(item) === index;
  });
}
unique(a);
//[1, "2", 3, 4, 6, 5, 2]
```

常规的方法
定义一个变量数组 result 保存结果，遍历需要去重的数组，如果该元素已经存在在 res 中了，则说明是重复的元素，如果没有，则放入 result 中。

```javascript
var a = [1, "2", 1, 3, 4, 6, 5, 2];
function unique(a) {
  var result = [];

  for (var i = 0, len = a.length; i < len; i++) {
    var item = a[i];

    for (var j = 0, jLen = result.length; j < jLen; j++) {
      if (result[j] === item) break;
    }

    if (j === jLen) result.push(item);
  }

  return result;
}
unique(a);
//[1, "2", 3, 4, 6, 5, 2]
```

数组还有很多的 api 需要大家多多练习，我会以后的文章中总结一下
