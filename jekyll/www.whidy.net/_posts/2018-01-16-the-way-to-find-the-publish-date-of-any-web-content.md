---
author: whidy
comments: true
date: 2018-01-16 06:17:29+00:00
excerpt: 为什么要搞清楚该网页内容的发布时间呢，有些网站作者的确很不友好，故意隐藏，目的是啥我也不知道。但是我觉得有时候的确很有必要知道正在查阅的内容，尤其是相对重要的内容的时候，他的发布日期对我来说很重要。
layout: post
link: http://www.whidy.net/the-way-to-find-the-publish-date-of-any-web-content.html
slug: the-way-to-find-the-publish-date-of-any-web-content
title: 怎样找到当前页面发布日期的几种方法
wordpress_id: 3078
categories:
- 其它
- 杂谈
tags:
- 技术
- 网站
---

为什么要搞清楚该网页内容的发布时间呢，有些网站作者的确很不友好，故意隐藏，目的是啥我也不知道。但是我觉得有时候的确很有必要知道正在查阅的内容，尤其是相对重要的内容的时候，他的发布日期对我来说很重要。比如，遇到以下情况：



 	
  * 有时候我们看到一些不错的文章或者新闻内容，分享给其他人后却被朋友嘲笑这都是老掉牙的内容了；

 	
  * 还有时，查阅一些生活知识，或者时效性强的内容，比如你要补血，发现菠菜补铁促进生血，或者想多吃菠菜变成大力水手那样。其实现代科学证明没啥鸟用；

 	
  * 再或者查找某些技术资料时，按照技术文章对应的方法实践的过程中发现有差异，或者无效的时候很气愤耽误了大量时间。


因此，我接下来要以知乎的某个文章[有哪些高级笑话只有具备了一定的专业知识才能听懂？](https://www.zhihu.com/question/59598299)（我这里暂时不想去深究为啥知乎不公开提问日期）作为主要示例介绍一下如何能够找到网上的任何页面的发布日期的几种方法了。

<!-- more -->


### 安装谷歌插件Finitimus


这个插件的工作原理，我暂时还不太清楚，官方并没有说明，不过根据我的观察，它获取发布日期的渠道之一，就是利用google搜索的收录（更新）日期来的，如果一篇文章没有明确的发布日期，那将以谷歌收录（更新）为准，相对来说已经算比较准确的了。如下图：

[caption id="attachment_3092" align="aligncenter" width="400"][![](http://www.whidy.net/wp-content/uploads/2018/01/01-400x441.jpg)](http://www.whidy.net/wp-content/uploads/2018/01/01.jpg) 如果页面更新了。也许就不准确了[/caption]

如果没有收录的情况，或许该插件会去分析页面的代码，也就是把我要讲的下一条操作自动化了。


### 页面源代码内查询


一般浏览器都要查看源代码的功能，我想如果你没有的话，或许你也看不懂我接下来要讲的内容，那就略过，当然有兴趣了解的话接着看。

大部分网站查看源码，并搜索publish，date，这样的关键词，找到前面几个基本上就能获得想要的日期了。当然有的也可能不一样，比如知乎的是“dateCreated”，下面还有个“dateModified”（看到这里你或许发现跟第一条说的插件日期相近，我推测谷歌抓取的就是这个数据）

还是以知乎为例，如下图

[caption id="attachment_3093" align="aligncenter" width="400"][![](http://www.whidy.net/wp-content/uploads/2018/01/03-400x153.jpg)](http://www.whidy.net/wp-content/uploads/2018/01/03.jpg) 通过页面源码查询日期[/caption]


### 分析页面链接和已存在的评论


如果上面的方法都不适合你，那就只能粗略的查找了，比如还是那篇文章，按时间排序后，页面底部找到[最后一页](https://www.zhihu.com/question/59598299/answers/created?page=35)，看到一条[评论](https://www.zhihu.com/question/59598299/answer/166866744)为2017-05-09，那大概这个问题就是2017年5月发布的了，其他的也可举一反三。


### 通过搜索引擎的结果显示


国内百度用的比较多，那么就拿百度说吧，比如百度搜索“有哪些高级笑话只有具备了一定的专业知识才能听懂？”得出的结果，虽然很多相似的，不过就拿前面几个来看，找最有可能的就可以了，如下图：

![百度结果查询日期](http://www.whidy.net/wp-content/uploads/2018/01/02-400x365.png)

还有其他的google利用inurl:来查询，就不说了。


### 总结


其实如果有的时候有些内容真的很重要，又很难查到日期，这些稍显复杂的方法也许就有用了，而有时候似乎显得不那么重要，其实从时间成本上来说，不如就去找别的方法了。

本文也就是抛砖引玉，简单介绍了一下几种查找出网页内容发布日期的方法，希望对各位有所帮助~

参考：[How to Find the Publish Date of Any Web Content](https://techstacker.com/posts/9qCcL6gTx4JbaieEW/how-to-find-the-publish-date-of-any-web-content)
