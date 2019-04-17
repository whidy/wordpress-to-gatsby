---
author: whidy
comments: true
date: 2014-03-05 14:57:49+00:00
layout: post
link: http://www.whidy.net/multi-rows-vertical-align-middle-with-float-parent.html
slug: multi-rows-vertical-align-middle-with-float-parent
title: 父级带有浮动的多行文字垂直居中
wordpress_id: 1869
categories:
- CSS
- HTML
- IT技术
- 技术分享
tags:
- 技术
- 网站
---

这几天在公司做专题,熟悉公司的一些工作内容,遇到了个问题,如图:

[caption id="attachment_1872" align="aligncenter" width="400"][![高亮为需要做的效果部分](http://www.whidy.net/wp-content/uploads/2014/03/vaM-400x104.jpg)](http://www.whidy.net/wp-content/uploads/2014/03/vaM.jpg) 高亮为需要做的效果部分[/caption]

这里面有四个小方框,其中两个是图,两外两个蓝色背景的则是由不同行数的文字垂直居中,那么怎么做呢?今天可是想了很久,,,查了很多资料,现在也整理不出来,我这个东拼西凑的测试代码是哪里弄来的,反正估计网上是找不到的了...

这个东西暂且叫做"关于多个父级带有浮动的DIV层内文字垂直居中"问题吧.

如果多个块级元素分别包含不同内容,而内容在里面需要水平居中,最重要的是这几个块级元素还要是能够在一行显示,怎么办?

<!-- more -->

先看下面这个例子:

<del>http://jsfiddle.net/kingterrors/f2xC3/embedded/result,html,css/light</del>

PS:由于近日(2014年6月)jsfiddle无法正常访问,可能受内网影响,现将之前所有jsfiddle预览去除,不过你仍然可将以上地址拷贝到浏览器预览,或选择尝试以下代码:


    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>multi rows vertical align middle with float parent</title>
    <style type="text/css">
    * {
        margin: 0;
        padding: 0;
    }
    .outer {
        background:#eee;
        height: 175px;
        width: 275px;
        position: relative;
        display: table-cell;
        vertical-align: middle;
        padding: 5px;
        border: 1px solid #ccc;
    }
    .inner {
        position:static;
        *position:absolute;
        top: 50%;
        width:100%;
        float:left;
    }
    p {
        background:#fff;
        position: relative;
        top: -50%;
        padding:10px;
        color: #222;
        font-size: 18px;
    }
    </style>
    </head>
    <body>
    <div class="outer">
        <div class="inner">
            <p>第一行文字
                <br/>第二行文字
                <br/>第三行文字
                <br/>
            </p>
        </div>
    </div>
    <div class="outer">
        <div class="inner">
            <p>第一行文字</p>
        </div>
    </div>
    </body>
    </html>
    ```



就目前来说是基本上都兼容的,我这里主要考虑居中问题不考虑水平位移,需要调整的自行优化.

但是有时候多个父级浮动之间又需要有间隙,我想来想去结果才用了下面这个又套了一层的方法,不知道还有没有更好的办法了.虽然有效但是感觉整个结构都很复杂了,总觉不够理想,这里直接放出效果:

<del>http://jsfiddle.net/kingterrors/Suamp/embedded/result,html,css/light</del>

PS:由于近日(2014年6月)jsfiddle无法正常访问,可能受内网影响,现将之前所有jsfiddle预览去除,不过你仍然可将以上地址拷贝到浏览器预览,或选择尝试以下代码:


    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>multi rows vertical align middle with float parent</title>
    <style type="text/css">
    * {
        margin: 0;
        padding: 0;
    }
    .multiBox {
        float: left;
        margin-right: 10px;
    }
    .outer {
        background:#eee;
        height: 175px;
        width: 275px;
        position: relative;
        display: table-cell;
        vertical-align: middle;
        padding: 5px;
        border: 1px solid #ccc;
    }
    .inner {
        position:static;
        *position:absolute;
        top: 50%;
        width:100%;
        float:left;
    }
    p {
        background:#fff;
        position: relative;
        top: -50%;
        padding:10px;
        color: #222;
        font-size: 18px;
    }
    .clearfix:after {
        content:".";
        display: block;
        height: 0;
        clear: both;
        visibility: hidden;
    }
    </style>
    </head>
    <body>
    <div class="multiBox">
        <div class="outer clearfix">
            <div class="inner">
                <p>第一行文字
                    <br/>第二行文字
                    <br/>第三行文字
                    <br/>
                </p>
            </div>
        </div>
    </div>
    <div class="outer">
        <div class="inner">
            <p>第一行文字</p>
        </div>
    </div>
    </body>
    </html>
    ```



大概就是这样,总之兼容性好像基本没问题,关键是有个定位是**static**!!!请注意!

有空再研究下...
