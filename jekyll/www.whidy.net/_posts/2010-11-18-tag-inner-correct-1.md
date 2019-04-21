---
author: whidy
comments: true
date: 2010-11-18 16:41:10+00:00
template: post
draft: false
link: http://www.whidy.net/tag-inner-correct-1.html
slug: /tag-inner-correct-1
title: js修改标签内内容(上)
wordpress_id: 168
category: '开发'
tags:
- 技术
---

最近几天做页面,跟表单设计制作打交道很多,很多页面的表单格式都很简单,其中,在设计初期,有些效果未添加,而后期需要增加这些效果,于是面对大量的input标签,修改起来也出现了困难,具体情况待我细说.

比如原始的代码大部分格式是这样的:


    
    ```html
    <html>
    <head>
    </head>
    <body>
    <form>
    <input type="text" />
    </form>
    </body>
    </html>
    ```



而,后来有需求说,需要添加一个效果,当光标进入输入框时,会出现比如输入框边框颜色变化,输入框背景颜色变化的效果,当然,如果这仅仅是修改其中这一个输入框的效果,那么方法很多,其中最简单的方法可能可以这样写:


    
    ```html
    <html>
    <head>
    </head>
    <body>
    <form>
    <input type="text" onBlur="this.style.backgroundColor='#ffffff'" onMouseUp="this.style.backgroundColor='#fffab5'" />
    </form>
    </body>
    </html>
    ```



是的,大概就是这样,但是如果有很多页面,有很多input标签,难道一个个这样加,虽然我不是很会js,但是我感觉应该可以直接修改input标签内的内容,更多的是通过获取某个ID,并通过setAttribute()修改某个属性的值,然后事实并不是这样的.也不知道是不是我代码写错了,还是什么的,无论是用setAttribute(属性,值)还是setAttribute(属性,函数),效果都无法实现,当然,这里是为了测试才使用ID的,既然无法实现,则采取另外一个思路,直接通过getElementsByTagName()方法,对于这个方法,可以方便的修改所有input标签的属性,即getElementsByTagName("input"),当然,首先是需要遍历当前页面的所有input标签,然后一个个进行修改,之前,我试了很多次,可能是由于代码规范问题,因为我还没有系统的学习js,或者可能是种种原因,弄了一晚上没弄好,最后还Anfy同学的帮助下,解决了这个问题,由于时间关系,今天暂时写这些,明天把这个简单的小例子写出来,分析,同时也是为了方便以后查阅,举一反三!
