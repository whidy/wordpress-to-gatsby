---
author: whidy
comments: true
date: 2014-10-31 03:46:49+00:00
layout: post
link: http://www.whidy.net/css3-arrows-summary.html
slug: css3-arrows-summary
title: 通过CSS3制作页面折角箭头的方法总结
wordpress_id: 2611
categories:
- CSS
- HTML
- IT技术
- 技术分享
tags:
- 技术
- 教程
---

最近在做wap方面工作,对html5和css3的相关知识又学习了些许,近期对于这种箭头" > "的CSS3制作方法进行了简单的总结,如果以后有想到其他更好的,也会不间断更新.闲话少说,直接上代码:

    
    <code class="html"><!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>css3 arrow test demo by whidy</title>
    <meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no"/>
    <style type="text/css">
    body {font-family:"Microsoft YaHei";}
    h3 {line-height:2;border-bottom:1px dashed #aaa;}
    .updated-time {font-size:14px;color:#999;}
    i {font-style:normal;}
    div {position:relative;}
    div p {padding-top:50px;}
    .arrow-1::after {-webkit-transform:rotate(45deg);border-color:#666;border-width:1px 1px 0 0;height:8px;left:0px;top:0px;width:8px;border-image:none;border-style:solid;content:" ";position:absolute;}
    .arrow-2 {display:inline-block;position:relative;vertical-align:top;}
    .arrow-2::before,.arrow-2::after {content:"";font-size:0;width:0;height:0;line-height:0;overflow:hidden;display:inline-block;position:absolute;top:0;border:0 dashed transparent;border-left-style:solid;border-width:7px;}
    .arrow-2::before {border-left-color:#666;left:0;}
    .arrow-2::after {border-left-color:#fff;left:-2px;}
    .arrow-3 {-webkit-transform:rotate(45deg);width:12px;height:12px;-webkit-box-shadow:2px -2px 0px -1px #000;background-color:#fff;display:block;}
    .arrow-4 {font-family:-webkit-pictograph;transform:scale(1,2);display:block;}
    .arrow-5 {-webkit-transform:rotate(-90deg) scale(1,0.5);font-family:cursive;font-size:24px;display:inline-block;}
    </style>
    </head>
    <body>
    <h3>这是一个通过CSS3各种方式来测试箭头的DEMO</h3>
    <div>
        <i class="arrow-1"></i>
        <p>通过写上边框和右边框形成的角度进行旋转,代码简单</p>
    </div>
    
    <div>
        <i class="arrow-2"></i>
        <p>通过两个三角形叠加形成一个箭头,代码较多,需考虑背景色</p>
    </div>
    
    <div>
        <i class="arrow-3"></i>
        <p>通过旋转一个白色正方形,并给他阴影产生的效果(似乎android 2.x不支持模糊距离为0的情况.所以虽然效果也不错,不过依情况适用)</p>
    </div>
    
    <div>
        <i class="arrow-4"> > </i>
        <p>通过字体设置为<em>-webkit-pictograph</em>并进行缩放产生的效果,兼容性较差</p>
    </div>
    
    <div>
        <i class="arrow-5">V</i>
        <p><del>这个实际上也是通过字体(cursive)控制,字母V通过旋转和变形,我觉得可能不好用,适合卡通版箭头吧...</del>(有的移动端没这个字体或浏览器支持不好,PC端兼容性较差 2014年10月22日)</p>
    </div>
    
    <p class="notes">参考网站:<strong>http://www.w3cplus.com/content/css3-transform</strong></p>
    <p class="updated-time">更新日期:2014年10月31日</p>
    </body>
    </html></code>
    


上面也对各种制作方法进行了简单说明,大家也可以打开查看[DEMO页面](http://www.whidy.net/demos/css3_arrows.html)
