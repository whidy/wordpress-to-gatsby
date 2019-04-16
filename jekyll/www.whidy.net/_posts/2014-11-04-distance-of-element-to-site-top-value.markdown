---
author: whidy
comments: true
date: 2014-11-04 03:59:08+00:00
excerpt: 前阵子做一个项目,做到了一个效果,关于一个导航条跟随屏幕滚动保持在页面顶端的效果,其中有一部分js需要计算导航条距离网页顶部值,当时想不出好的解决方案,根据特定的页面结构写了个不是很好的方法,然而不能适应各种情况,因此今天就研究了一下.
layout: post
link: http://www.whidy.net/distance-of-element-to-site-top-value.html
slug: distance-of-element-to-site-top-value
title: 元素到网页顶部距离计算方法
wordpress_id: 2618
categories:
- HTML
- IT技术
- Javascript
- 技术分享
tags:
- 技术
- 教程
---

前阵子做一个项目,做到了一个效果,关于一个导航条跟随屏幕滚动保持在页面顶端的效果,其中有一部分js需要计算导航条距离网页顶部值,当时想不出好的解决方案,根据特定的页面结构写了个不是很好的方法,然而不能适应各种情况,因此今天就研究了一下.

先来看看这个来着作者lisatisfy的方法:

    
    <code class="js">function getAbsPoint(e) {
        //再封装个函数吧。传进来的e可以是字符串类型（即id）,也可以是htmlElement对象。觉得getEL是个累赘的话，就把它删除掉。
        e = getEL(e);
        var x = e.offsetLeft;
        var y = e.offsetTop;
        while (e = e.offsetParent) {
        x += e.offsetLeft;
        y += e.offsetTop;
        }
        return {
        "x": x,
        "y": y
        };
    }
    //使用getEL，不用$，避免冲突。
    function getEL(id) {
        if (typeif == "undefined") {
        return null;
        }
        if (typeof id == "string") {
        return document.getElementById(id);
        }
        return id;
    }
    </code>


这个的确不错,但是有一些缺陷.我也给作者留言了.并指出了可能出现的问题(当父级多个为相对定位时计算会出现问题,,,以及元素本身的边框值无法计算进去).不过思路是很好的,通过计算与父级层的距离不断计算叠加高度获取最终值.我的表达可能不够清晰,建议自己用这个js写个demo测试.

<!-- more -->

基于这个思想,我完善了一个demo,见源码

    
    <code class="html"><html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>the distance to top</title>
        <style type="text/css">
        div {margin:10px 20px;padding:5px;border:3px solid #aaa;position:relative;}
        .para {background-color:#ccc;}
        </style>
    </head>
    <body>
    <div class="outer">
        <div class="outerWrap">
            <div class="header"></div>
            <div class="content">
                <div class="content-inner">
                    <p class="para" id="para">
                        Hello, whidy! 这是一个获取当前元素距离网页顶部高度的计算demo.
                    </p>
                </div>
            </div>
        </div>
    </div>
    <script type="text/javascript">
    para = document.getElementById('para');
    var y = para.offsetTop;
    while (para = para.offsetParent) {
        var oStyle = para.currentStyle? para.currentStyle : window.getComputedStyle(para, null); //currentStyle兼容IE
        var borderTopWidth = parseInt(oStyle.getPropertyValue('border-top-width')); //border-top-width实际上用于被包父级层的边框值计算,因此本demo内header的边框值对此处不影响,取而代之的是直接计入content盒子距离outerWrap的高度
        if(borderTopWidth) { //如果有边框值则加上边框
            y += para.offsetTop + borderTopWidth;
        }
        console.log(y);
    }
    </script>
    </body>
    </html>
    </code>


同时以上代码的**[DEMO测试页](http://www.whidy.net/demos/distanceToTop.html)**,你可以拷贝代码测试删除div的position:relative样式计算值依然相同.

根据我的个人测试,是没有什么问题的,无论父级是否为相对定位或者含有边框都能正常进行计算.当然毕竟还是有很多考虑不够周全的地方(例如更加**特殊或者复杂的结构**下,这里的计算是否依然准确,会不会除了边框之外的样式也会影响到高度计算,兼容性,**执行效率**如何等等),这里是DEMO测试页面如果各位朋友测试中有疑问请留言,多谢!

最后关于这个计算网页中元素距离网页顶端的距离值计算的DEMO制作学习中我还发现了一些其他的问题,例如关于元素距离高度等相关各种值,当然这里主要是offsetTop,关于父级节点获取例如offsetParent和parentNode差异,元素样式值获取等等,这里不一一列举了.等有时间在进行详细研究和学习.

参考资料:

[Javascript 元素到页面左部和顶部的距离](http://blog.csdn.net/lisatisfy/article/details/6565013)

[MDN Window.getComputedStyle()](https://developer.mozilla.org/zh-CN/docs/Web/API/Window.getComputedStyle).

[获取元素CSS值之getComputedStyle方法熟悉](http://www.zhangxinxu.com/wordpress/?p=2378)


