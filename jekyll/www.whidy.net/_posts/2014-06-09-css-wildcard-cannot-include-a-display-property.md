---
author: whidy
comments: true
date: 2014-06-09 13:57:18+00:00
template: post
link: http://www.whidy.net/css-wildcard-cannot-include-a-display-property.html
slug: /css-wildcard-cannot-include-a-display-property
title: CSS的通配符*内不能用display属性?
wordpress_id: 2424
category: '开发'
tags:
- 技术
---

本来是想简单的reset一下,并且做测试,希望所有元素都为块级元素,于是**给*加了个display:block属性值结果发现居然就无法正常解析style了**...想去搜一下是怎么回事呢,却找不到,本想多测试几个属性,试试这个通配符是否还有其他属性无法使用,结果也没试出来,就此抛下疑问?难道不能这样写


    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>css * cannot use display property</title>
    </head>
    <style type="text/css">
    * {display: block;border: 1px solid #f00;padding: 10px;margin-bottom: 10px;}
    body {background-color: #fc0;}
    </style>
    <body>
    <p>body with background color but styles come out too! we dont want this happen!</p>
    <span>you can also try it yourself :)</span>
    <img src="#" width="300" height="300" />
    <a href="#">all blocks now?!</a>
    </body>
    </html>
    ```



而,假设这样的话,不同浏览器效果更是离谱,这里以IE6,7,8,CHROME,IE11为例.测试结果如图:

![通配符有了display属性的结果](https://www.whidy.net/wp-content/uploads/2014/06/css_display-400x165.png)

暂不提这个IE6连HTML节点也算进去了(注意滚动条边框),就说这个不同浏览器的效果,也值得研究下了.
