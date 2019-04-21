---
author: whidy
comments: true
date: 2012-12-10 06:29:19+00:00
template: post
draft: false
link: http://www.whidy.net/jq-more-demo.html
slug: /jq-more-demo
title: 利用jQuery点击显示更多元素演示代码
wordpress_id: 1431
category: '开发'
tags:
- 技术
---

上次说了一个**[phpcms单页面模板不能用翻页](http://www.whidy.net/phpcms-page-solution.html)**的问题.之后居然发现全系列IE不兼容.之后,一块一块进行排查找出来了.还做了个小demo,这里为了让大家看得更加清楚.我将这个demo分享出来,当然目前情况下来看,IE6,IE7是无法兼容的.代码效果如下:

<del>http://jsfiddle.net/kingterrors/VXQ9d/embedded/result,html,css/</del>

<!-- more -->

这个可以直接看效果,将代码整合之后的样子是这样的.


    
    ```html
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Read more list by Whidy</title>
    <script src="http://code.jquery.com/jquery-latest.js"></script>
    <style>
    body {color:#444;}
    ul {list-style:none;}
    .more {font-size: 80%; color:#888;}
    </style>
    </head>
    <body>
    <ul class="list">
      <li>hello? I wanna see you :D</li>
      <li>...</li>
      <li>zzz</li>
      <div class="more">Click here to see whidy smile</div>
      <li>-</li>
      <li>you are not here!</li>
      <li>:(</li>
      <li>zzz</li>
      <div class="more">Ooops, ToT, find it again.</div>
      <li>-</li>
      <li>I gotcha you, whidy.</li>
      <li>Hei!</li>
      <li><img src="http://www.whidy.net/wp-includes/images/smilies/icon_mrgreen.gif" /></li>
      <li>a simple demo ended by <b>whidy</b>.z</li>
      <div class="more">haha</div>
    </ul>
    <script>
    $(".list li").eq(2).nextAll("li").hide();
    $(".list li").eq(3).nextAll("div").hide();
    $(".more").click(function () {
    $(this).slideUp("slow");
    $(this).nextUntil(".more").next().fadeIn();
    $(".more:last").hide(); // for a php loop :) 
    });
    </script>
    </body>
    </html>
    ```



最后还有一件诡异的事情,我新建了两个同样的html文件,一个有效果一个没效果,有兴趣的看看咋回事呢?

有效果的: [https://www.whidy.net/wp-content/uploads/2012/12/jq-more-demo-on.html](https://www.whidy.net/wp-content/uploads/2012/12/jq-more-demo-on.html)
没效果的: [https://www.whidy.net/wp-content/uploads/2012/12/jq-more-demo-off.html](https://www.whidy.net/wp-content/uploads/2012/12/jq-more-demo-off.html)
