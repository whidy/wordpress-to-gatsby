---
author: whidy
comments: true
date: 2012-11-30 02:05:25+00:00
layout: post
link: http://www.whidy.net/horizontally-center-elements-of-a-dynamic-width.html
slug: horizontally-center-elements-of-a-dynamic-width
title: 如何让元素水平居中于动态宽度页面或容器中
wordpress_id: 1167
categories:
- CSS
- HTML
- IT技术
- 原创翻译
- 精彩分享
tags:
- 技术
- 教程
---

现如今,自适应窗口的页面布局已经十分常见了,那么不同的显示器,不同的人群可能在查看页面时的显示效果必然不会相同.为了保证风格整体一致,那么在一个动态变化宽度的页面或容器中,元素居中将被常常用到.这里我并不是简简单单的给div加上一个text-align:center;属性后,其单独的块级子元素(例如img)自动居中,这种方法估计人人皆知.我将用另一个办法解决这个问题,例如子元素内比较复杂的导航条等等.这里我就以导航条的居中为例.

先来看看相关效果:

<del>http://jsfiddle.net/kingterrors/AqTJV/embedded/result,html,css/</del>

PS:由于近日(2014年6月)jsfiddle无法正常访问,可能受内网影响,现将之前所有jsfiddle预览去除,不过你仍然可将以上地址拷贝到浏览器预览,或选择尝试以下代码:


    
    <code class="html"><!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>Horizontally center elements of a dynamic width</title>
    <style type="text/css">
    ul {display:table;margin:10px auto;min-width:320px;}
    li {float:left;list-style:none;margin-left:5px;padding:5px 0;}
    li:first-child { margin-left:0;}
    li a {background:#82B5DA;border:1px solid #599CCE;border-radius:3px;box-shadow:0 0 3px rgba(0,0,0,0.3);padding:5px;color:#333;text-decoration:none;text-shadow:1px 1px 0 rgba(255,255,255,0.3);}
    li a:hover { background:#599CCE;}
    </style>
    </head>
    <body>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Blog</a></li>
      <li><a href="#">Tutorials</a></li>
      <li><a href="#">About whidy</a></li>
    </ul>
    </body>
    </html>
    </code>



如果点了CSS查看,大家会发现这里用了display: table;这个估计很少会有人用,而且它有个很大的问题,就是这种居中的方式仅仅支持IE8+,那么IE7-不是悲剧了.因此,这里又提供一个更好的方案:

<del>http://jsfiddle.net/kingterrors/AgxR5/embedded/result,html,css/</del>

PS:由于近日(2014年6月)jsfiddle无法正常访问,可能受内网影响,现将之前所有jsfiddle预览去除,不过你仍然可将以上地址拷贝到浏览器预览,或选择尝试以下代码:


    
    <code class="html"><!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>Horizontally center elements of a dynamic width</title>
    <style type="text/css">
    ul {margin-top:10px;text-align:center;min-width:330px;}
    li {display:inline-block;list-style:none;margin-left:5px;padding:5px 0;}
    li:first-child {margin-left:0;}
    li {background:#82B5DA;border:1px solid #599CCE;border-radius:3px;box-shadow:0 0 3px rgba(0,0,0,0.3);padding:5px;color:#333;}
    li:hover {background:#599CCE;}
    li a {color:#333;text-decoration:none;text-shadow:1px 1px 0 rgba(255,255,255,0.3);}
    li {*display:inline;zoom:1;}
    </style>
    </head>
    <body>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Blog</a></li>
      <li><a href="#">Tutorials</a></li>
      <li><a href="#">About whidy</a></li>
    </ul>
    </body>
    </html>
    </code>



这里有几点需要说明的是,块级元素前面已经提到是可以直接用text-align:center;居中的,而内联的也就是含有浮动的块级元素怎么处理呢,IE7对这个内联块级支持仍然不是很好.那么我们还要给li元素增加一个inline-block. zoom: 1;这样IE7就能很好的工作了.IE6好像还有点问题,那么就让IE 6 去shit吧.

总结:这是一个十分简单的关于动态宽度的页面或容器内元素自动居中的例子,我也参考过其他网友的方法,比如利用父子关系的定位,父级元素相对定位,子级元素按照百分比绝对定位的方法,不过个人感觉过于复杂,大部分情况下如果采用此文的方法也许会更好些.当然,面对不同的情景,大家也就根据自己需要进行选择了.

参考文章:http://css-plus.com/2012/05/how-to-horizontally-center-elements-of-a-dynamic-width/
