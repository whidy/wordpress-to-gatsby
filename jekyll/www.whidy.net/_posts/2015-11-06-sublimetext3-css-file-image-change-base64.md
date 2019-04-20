---
author: whidy
comments: true
date: 2015-11-06 08:03:05+00:00
excerpt: 如果在SublimeText3的css文件引用图片里将图片快速转换为base64(Data URL)的方法,以及利用chrome开发者工具获取图片的Data
  Url的方法
template: post
link: http://www.whidy.net/sublimetext3-css-file-image-change-base64.html
slug: /sublimetext3-css-file-image-change-base64
title: SublimeText3的css文件引用图片转base64快速方法
wordpress_id: 2819
category: '开发'
tags:
- sublime text
- 技术
- 教程
---

在你做的css文件中,起初背景图都是直接引用目录的切好的图片.如下:

    
    ```css
    .icons {background-image:url(../images/icon.png);}
    ```


那么在做移动端页面的时候,有时我们需要将小图直接转换成base64格式,一般只能借助第三方工具.
这里其实用sublime text 3 的快捷键**ctrl+'**可以直接快速转换.
当然页面的图片建议是压缩(例如tinypng工具)后的,要不然转换出的字符将会很长.
如果能确定页面的图片都可以直接转换,你可以直接选择 url( 然后快捷键 alt+f3 ,接着按 ctrl+' ,这样一来css的图片就全部转换好了.

另外还有一种通过chrome快速获取网页上图片的Data Url方法.如图

![chrome_ImageToDataUrl](http://www.whidy.net/wp-content/uploads/2015/11/chromeDataUrl-400x165.png)
