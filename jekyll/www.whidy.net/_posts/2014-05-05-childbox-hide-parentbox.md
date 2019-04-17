---
author: whidy
comments: true
date: 2014-05-05 15:04:40+00:00
layout: post
link: http://www.whidy.net/childbox-hide-parentbox.html
slug: childbox-hide-parentbox
title: 子级元素如何覆盖父级元素之边框颜色的遮盖应用
wordpress_id: 2046
categories:
- CSS
- HTML
- IT技术
- 技术分享
tags:
- 技术
---

由于昨天重装系统,很多程序还未正确配置好,这篇暂且长话短说,直接上代码.
关于这个需求在网站制作上还是经常遇到的(例如白色边框覆盖其他边框的障眼法),做到全兼容似乎只有这个方法最好,特分享出来.这里坚决不用z-index,更加不用绝对定位!查看[DEMO](http://whidy.net/demos/childbox-hide-parentbox.html)


    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>childBox and parentBox overlay relationship</title>
    <style type="text/css">
    * {margin:0;padding:0;line-height:1.5;font-family:"Microsoft YaHei";}
    body {background-color:#eee;}
    .container {width:1000px;margin:30px auto;}
    .parentBox {width:300px;height:300px;margin:0 auto; border:50px solid #ccc;*overflow:hidden;}
    .childBox {width:200px;padding:10px;margin:0 auto;height:250px;border:40px solid #aaa;margin-top:20px;position:relative;}
    h3 {font-size:18px;}
    p {font-size:14px;margin:10px 0;}
    .author {text-align:right;}
    </style>
    </head>
    <body>
     <div class="container">
     <div class="parentBox">
     <div class="childBox">
     <h3>childBox and parentBox</h3>
     <p>The childBox overlay the parentBox, otherwise, it must be compatible widt all IEs</p>
     <p class="author">whidy</p>
     </div>
     </div>
     </div>
    </body>
    </html>
    ```



明天重新整理一下,发一点相关页面应用到这个的地方.
