---
author: whidy
comments: true
date: 2013-08-12 08:14:11+00:00
layout: post
link: http://www.whidy.net/xianjian-ol-solution.html
slug: xianjian-ol-solution
title: 新仙剑OL网吧无法正常运行解决方法之一
wordpress_id: 1751
categories:
- IT技术
- 技术分享
tags:
- 技术
---

最近在网吧上网，下载了插件却依然无法正常运行新仙剑OL，特点是插件无法正常运行，在网上寻求解决方案得知一个服务未能启用，这个服务就是terminal service，将这个服务启用就好了。但是每次来网吧都要操作一遍很是繁琐。于是随便研究了一下，写了一个命令行，直接运行，如果网吧连CMD.EXE都屏蔽了就麻烦了哦，那么下面共享出这段代码。分别执行！


<blockquote>sc config termservice start= auto
net start termservice</blockquote>


之后在运行游戏试试哦
