---
author: whidy
comments: true
date: 2014-04-20 05:34:08+00:00
layout: post
link: http://www.whidy.net/google-web-tool-structured-data-errors.html
slug: google-web-tool-structured-data-errors
title: 谷歌站长工具结构化数据错误提示修正方法
wordpress_id: 1995
categories:
- IT技术
- 技术分享
tags:
- wordpress
- 教程
- 网站
---

我有个习惯,看到哪里报错了,非解决不可,要不然心里惦记着啊,不舒服啊...这最近用**谷歌站长工具**,发现我这个wordpress博客有一大堆问题啊...例如:

[caption id="attachment_1996" align="aligncenter" width="400"][![Structured Data Errors](http://www.whidy.net/wp-content/uploads/2014/04/Structured-Data-Errors-400x312.jpg)](http://www.whidy.net/wp-content/uploads/2014/04/Structured-Data-Errors.jpg) 一大堆结构化数据错误...[/caption]

除了最明显的结构化数据这里有无数个页面错误,好在这里大多可以通过修改模版一次性解决.但是如何解决了,最令我无语的是起初我用的是英文版的谷歌站长工具...看不懂,什么叫做**Structured Data > hatom (markup: microformats.org)**?什么叫做**Missing: updated**? 什么叫做**Missing: author**?搞不懂...看了半天帮助文档,弄了一晚上没搞明白,外加坑爹中国GFW,又不能上google plus...好多服务都限制了.不过功夫不负有心人.我看了无数遍帮助文档,还有Structured Data Testing Tool里面的Examples,以及谷歌的论坛,终于解决了.下面来说一下这两个问题怎么解决了.

<!-- more -->

关于**Missing: author**解决办法:

官方说在HTML内添加:<a href="你的g+地址"?rel="author">Google</a>(可能是这样的,我不记得了...)但是这样做页面就会多出来个google,那么我只好通过删掉内容,放一个空标签进去了.这样似乎可以解决,但是我不喜欢空标签,我看了Examples里面有一个这样写的:

    
    ```html
    <link rel="author" href="https://plus.google.com/107770226485624482093" />
    ```


[caption id="attachment_1997" align="aligncenter" width="400"][![author](http://www.whidy.net/wp-content/uploads/2014/04/author-400x173.jpg)](http://www.whidy.net/wp-content/uploads/2014/04/author.jpg) Missing: author错误提示解决办法图[/caption]

我试了一下,编辑header.php,添加此段引用代码,将href=""内地址换成你自己的.就通过了测试...(对了前提是你要有通过E-mail验证.)

关于`**Missing: updated**`解决办法:

找到主题的function.php这个地方,如图

[caption id="attachment_1998" align="aligncenter" width="400"][![updated](http://www.whidy.net/wp-content/uploads/2014/04/updated-400x282.jpg)](http://www.whidy.net/wp-content/uploads/2014/04/updated.jpg) Missing: updated错误的解决方法图[/caption]

在发布日期这里找到`class="entry-date"`里面添加一个updated就可以了,只是标记作用.

这些小问题,解决起来很容易,可是实际在寻找解决方法的时候可是困难重重,希望能帮助哪些需要解决也没找到如何解决的朋友.直到后来,,,昨天发现原来有中文版的谷歌站长工具,真是费尽我脑汁去翻译,晕死了.

如果有人遇到了相同的问题或者更多关于结构化数据错误,可以去这里[Google Product Forums](https://productforums.google.com/forum/#!forum/en)搜索答案,就不要用baidu了,它什么也不会告诉你的: )

PS:毕竟本文有时效性,不同的主题可能也不一样,无法做到通用,我也只能做到提供一种方案,大家举一反三咯~有些模板也要修改PO和MO的,大家可参考参考[WORDPRESS自定义模板后的PO文本翻译修改以及MO修改教程](http://www.whidy.net/wordpress-po-and-mo-modified-tourist.html)(更新日期:2015-06-05)
