---
title: Mac前端开发环境配置
date: 2018-10-03 11:55:57
tags: [Mac]
categories: ["其他"]
---

# Mac

## 安装 Homebrew

前提是科学上网

```bash
# 安装Xcode命令行工具
$ xcode-select --install
# 安装homebrow
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## 安装必备工具

```bash
brew install coreutils vim node git wget
```

<!--more-->

## git 和 github

### github 配置

打开命令行运行

```bash
ssh-keygen -t rsa -b 4096 -C "你的邮箱"
```

按回车三次，然后运行

```bash
cat ~/.ssh/id_rsa.pub
```

复制得到的字符串，然后打开 github，
进入[ssh keys](https://github.com/settings/keys)
点击 `New SSH Key` ，粘贴到 key 里，点击`add key`,完成
然后在命令行运行

```bash
ssh -T git@github.com
```

查看是否成功，yes 回车

### git 配置

```bash
git config --global user.name 你的英文名字
git config --global user.email 你的常用邮箱
git config --global push.default simple
git config --global core.quotepath false
git config --global core.editor "vim"
```

搞定

## iterm2&oh my zsh

参考[田园里的蟋蟀](https://www.cnblogs.com/xishuai/p/mac-iterm2.html)
和 github 文档

## hexo 博客迁移

clone 你的博客备份
进入你的博客的根目录

```bash
#安装hexo
npm install hexo-cli -g
#安装依赖
npm install
npm install hexo-deployer-git --save
npm install hexo-generator-feed --save
npm install hexo-generator-sitemap --save
```

现在就可以正常使用 hexo 写博客啦
