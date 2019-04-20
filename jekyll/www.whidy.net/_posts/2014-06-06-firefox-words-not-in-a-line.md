---
author: whidy
comments: true
date: 2014-06-06 03:10:29+00:00
template: post
link: http://www.whidy.net/firefox-words-not-in-a-line.html
slug: /firefox-words-not-in-a-line
title: 关于火狐的文字换行问题思考
wordpress_id: 2418
category: '开发'
tags:
- 技术
---

遇到这个问题,可以说是巧合吧,由于场景可能过于复杂我也不不方便进行大量测试,我做的CMS模板中,正好有一处读取18个字符长度,而这个长度在中英文和特殊字符混排的时候是多变的,所以并不固定,不过一般情况下我会保守留一个比较宽的宽度,让一行内可以不出意外的容纳下任何混排的标题.

先来看看问题图片:

![关于FF和CHROME在行内文字换行测试(附IE6测试)](https://www.whidy.net/wp-content/uploads/2014/06/ff_chrome-400x286.png)

事实上,并不顺利~我将其代码片段弄下来做了个demo,大家测试一下(说明:chrome版本34, firefox版本29,IE6可以尝试测试word-wrap:break-word;同时对其进行hasLayout测试观察变化).


    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    	<title>关于FF和CHROME在行内文字换行测试(附IE6测试)</title>
    </head>
    <style type="text/css">
    .width-346px {width: 346px;}
    .font-style {font:bold 18px/2 "Microsoft YaHei";/*word-wrap:break-word;overflow:hidden; zoom: 1;*/}
    </style>
    <body>
    <h1>这是关于火狐和谷歌浏览器的区别测试</h1>
    <div class="width-346px">
    	<a href="#" class="font-style">Intel打响反击战 Computex2014平板综述</a>
    	<span class="font-style">Intel打响反击战 Computex2014平板综述</span>
    	<p class="font-style">Intel打响反击战 Computex2014平板综述</p>
    </div>
    </body>
    </html>
    ```



虽然我写了三行不同标签,相同样式的文字,其实**跟标签名没什么关系**了,有人可能会怀疑我没有做css reset,这点可以排除我为了减少代码量就没有写,实际上**写上CSS RESET一样在火狐下会换行**,我尝试**使用word-wrap:break-word;等属性也是无效**的.因此,这个火狐浏览器对于此处换行的解释我也无从得知,但是可以肯定一点,虽然外层我限制了width-346px,实际上从火狐的开发者工具上来看,内部三行内容的真实宽度也依然是346px,因此并**不是内部内容宽度大于父级导致换行**!原因不明!

最后,没有办法,只好给父级加宽了1px,火狐就显得正常了...若有人有兴趣看到此问题,望共同讨论研究下ff的兼容性问题.



* * *



2014年6月16日15:03:25

在Bob的提醒下,的确是这个问题,加一个**white-space:nowrap;**即可,不过你属性名敲掉了个字母哦~最后献上解决方案:


    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>关于FF和CHROME在行内文字换行测试(附IE6测试)-解决!</title>
    </head>
    <style type="text/css">
    .width-346px {width: 346px;}
    .font-style {font:bold 18px/2 "Microsoft YaHei";white-space:nowrap;}
    </style>
    <body>
    <h1>这是关于火狐和谷歌浏览器的区别测试</h1>
    <div class="width-346px">
        <a href="#" class="font-style">Intel打响反击战 Computex2014平板综述</a>
        <span class="font-style">Intel打响反击战 Computex2014平板综述</span>
        <p class="font-style">Intel打响反击战 Computex2014平板综述</p>
    </div>
    </body>
    </html>
    ```



以后遇到莫名其妙的换行问题,可要多多注意.参考来自Bob的[word-break、word-wrap、word-space、white-space对比图](http://bobscript.com/archives/236/)
