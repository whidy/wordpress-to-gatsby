---
author: whidy
comments: true
date: 2012-07-15 11:19:47+00:00
layout: post
link: http://www.whidy.net/how-to-remove-margins-for-first-last-elements.html
slug: how-to-remove-margins-for-first-last-elements
title: 如何为第一个或最后一个元素甚至是某类规律元素添加样式?
wordpress_id: 891
categories:
- CSS
- IT技术
- 原创翻译
- 技术分享
- 精彩分享
tags:
- 技术
- 网站
---

有时候,我们在写DIV+CSS的时候,在某一类相同的元素内想给其中的第一个元素或者最后一个元素,甚至是其中某些特定的有规则的排列的元素添加特别的CSS样式,我们该如何下手?下面我将给大家将就一些在CSS中十分实用的方法.

首先,你可以手动使用下面这段代码来应用修改某个元素的效果(当然这个办法很笨,是个人都知道):

<del>http://jsfiddle.net/kingterrors/szCM9/embedded/result,html,css/</del>

PS:由于近日(2014年6月)jsfiddle无法正常访问,可能受内网影响,现将之前所有jsfiddle预览去除,不过你仍然可将以上地址拷贝到浏览器预览,或选择尝试以下代码:


    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>how to remove margins for first last elements</title>
    <style type="text/css">
    ul {
        border: 1px solid #000;
        margin: 0;
        padding: 0;
        list-style: none;
        float:left;
    }
    ul li {
        background:#eee;
        color: #F00;
        margin: 50px;
    }
    .first {
        color: #000;
        margin-top: 0 !important;
        margin-left: 0 !important;
    }
    .last {
        color: #0f0;
        margin-bottom: 0 !important;
        margin-right: 0 !important;
    }
    </style>
    </head>
    <body>
    <ul>
      <li class="first">Hello, This is first element</li>
      <li>WOW, so many elements</li>
      <li>WOW, so many elements</li>
      <li>WOW, so many elements</li>
      <li class="last">Here it is, The last element</li>
    </ul>
    </body>
    </html>
    ```



当然你也可以利用:first-child伪类和:last-child伪类(当然这种效果IE6完全不支持,IE7,IE8部分支持,其中IE7和IE8效果相同,不支持:last-child),比如:

<del>http://jsfiddle.net/kingterrors/44GzJ/embedded/result,html,css/</del>

PS:由于近日(2014年6月)jsfiddle无法正常访问,可能受内网影响,现将之前所有jsfiddle预览去除,不过你仍然可将以上地址拷贝到浏览器预览,或选择尝试以下代码:


    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>how to remove margins for first last elements</title>
    <style type="text/css">
    ul {
        border: 1px solid #000;
        margin: 0;
        padding: 0;
        list-style: none;
        float:left;
    }
    ul li {
        background:#eee;
        color: #F00;
        margin: 50px;
    }
    ul li:first-child {
        color: #000;
        margin-top: 0 !important;
        margin-left: 0 !important;
    }
    ul li:last-child {
        color: #0f0;
        margin-bottom: 0 !important;
        margin-right: 0 !important;
    }
    </style>
    </head>
    <body>
    <ul>
      <li>Hello, This is first element</li>
      <li>Whidy! so many elements</li>
      <li>Whidy! so many elements</li>
      <li>Whidy! so many elements</li>
      <li>Here it is, The last element</li>
    </ul>
    </body>
    </html>
    ```



[caption id="attachment_892" align="aligncenter" width="400"][![](/wp-content/uploads/2012/07/E2-400x285.jpg)](/wp-content/uploads/2012/07/E2.jpg) IE6,IE7,IE8都不能完好支持first-child和last-child伪类[/caption]

其中还有种很另类的方式,给任意元素的规则性的添加伪类.比如你有5个li元素,你想让每两个li有区别,比如应用在有些特殊列表,你给每两行加上不同的背景色,我这里随便做了个效果给大家参考:

<del>http://jsfiddle.net/kingterrors/76jxP/embedded/result,html,css/</del>

PS:由于近日(2014年6月)jsfiddle无法正常访问,可能受内网影响,现将之前所有jsfiddle预览去除,不过你仍然可将以上地址拷贝到浏览器预览,或选择尝试以下代码:


    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>how to remove margins for first last elements</title>
    <style type="text/css">
    ul {
        border: 1px solid #000;
        margin: 0;
        padding: 0;
        list-style: none;
        float:left;
    }
    ul li {
        background:#eee;
        color: #F00;
        margin: 50px;
    }
    ul li:nth-child(2n) {
        color: #000;
        margin-top: 0 !important;
        margin-left: 0 !important;
    }
    </style>
    </head>
    <body>
    <ul>
      <li>Hello, This is first element</li>
      <li>Whidy! so many elements</li>
      <li>Whidy! so many elements</li>
      <li>Whidy! so many elements</li>
      <li>Here it is, The last element</li>
    </ul>
    </body>
    </html>
    ```



当然这个在IE8以下包括IE8的版本都是不被支持的 8O !

最后总结一下:first-child和:last-child伪类在IE6下是完全不支持的,而IE7和IE8仅支持:first-child,IE9是完全支持的.而:nth-child只有IE9支持,其他的比如Safari 3+, Firefox 3.5+ and Chrome 1+是完全支持以上效果的.

另外,你也可以用jq来控制某个任意元素的样式,之前我也提到过,有兴趣可以看看[列表中最后一个元素样式清除修改方法](/lastchild-styles-clean.html) :roll:

如果有兴趣可以参考下原文,[Remove Margins for First/Last Elements](http://css-tricks.com/snippets/css/remove-margins-first-element/)
