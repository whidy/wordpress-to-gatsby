---
author: whidy
comments: true
date: 2014-05-24 09:14:19+00:00
layout: post
link: http://www.whidy.net/ie6-and-ie7-has-a-different-distance-bug.html
slug: ie6-and-ie7-has-a-different-distance-bug
title: IE6和IE7在同级相邻元素间边距问题
wordpress_id: 2333
categories:
- CSS
- HTML
- IT技术
tags:
- 技术
---

IE6和IE7一向令网页制作者头痛,虽然有些经验丰富的前端开发人员能快速解决大部分问题,但是有时候,仍然会遇到一些令人疑惑的问题.我在做一个简单效果时,发现有时候及时清浮并不是一件好事,通过触发**hasLayout**反而出了问题.接下来详细说说这个IE6和IE7的问题.

两个同级的相邻的元素A和B(均为块级元素),当A内部有元素浮动,并且拥有外边距时,B则会贴紧A的最后一个元素,假设B没有清除浮动,则会与A的最后一个元素的左右边距保持边距距离,例如图一:

[caption id="attachment_2338" align="aligncenter" width="400"][![B没有清浮的情况下,左右边距正常](http://www.whidy.net/wp-content/uploads/2014/05/B-no-clear-400x531.png)](http://www.whidy.net/wp-content/uploads/2014/05/B-no-clear.png) B没有清浮的情况下,左右边距正常[/caption]

<!-- more -->可以看到有很多差异,当然我今天主要讨论的是边距问题,大家可忽略这很多不同的差异,大家只需要记住图片和代码.那么图一的代码如下:


    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>the two side distance normal!</title>
    <style type="text/css">
    * {margin:0;padding:0;list-style:none;text-align:left;vertical-align:top;}
    .text-list {}
    .text {width:100px;height:100px;border:5px solid #aaa;margin:10px;padding:1px;float:left;display:inline;}
    .extra {height:20px;line-height:20px;background-color:#ddd;}
    </style>
    </head>
    <body>
    <div class="content">
    	<ul class="text-list">
    		<li class="text">Text Here</li>
    		<li class="text">Text Here</li>
    		<li class="text">Text Here</li>
    	</ul>
    </div>
    <div class="extra">Extra infomations Here, Demo test by whidy!</div>
    </body>
    </html>
    ```



好了,这不是重点,接下来看BUG,因为今天要说的是**上下相邻元素间距BUG**!依旧先上图,见图二:

[caption id="attachment_2337" align="aligncenter" width="400"][![清除浮动后的间距BUG](http://www.whidy.net/wp-content/uploads/2014/05/clear-float-BUG-400x750.png)](http://www.whidy.net/wp-content/uploads/2014/05/clear-float-BUG.png) 清除浮动后的间距BUG[/caption]

那么**清除浮动**,有几种办法,

1. 传统方法,给.extra加个clear:both;即可,也不会出现BUG.

2. 给.text-list加个overflow:hidden;zoom:1;来清除浮动.

3. 用流传的万能的clearfix,添加到ul的类中,实际跟方法2原理相同

重点是,我在实际页面制作中是有需要给**.text-list**或者**.content**加一个**宽度**,所以我选择了方法2,于是出现了图二的情况

我很奇怪,类名为text元素的下边距哪里去了,理应方法二清除浮动,他会重新计算内部整体高度,可是事实并非如此,先上我这个错误代码:


    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>Do not hasLayout!</title>
    <style type="text/css">
    * {margin:0;padding:0;list-style:none;text-align:left;vertical-align:top;}
    .text-list {width:500px;overflow:hidden;zoom:1;}
    .text {width:100px;height:100px;border:5px solid #aaa;margin:10px;padding:1px;float:left;display:inline;}
    .extra {height:20px;line-height:20px;background-color:#ddd;}
    </style>
    </head>
    <body>
    <div class="content">
    	<ul class="text-list">
    		<li class="text">Text Here</li>
    		<li class="text">Text Here</li>
    		<li class="text">Text Here</li>
    	</ul>
    </div>
    <div class="extra">Extra infomations Here, Demo test by whidy!</div>
    </body>
    </html>
    ```



我反复尝试各种调试,用尽各种清浮.各种测试方案,绞尽脑汁花了很长时间终于找出这个错误代码的究竟是如何影响了.

**问题就出在.text-list的样式上**.删掉就好.另外,清浮必须采用**给extra元素加clear:both;**这是唯一方法,至于宽度问题,让它auto就好吧...最终应该正确的代码:


    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>looks good</title>
    <style type="text/css">
    * {margin:0;padding:0;list-style:none;text-align:left;vertical-align:top;}
    .text-list {}
    .text {width:100px;height:100px;border:5px solid #aaa;margin:10px;padding:1px;float:left;display:inline;}
    .extra {height:20px;line-height:20px;background-color:#ddd;clear:both;}
    </style>
    </head>
    <body>
    <div class="content">
    	<ul class="text-list">
    		<li class="text">Text Here</li>
    		<li class="text">Text Here</li>
    		<li class="text">Text Here</li>
    	</ul>
    </div>
    <div class="extra">Extra infomations Here, Demo test by whidy!</div>
    </body>
    </html>
    ```



这个困扰我几天的问题,今天正是双休,抽空研究了一下.总结就是,**触发hasLayout的条件要牢记**,虽然有时候你会意想不到的很普通的属性也会影响到布局,那么就真的要一个个删除检查了.虽然一般解决方案是为了触发hasLayout,这次却是为了不触发hasLayout~
