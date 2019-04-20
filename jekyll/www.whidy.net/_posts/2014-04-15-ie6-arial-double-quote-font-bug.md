---
author: whidy
comments: true
date: 2014-04-15 12:41:22+00:00
template: post
link: http://www.whidy.net/ie6-arial-double-quote-font-bug.html
slug: /ie6-arial-double-quote-font-bug
title: 一个小小的双引号引发的思考-XP内IE下的字体(下)
wordpress_id: 1916
category: '开发'
tags:
- 技术
- 网站
---

在原版的XP系统下IE 6,IE7,对于自体支持似乎不是特别的好.上次提到过中文字体似乎对于中文标点都不能正常显示出来.更不要提英文字符对汉字的支持了.
正是这个原因上期的背景图解决IE6,7字符替换问题费了很大的功夫.
这次我简要总结一下我所发现的XP下IE6和IE7下字体的一些问题.

其实我之前做网站从未遇到这样的问题,可能是很久以前微软雅黑并未普及吧.就目前来看,网上关于字体的资料太少,国外有却跟汉字毫无关系.我也下了一个可能并不准确的结论:

<!-- more -->

**XP系统下(无微软雅黑等特别的字体)的IE6和IE7是不支持英文字体下的汉字标点符号,甚至连汉字的不同字体下的标点符号都没有区别,统一是两个大逗号的样子,唯独IE8对这些字体略有区别,有所改进(例如IE6和IE8下Arial的中文双引号就不一样),那么我估计IE6,7想用特别的标点符号样式的话还是放弃吧.**

对于上次我做的两个DEMO,我后来思前想后,觉得实在不妥,于是做了一个终极方案,我想恐怕我也再想不出来更好的办法了.这个方案的代码量比较少,hack内容也不多,因为字体是从google font内调用出来的,而找到这样的字体也是花了时间一个个测试的,这样的成本太高.我闲话少说,还是上[demo页面](http://www.whidy.net/demos/quote/quote_text_gg.html)和代码吧:


    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>大双引号文字段自适应DEMO</title>
    <link href='http://fonts.googleapis.com/css?family=Anonymous+Pro:700' rel='stylesheet' type='text/css'>
    <style type="text/css">
    .container {width: 720px;color: #000;padding:20px;background-color: #eee; text-align: left;position: relative;overflow: hidden;zoom:1;}
    .quote {font-family:'Anonymous Pro', SimHei , arial; font-size: 200px;line-height: 200px;height: 100px;overflow: hidden;margin-top: -24px;}
    .q-start {position: relative;display:inline;float: left;}
    .q-end {*margin-top:-30px;position:absolute; }
    .content {margin:40px 0 0 8px;*margin-top:60px;padding-bottom:30px;position: relative;font:bold 24px/40px "Microsoft YaHei", SimHei;text-indent:0;}
    </style>
    </head>
    <body>
        <div class="container">
            <span class="quote q-start">“</span>
    		<p class="content">HTC于北京时间23：00在英国伦敦和美国纽约同步举行发布会，正式发布新旗舰智能手机HTC One (M8)，0界面等几大亮点。HTC One (M8)带来突英国伦敦和美国纽约同步举行发布会，正式发布新旗舰智能手机HTC One (M8)，0界面等几大亮点。HTC One (M8)带来突英国伦敦和美国纽约同步举行发布会，正式发布新旗舰智能手机HTC One (M8)，0界面等几大亮点。HTC One (M8)带来突英国伦敦和美国纽约同步举行发布会，正式发布新旗舰智能手机HTC One (M8)，0界面等几大亮点。HTC One (M8)带来突破性的设计与质量，拥有一体成型的高质感金属外型设计，5.0英寸1080p屏幕，极窄边框以及平滑柔和的圆弧曲线，机身更加圆润和轻薄。<span class="quote q-end">”</span></p>
        </div>
    </body>
    </html>
    ```



希望以后能对字体有更深入的研究,把这些问题说清楚.

PS: 有人说@font-face,其实仔细考虑并不适用,毕竟汉字的字体体积太大.

之前的方法,参考:
[一个小小的双引号引发的思考-XP内IE下的字体(上)](http://www.whidy.net/ie6-arial-double-quote.html)
