---
author: whidy
comments: true
date: 2014-04-10 15:04:26+00:00
layout: post
link: http://www.whidy.net/ie6-arial-double-quote.html
slug: ie6-arial-double-quote
title: 一个小小的双引号引发的思考-XP内IE下的字体(上)
wordpress_id: 1899
categories:
- CSS
- HTML
- IT技术
- 技术分享
tags:
- 技术
---

有个效果如图:

[caption id="attachment_1912" align="aligncenter" width="400"][![这样的双引号只能用图片代替了](http://www.whidy.net/wp-content/uploads/2014/04/quote-400x250.png)](http://www.whidy.net/wp-content/uploads/2014/04/quote.png) 这样的双引号只能用图片代替了[/caption]

本来写了个全无图的效果.不过似乎只能针对XP下有对应的黑体和微软雅黑才行.在公司的WIN7电脑测试本来这个双引号不需要用到背景图,可是回来准备严格测试的时候,发现问题了,在虚拟机上的一个纯净的精简XP上,这个双引号就算用黑体也是大大的两个像圆形的逗号...最终测试无效,只好用背景图实现了.

<!-- more -->

说到这个效果,唯独WIN7以上的系统,IE8以上版本才能很好不需要图片展示出来,为了兼容IE6,7,,,ZHENSHIKUBI!经过数小时测试,只好采用背景图.为了自适应而做的一个**大双引号文字段自适应DEMO**,其实我感觉这个后来改的版本并不好,用了大量hack以及IE判断.我写出来也只是研究一下,希望以后能想到更好的方法.看代码(或打开此[demo页面](http://www.whidy.net/demos/quote/quote_text_icon.html)):


    
    <code class="html"><!DOCTYPE html>
    <html>
    <head>
    <title>大双引号文字段自适应DEMO</title>
    <style type="text/css">
    .container {width: 720px;color: #000;padding:20px;background-color: #eee; text-align: left;position: absolute;top: 200px;left: 220px;}
    .quote {font:bold 160px/160px Arial;height:70px;overflow: hidden;background-image:url(icon-quote.png)\9;background-repeat:no-repeat\9;width:60px\9;height:49px\9;}
    .q-start {position: relative;display:inline;float: left;top: 18px\9;*top:0;left: 5px\9;zoom:1;/* ie6,7字体问题 hack */background-position: 0 0\9;}
    .q-end {position:absolute; margin: -12px 0 0 -15px; margin:0\9;/* ie6,7字体问题 hack */background-position: -60px 0\9;}
    .content {margin:40px 0 0 8px;margin-left:0\9;padding-bottom:30px;position: relative;font:bold 24px/40px "Microsoft YaHei";text-indent:0;text-indent:0.5em\9;}
    </style>
    </head>
    <body>
    	<div class="container">
    	<!--[if !IE]><!--><span class="quote q-start">“</span><!--<![endif]-->
    	<!--[if IE]><!--><span class="quote q-start"></span><!--<![endif]-->
    		<p class="content">HTC于北京时间23：00在英国伦敦和美国纽约同步举行发布会，正式发布新旗舰智能手机HTC One (M8)，0界面等几大亮点。HTC One (M8)带来突破性的设计与质量，拥有一体成型的高质感金属外型设计，5.0英寸1080p屏幕，极窄边框以及平滑柔和的圆弧曲线，机身更加圆润和轻薄。<!--[if !IE]><!--><span class="quote q-end">”</span><!--<![endif]--><!--[if IE]><!--><span class="quote q-end"></span></p>
    	</div>
    </body>
    </html>
    </code>



看着很不爽的一个DEMO,当然这里还有另外一个相对简单多了的DEMO,不过建议在WIN7下的IETESTER测试,似乎虚拟机版本XP是不行的.查看代码(或打开此[DEMO页面](http://www.whidy.net/demos/quote/quote_text.html)):


    
    <code class="html"><!DOCTYPE html>
    <html>
    <head>
    <title>大双引号文字段自适应DEMO</title>
    <style type="text/css">
    .container {width: 720px;color: #000;padding:20px;background-color: #eee; text-align: left;position: absolute;top: 200px;left: 220px;}
    .quote {font:bold 160px/160px Arial;font-family: Arial; height:70px;overflow: hidden;*font-family: 黑体;}
    .q-start {position: relative;display:inline;float: left;*top: 20px;*left: 0px;*text-indent:-6em;/* ie6字体问题 hack */}
    .q-end {position:absolute; margin: -12px 0 0 -15px; *margin: 0 0 0 -15px; *padding-top:8px;/* ie6字体问题 hack */}
    .content {margin:40px 0 0 8px;padding-bottom:30px;position: relative;font:bold 24px/40px "Microsoft YaHei";text-indent:0;}
    </style>
    </head>
    <body>
        <div class="container">
            <span class="quote q-start">“</span>
    		<p class="content">HTC于北京时间23：00在英国伦敦和美国纽约同步举行发布会，正式发布新旗舰智能手机HTC One (M8)，0界面等几大亮点。HTC One (M8)带来突破性的设计与质量，拥有一体成型的高质感金属外型设计，5.0英寸1080p屏幕，极窄边框以及平滑柔和的圆弧曲线，机身更加圆润和轻薄。<span class="quote q-end">”</span></p>
        </div>
    </body>
    </html>
    </code>



关于这个DEMO中存在的问题,下次再详谈,一眨眼又11点多了,睡大觉.
