---
author: whidy
comments: true
date: 2012-05-14 14:21:59+00:00
template: post
link: http://www.whidy.net/css-font-size.html
slug: /css-font-size
title: 默认css字体大小单位及样式研究
wordpress_id: 748
category: '开发'
tags:
- 技术
---

我们在给网页字体进行CSS定义的时候,以前通常是使用像素来进行定义,然而,这已经是很古老的方式了,在现如今手机,平板,笔记本等各种不同分辨率设备普及的情况下,我们不只是用电脑浏览网页了,更多的时候或许已经是手持设备了,那么,就将面临一个问题,如何在如此多的不同分辨率下的设备将页面正常展现出来呢?

今天我们暂且不提框架自适应的问题,流体布局以后我熟练掌握后与大家分享,呵呵,就拿这个在定义字体大小方面来进行讨论,用px呢还是em,或是%?

首先需要声明的是在中文网站中,大部分规范是使用12px的汉字作为内容,14px加粗作为标题,当然有些h1,h2或许更大,一般字体用为黑体,而小标题和内容部分字体一般情况下是使用宋体的,这是中文站的一般标准.虽然近两年,随着显示器的不断变大,分辨率的增加,很多网站开始把14px当作最小字体了.然而,可能在很多情况下并不合适,例如手机访问,是不是字太大了等等一系列问题,那么有人可能会说通过终端判断返回不同的CSS,那么这种处理方式较为繁杂.怎么解决页面字体大小就成了一个需要思考的问题.

其实,如果经常访问英文网站的朋友应该不难发现一个特点,他们页面的字体都是用的em作为单位,比如:


    
    ```css
    body { font: normal 100% Helvetica, Arial, sans-serif; } /* 字体大小是页面默认大小的100%,即16像素. */
    h1 { font-size: 1.5em; } /* h1的大小是默认大小的1.5倍,即24像素(24/16=1.5). */
    small { font-size: 0.875em; } /*  small元素的大小是默认大小的0.875倍,即14像素(14/16=0.875). */
    ```



上面是个简单的CSS说明,在实际应用中,也是如此,给body内的font属性进行修改,就可以直接给整个页面字体大小进行缩放,这是一件十分方便的事情.以下我在做个简单的例子给大家直接预览.
先是body内100%时的效果:

<del>http://jsfiddle.net/kingterrors/DEKSy/embedded/result,html,css/</del>

PS:由于近日(2014年6月)jsfiddle无法正常访问,可能受内网影响,现将之前所有jsfiddle预览去除,不过你仍然可将以上地址拷贝到浏览器预览,或选择尝试以下代码:


    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>Font size research</title>
    <style type="text/css">
    body {font: normal 100% Helvetica, Arial, sans-serif;}
    h1 {font-size: 1.5em;}
    small {font-size: 0.875em;}
    .small {font-size: 14px; /* never changed */}
    </style>
    </head>
    <body>
      <h1>This is a Header1</h1>
      <small>and this is small part</small>
      <p class="small">this is another small part with css style sheet that would never change!</p>
      <p>and how about this?</p>
      <p>This is a reseach by <em>Whidy</em></p>
    </body>
    </html>
    ```



然后是body为87.5%时的效果:

<del>http://jsfiddle.net/kingterrors/K3Qbt/embedded/result,html,css/</del>

PS:由于近日(2014年6月)jsfiddle无法正常访问,可能受内网影响,现将之前所有jsfiddle预览去除,不过你仍然可将以上地址拷贝到浏览器预览,或选择尝试以下代码:


    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>Font size research</title>
    <style type="text/css">
    body {font: normal 87.5% Helvetica, Arial, sans-serif;}
    h1 {font-size: 1.5em;}
    small {font-size: 0.875em;}
    .small {font-size: 14px; /* never changed */}
    </style>
    </head>
    <body>
      <h1>This is a Header1</h1>
      <small>and this is small part</small>
      <p class="small">this is another small part with css style sheet that would never change!</p>
      <p>and how about this?</p>
      <p>This is a reseach by <em>Whidy</em></p>
    </body>
    </html>
    ```



大家可以通过两个例子看出来,不变的永远是用px做单位的元素(好像这句话很弱智...),不过显而易见的是,用em绝对是目前和将来的主流!(其实很多大网站普及很久了...z)



* * *



PS: 实际上在国内这种做法仍然未能很好应用,在wap端方向有部分网站开始使用,不知道国内是由于汉字原因呢还是什么,似乎网页设计字体标准仅仅由曾经的12px升级到14px而已(2014年5月17日)
