---
author: whidy
comments: true
date: 2012-08-28 13:52:41+00:00
layout: post
link: http://www.whidy.net/sublime-text-2-zencoding-intro.html
slug: sublime-text-2-zencoding-intro
title: Sublime Text 2下使用ZenCoding简介
wordpress_id: 990
categories:
- HTML
- IT技术
- 技术分享
tags:
- sublime text
- 技术
- 教程
---

上次简单全面的介绍了Sublime Text 2这款编辑器,对这个轻巧的编辑器,关注的人还是不少的,我虽然大部分时间还是习惯用Dreamweaver,不过同时也在逐渐适应这款编辑器,并时不时研究一下,今天将为大家分享一个关于Sublime Text 2插件ZenCoding的简单说明和使用方法.

首先是ZenCoding的安装方法,这里不详述,可以参考之前写过的一篇文章[<<Sublime Text 2 注册激活办法以及简单的使用介绍>>](/sublime-text-2-cracked-and-how-to-use-it.html),首先我们看一下来自国外Vimeo的[演示视频](http://v.youku.com/v_show/id_XNDQ0MjE1MzIw.html).

看完这段视频大家一定会觉得很神奇吧.不过这个视频是3年前录制的,如果需要下载原版清晰的视频,请点击:[<<原版视频介绍>>](http://sdrv.ms/SOAtYz)可能是当时的版本区别问题,貌似跟现在的Sublime Text 2操作略有不同.

不过大家就算在Sublime Text 2下安装了Zencoding插件,去不知道怎么使用,那么这的确很让人无奈,我就简单分享一下,让大家更快更容易上手.首先关于快速自动生成代码的快捷键是"**Ctrl+Alt+Enter**",它会在程序底部弹出一个输入框.那么你可以尽情的按照视频介绍中的方法来使用,具体什么效果试试就知道了;另一个方面,还有个"**Ctrl+Alt+Shift+H**"组合键可以在你的新建的文件中快速生成html页面的基本结构代码,一般作为测试简单的脚本之类的超级方便 :twisted:

这里简单介绍将简单的缩写代码展开方式及规律,Sublime Text 2支持的属性和操作符的列表:



	
  * E
元素名称(div, p);

	
  * E#id
使用id的元素(div#content, p#intro, span#error);

	
  * E.class
使用类的元素(div.header, p.error.critial). 你也可以联合使用class和idID: div#content.column.width;

	
  * E>N
子代元素(div>p, div#footer>p>span);

	
  * E+N
兄弟元素(h1+p, div#header+div#content+div#footer);

	
  * E*N
元素倍增(ul#nav>li*5>a);

	
  * E$*N
条目编号 (ul#nav>li.item-$*5);


随便试几个便知道效果了 8)

另外,如果用户需要自定义上文出现的红色加粗的快捷键,或者查看更多快捷键,可以打开这个配置:

[caption id="attachment_1000" align="aligncenter" width="400"][![SublimeText2 zenCoding配置](/wp-content/uploads/2012/08/SublimeText2zenCoding-400x253.jpg)](/wp-content/uploads/2012/08/SublimeText2zenCoding.jpg) SublimeText2 zenCoding配置[/caption]

于是可以看到这个配置文件,双击keys,就能看到所有快捷键设置了

最后感谢作者神飞的[Zen Coding: 一种快速编写HTML/CSS代码的方法](http://www.qianduan.net/zen-coding-a-new-way-to-write-html-code.html),我也是参考了他的文章的.
