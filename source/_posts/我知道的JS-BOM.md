---
title: 我知道的JS-BOM
date: 2018-04-22 23:07:16
tags: [JavaScript]
---

# BOM

BOM(Browser Object Model) 是指浏览器对象模型，是用于描述这种对象与对象之间层次关系的模型，浏览器对象模型提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。BOM 由多个对象组成，其中代表浏览器窗口的 Window 对象是 BOM 的顶层对象，其他对象都是该对象的子对象。

## 浏览器的组成

浏览器的核心是两部分：渲染引擎和 JavaScript 解释器（又称 JavaScript 引擎）
不同的浏览器有不同的渲染引擎
Firefox：Gecko 引擎
Safari：WebKit 引擎
Chrome：Blink 引擎
IE: Trident 引擎
Edge: EdgeHTML 引擎

渲染引擎处理网页，通常分成四个阶段
解析代码：HTML 代码解析为 DOM，CSS 代码解析为 CSSOM（CSS Object Model）。
对象合成：将 DOM 和 CSSOM 合成一棵渲染树（render tree）。
布局：计算出渲染树的布局（layout）。
绘制：将渲染树绘制到屏幕。

## 重绘（Repaint）和回流（Reflow）

重绘是当节点需要更改外观而不会影响布局的，比如改变 color 就叫称为重绘
回流是布局或者几何属性需要改变就称为回流。

优化
使用 translate 替代 top
使用 visibility 替换 display: none ，因为前者只会引起重绘，后者会引发回流（改变了布局）
把 DOM 离线后修改，比如：先把 DOM 给 display:none (有一次 Reflow)，然后你修改100次，然后再把它显示出来
不要把 DOM 结点的属性值放在一个循环里当成循环里的变量
不要一项一项地改变样式，而是使用 CSS class 一次性改变样式。
不要使用 table 布局，可能很小的一个小改动会造成整个 table 的重新布局
使用 documentFragment 操作 DOM
动画使用 absolute 定位或 fixed 定位，这样可以减少对其他元素的影响。
使用 window.requestAnimationFrame()，因为它可以把代码推迟到下一次重流时执行，而不是立即要求页面重流。
使用虚拟 DOM（virtual DOM）库。

## window

BOM 的核心是 window 对象，它表示浏览器的一个实例。在浏览器中，即是 javascript 访问浏览器窗口的一个接口，又是 ECMAScript 规定的 Global 对象，这就意味着在网页中定义的任意变量、函数、对象都是以 window 作为 Global 对象。

<!--more-->

所有在全局作用域中声明的变量、函数、对象都会作为 window 的属性和方法

属性和方法
[参见阮一峰的 js 教程](https://wangdoc.com/javascript/bom/window.html)

事件
load 事件发生在文档在浏览器窗口加载完毕时。window.onload 属性可以指定这个事件的回调函数。
浏览器脚本发生错误时，会触发 window 对象的 error 事件。我们可以通过 window.onerror 属性对该事件指定回调函数。
