---
title: Node.js入坑记（一）
date: 2018-10-1 20:33:28
tags: [node.js]
---
未完成
# Node.js

> 任何能够用 JavaScript 实现的应用系统，最终都必将用 JavaScript 实现
是时候入坑 node.js 了，几个月前 deno 都开始了，vue3.0 的计划已经出来了，扶我起来。我还学的动

## 什么是 Node.js

Node.js 是一个 JavaScript 的运行时环境，构建在 chrome v8 引擎之上。采用事件驱动，非阻塞 I/O 模型，轻量且高效，让并发编程更加简单。使用 npm 作为包管理器。

## 基本原理

Node.js内置v8引擎，所以使用Javascript语法，所以是单线程。由于I/O的速度慢，就必须要等结果出来，才能运行后边的任务。所以引入event loop，把等待中的I/O任务放到事件循环里，然后放到线程池，保证cpu能够尽力运行


