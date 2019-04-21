---
author: whidy
comments: true
date: 2015-01-04 13:37:56+00:00
description: 今天要说的是我才发现的一个BUG.关于魅族手机MX2,MX3(其他机型未测试),固件版本均为3.7.3A稳定版原生浏览器,在测试页面的字体大小样式时无效,
template: post
draft: false
link: http://www.whidy.net/mx-browser-font-size-bug.html
slug: /mx-browser-font-size-bug
title: 魅族手机MX2原生浏览器字体大小问题
wordpress_id: 2679
category: '开发'
tags:
- 手机
- 技术
- 网站
---

都知道魅族的手机很坑了,我就不多说了.

今天要说的是我才发现的一个BUG.关于魅族手机MX2,MX3(其他机型未测试),固件版本均为3.7.3A稳定版原生浏览器,在测试页面的字体大小样式时无效,如果你的魅族手机有遇到类似问题,可以试试这个[demo](http://www.whidy.net/demos/mx_font_size_test/fz1.html)测试一下,顺便看下源码:

    
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>meizu mx2 stock browser bug with font size style</title>
    <style type="text/css">
    * {margin:0;padding:0;}
    body * {/*height:150px;*/display: block;}
    </style>
    </head>
    <body>
        <h1 style="font-size:60px;">h1 tag with a font-size 60px style!</h1>
        <p style="font-size:60px;">p tag with a font-size 60px style!</p>
        <span style="font-size:60px;">span tag with a font-size 60px style!</span>
        <strong style="font-size:60px;">strong tag with a font-size 60px style!</strong>
        <a href="#" style="font-size:60px;">a tag with a font-size 60px style!</a>
    </body>
    </html>
    ```


从这个代码中可以看出,所有元素应该都是60px字体大小.

但是又可以发现a标签的字体大小是比以上字体大,实际上a才是60px大小,而其他元素的字体大小则是一个默认值.为什么会这样,请问魅族开发人员!

我发现了一个现象,上面把高度给注释去掉了,也就是"hack"后,则字体大小显示正常,均保持了60px,见[demo2](http://www.whidy.net/demos/mx_font_size_test/fz2.html)...这是什么原因.

鬼才知道!

因此我们一致认为魅族原生浏览器坑爹.我不记得web标准是需要给设定了字体大小的元素加高度的吧...
