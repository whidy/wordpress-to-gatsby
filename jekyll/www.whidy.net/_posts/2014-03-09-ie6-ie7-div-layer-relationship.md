---
author: whidy
comments: true
date: 2014-03-09 14:40:00+00:00
layout: post
link: http://www.whidy.net/ie6-ie7-div-layer-relationship.html
slug: ie6-ie7-div-layer-relationship
title: ie6,7下相邻div叠加层级关系问题
wordpress_id: 1878
categories:
- CSS
- HTML
- IT技术
- 技术分享
tags:
- 技术
- 网站
---

在解决一个看似很简单的效果的时候,我想尽量用简单的代码做,效果如图:




![带有小箭头的文本框](http://www.whidy.net/wp-content/uploads/2014/03/arrowBorder.jpg)




我这里实际上只用了一个"<"这样的小图,这个小图则是放在一个左浮动的div,当然这个图是div通过背景图显示出来的,而右边则是一个border为1的div,那么我需要小图向右移动一个px,来遮住这个div的边框.或者带有边框的div向左边距为**小图div宽度减去1px**.如果大家看不懂我描述的,可以自己想想,,那么本身这个效果应该不难,但是我发现IE6,7的兼容性问题,导致不好弄了.首先z-index似乎在这里是无效的.那么我多次测试做了个样本大家可参考一下(由于加载速度较慢请打开查看: )




<!-- more -->




<del>http://jsfiddle.net/kingterrors/LV9Fg/embedded/result,html,css/light</del>




PS:由于近日(2014年6月)jsfiddle无法正常访问,可能受内网影响,现将之前所有jsfiddle预览去除,不过你仍然可将以上地址拷贝到浏览器预览,或选择尝试以下代码:



    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>ie6 ie7 div layer relationship</title>
    <style type="text/css">
    body {padding: 100px;font-size: 14px;}
    div {width:100px;height: 100px;}
    .div1 {background:#ccc;border: 1px solid #aaa;float: left;margin-right: -50px;position: relative;}
    .div2 {border: 1px solid #000;background:#eee;}
    .div3 {background:#ccc;border: 1px solid #aaa;float: left;}
    .div4 {border: 1px solid #000;background:#eee;margin-left: 50px;}
    </style>
    </head>
    <body>
    <div class="div1">我要这个覆盖住右边这个</div>
    <div class="div2"></div>
    <p>IE6,7有效达到效果,chrome杯具</p>
    <div style="clear:both;"></div>
    <div class="div3"></div>
    <div class="div4"></div>
    <p>而IE8+,CHROME正常,其他杯具- -!</p>
    </body>
    </html>
    ```




这里简单说明一下,在做IE6,7兼容性问题时,一定需要在上层的div时要加position:relative;的,而且仔细看都知道,这个似乎必须用两种不同的定位方式解决覆盖问题.暂时写到这里,以后有什么更好的方案再更新.



