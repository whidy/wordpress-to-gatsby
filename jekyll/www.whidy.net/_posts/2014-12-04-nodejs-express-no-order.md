---
author: amo
comments: true
date: 2014-12-04 13:50:29+00:00
template: post
draft: false
link: http://www.whidy.net/nodejs-express-no-order.html
slug: /nodejs-express-no-order
title: 安装express后验证显示没有相应命令
wordpress_id: 2654
category: '开发'
---

要总结什么规律，想自己写点东西出来，但是java的东西，公司已经限定死了，不使用优秀的开源框架，前端的js是不限制的，发现nodejs可以使用来开发后台的东西，直接操作文件也是可以的，于是就想使用nodejs来写。

安装了一个web的框架exress，是安装网上说的方法

sudo npm install -gd express

在命令行里敲express -V没有反映，出现/usr/bin/env:node No such file or directory的错误，别的说什么要安装一个工具集，

sudo npm install -g express-generator

擦，搞完之后敲express -V还是没有用，后来找usr/local/bin里面的express文件打开看，开头引用的是：#!/usr/bin/env node

引用的是node命令，但是node命令在安装了nodejs后一直使用的是nodejs的命令，在user/bin中可以找到nodejs的可执行文件，也就是在环境变量里只有nodejs，没有node，所以我直接在这个文件夹里sudo cp nodejs node

事实上我觉得，直接在这个文件夹下建立一个软链接，貌似也是可以用的，只是没有测试过。有兴趣可以自己试一下。

搞完之后直接敲express -V，ok，出来想要的东西了。其实还有很多nodejs的包在用npm下载之后是默认调用的node这个命令。因此，在环境变量中添加一个node命令还是比较靠谱的说。
