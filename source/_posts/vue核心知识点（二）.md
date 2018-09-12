---
title: vue核心知识点（二）
date: 2018-09-12 09:58:41
tags: [vue,组件通信]
---

# Vue

## 组件通信

### 父子组件通信

子组件向父组件传递数据（查看 [demo](http://jsbin.com/wijofehuge/edit?html,css,js,output)）

父组件向子组件传递数据（查看 [demo](http://jsbin.com/momowoqiku/edit?html,js,output)）

<!--more-->

### 非父子组件通信

[查看 demo](http://jsbin.com/motorofiri/edit?html,js,output)

```javascript
创建一个空的vue实例,作为bus
触发组件A中的事件

bus.$emit('event,1)
在组件B中的钩子函数中监听事件

bus.$on('event',function(){
    // ......
})
子组件通过`this.$parent可以修改父组件的数据
父组件通过this.$refs.xxx.数据,可以获取到自组件中的内容(给子组件添加索引ref=”xxx”)
```

## vue 中 keep-alive 组件的作用

keep-alive：主要用于保留组件状态或避免重新渲染。

比如： 有一个列表页面和一个 详情页面，那么用户就会经常执行打开详情=>返回列表=>打开详情这样的话 列表 和 详情 都是一个频率很高的页面，那么就可以对列表组件使用`<keep-alive></keep-alive>`进行缓存，这样用户每次返回列表的时候，都能从缓存中快速渲染，而不是重新渲染。

### include 和 exclude 属性

include 和 exclude 属性允许组件有条件地缓存。二者都可以用逗号分隔字符串、正则表达式或一个数组来表示(具体的参见文档)

## 可复用的组件

在编写组件的时候，时刻考虑组件是否可复用是有好处的。一次性组件跟其他组件紧密耦合没关系，但是可复用组件一定要定义一个清晰的公开接口。

Vue.js 组件 API 来自 三部分：prop、事件、slot：

prop 允许外部环境传递数据给组件，在 vue-cli 工程中也可以使用 vuex 等传递数据。
事件允许组件触发外部环境的 action
slot 允许外部环境将内容插入到组件的视图结构内。
