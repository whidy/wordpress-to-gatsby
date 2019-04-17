---
author: whidy
comments: true
date: 2014-04-19 14:33:41+00:00
layout: post
link: http://www.whidy.net/ie6-arial-double-quote-font-solution.html
slug: ie6-arial-double-quote-font-solution
title: 一个小小的双引号引发的思考-XP内IE下的字体(终)
wordpress_id: 1948
categories:
- HTML
- IT技术
- 技术分享
tags:
- 技术
- 网站
---

这是我的终极方案了...其实这个最简单IE6,7的中文双引号,蛋疼!这个方案从代码和易于理解的角度来看是最好的,缺点就是要外部引用两个东东,如果网速不好就杯具了.这次也不多少了,用到一个**伪类选择器**(为了兼容IE6,IE7引入了一个JS文件),用到上次说的外部引用**google font**.那就直接上代码和[DEMO测试页](http://www.whidy.net/demos/quote/quote_text_final.html)


    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>大双引号文字段自适应DEMO</title>
    <!--[if lt IE 8]>
    <script src="http://ie7-js.googlecode.com/svn/version/2.1(beta4)/IE8.js"></script>
    <link href='http://fonts.googleapis.com/css?family=Anonymous+Pro:700' rel='stylesheet' type='text/css'>
    <![endif]-->
    <style type="text/css">
    .container {width: 720px;color: #000;padding:20px;background-color: #eee; text-align: left;position: absolute;top: 200px;left: 220px;}
    .content {margin:40px 0 0 8px;padding-bottom:30px;position: relative;font:bold 24px/40px "Microsoft YaHei";text-indent:0;}
    .content:before, .content:after {font:bold 160px/160px Arial;*font-family:"Anonymous Pro"; height:75px;overflow: hidden;}
    .content:before {content:"“";position: relative;display:inline;margin: -40px 0 0 0;float: left;*top: -5px;
    }
    .content:after {content:"”";position:absolute; margin: -12px 0 0 -15px; *margin: -20px 0 0 5px;}
    </style>
    </head>
    <body>
        <div class="container">
    		<p class="content">HTC于北京时间23：00在英国伦敦和美国纽约同步举行发布会，正式发布新旗舰智能手机HTC One (M8)，0界面等几大亮点。HTC One (M8)带来突破性的设计与质量，拥有一体成型的高质感金属外型设计，5.0英寸1080p屏幕，极窄边框以及平滑柔和的圆弧曲线，机身更加圆润和轻薄。</p>
        </div>
    </body>
    </html>
    ```

之前的几种方法,参考:
[一个小小的双引号引发的思考-XP内IE下的字体(上)](http://www.whidy.net/ie6-arial-double-quote.html)
[一个小小的双引号引发的思考-XP内IE下的字体(下)](http://www.whidy.net/ie6-arial-double-quote-font-bug.html)

话说这个WORDPRESS更新真是快,才更新到3.8.2,这下又出了3.9- -,好在不用改主题...
