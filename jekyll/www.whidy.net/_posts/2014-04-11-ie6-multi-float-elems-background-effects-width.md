---
author: whidy
comments: true
date: 2014-04-11 13:16:29+00:00
layout: post
link: http://www.whidy.net/ie6-multi-float-elems-background-effects-width.html
slug: ie6-multi-float-elems-background-effects-width
title: 关于IE6行内多个元素浮动背景图对宽度影响
wordpress_id: 1914
categories:
- CSS
- HTML
- IT技术
- 技术分享
tags:
- 技术
- 教程
---

遇到这个问题实在是诡异.我对我自己能找出问题的原因也颇感惊讶,因为我根本不知道为什么会出现这样的现象,只是一个个凭感觉试出来的.如果有大神知道原因,希望能留言,如果不知道的正巧看到这篇文章,也可做个参考,解决一些可能是由于背景图产生的问题.惯例先上效对比果图(这里注释了背景).

[caption id="attachment_1919" align="aligncenter" width="400"][![关于IE6行内多个元素浮动背景图对宽度影响CHROME和IE6对比](http://www.whidy.net/wp-content/uploads/2014/04/ie6-bg-effects-width-400x310.png)](http://www.whidy.net/wp-content/uploads/2014/04/ie6-bg-effects-width.png) 关于IE6行内多个元素浮动背景图对宽度影响CHROME和IE6对比[/caption]

按照正常思路完成布局和代码编写后,基本上ie7+和主流标准浏览器看起来都不错.然而IE6,就是令人蛋疼.是怎么蛋疼了呢仔细看图,我放代码和[DEMO页面](http://www.whidy.net/demos/ie6BgEffectsWidth/ie6-bg-effects-width.html)(此页面兼容):

<!-- more -->

    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>关于IE6行内多个元素浮动背景图对宽度影响</title>
    <style type="text/css">
    * {margin:0;padding:0;}
    body {font:normal normal 14px/28px 'Microsoft YaHei';}
    a {text-decoration: none;color: #888;}
    a:hover {text-decoration: none;color: #222;}
    .box {width:215px;margin:20px auto;}
    .box-hd {padding-bottom:10px; border-bottom:1px solid #acacac;font-size:20px; line-height:45px;}
    .box-bd {width:215px;border-top:1px solid #c7c7c7;}
    .txts {width:193px;height:200px;padding:0 10px;border:1px solid #dcdcdc;}
    .box-hd-icon {width:45px;height:45px;display:inline-block;background-image:url(sprite.png); background-repeat:no-repeat;vertical-align:middle;}
    .box-hd em {margin-left:10px;color:#4a4a4a;font-style:normal;}
    .box-hd strong {margin-left:3px;font-family:Arial;font-size:18px;font-weight:normal; color:#7e7e7e;}
    .txts li {width:193px;height:20px;padding:10px 0 9px 0;vertical-align:top; border-bottom:1px dashed #d0d0d0;overflow:hidden;zoom:1;}
    .txts li span {height:19px;display:inline-block;float:left;line-height:19px;overflow:hidden;zoom:1;}
    .num {width:19px;height:19px;color:#888;text-align:center;/*background-image:none;*/ /*ie6*/}
    .txts-icon {background:url(sprite.png) no-repeat -65px 0;color:#fff;text-align:center;}
    .txts-tit {width:112px;margin-left:10px;display:block;float:left;font-size:15px;text-align:left;}
    .txts-score {width:35px;margin-right:3px;font-size:12px;color:#696969;text-align:right;}
    .txts .icon-hand {width: 14px;height: 19px;background: url(sprite.png) no-repeat -70px -112px;float:right;opacity:0.4;filter:alpha(opacity=40);}
    .txts .last {border-bottom:none;}
    </style>
    </head>
    <body>
    <div class="box rank">
    	<div class="box-hd"><span class="box-hd-icon"></span><em>诗词</em><strong>TOP</strong></div>
    	<div class="box-bd">
    		<ol class="txts">
    			<li>
    				<span class="num txts-icon">1</span>
    				<span class="txts-tit"><a href="#" target="_blank">小桥流水人家</a></span>
    				<span class="txts-score">1</span>
    				<span class="icon-hand"></span>
    			</li>
    			<li>
    				<span class="num txts-icon">2</span>
    				<span class="txts-tit"><a href="#" target="_blank">古道西风瘦马</a></span>
    				<span class="txts-score">12</span>
    				<span class="icon-hand"></span>
    			</li>
    			<li>
    				<span class="num txts-icon">3</span>
    				<span class="txts-tit"><a href="#" target="_blank">我不记得了</a></span>
    				<span class="txts-score">123</span>
    				<span class="icon-hand"></span>
    			</li>
    			<li>
    				<span class="num">4</span>
    				<span class="txts-tit"><a href="#" target="_blank">DemoByWhidy</a></span>
    				<span class="txts-score">1254</span>
    				<span class="icon-hand"></span>
    			</li>
    			<li class="last">
    				<span class="num">5</span>
    				<span class="txts-tit"><a href="#" target="_blank">这个名称不能长</a></span>
    				<span class="txts-score">12345</span>
    				<span class="icon-hand"></span>
    			</li>
    		</ol>
    	</div>
    </div>
    </body>
    </html>
    ```



大家可以自己注意注释部分,我也不多说了,毕竟我也不清楚原理...不过图上那个小手没有是因为超过高度隐藏了,如果不限制每个li的高度,会发现小手已经下去了.
