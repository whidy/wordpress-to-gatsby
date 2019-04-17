---
author: whidy
comments: true
date: 2014-06-05 13:53:08+00:00
layout: post
link: http://www.whidy.net/google-disconnected.html
slug: google-disconnected
title: wordpress默认主题引用google fonts导致访问速度过慢解决
wordpress_id: 2411
categories:
- IT技术
- 技术分享
tags:
- wordpress
- 技术
- 网站
---

这几天博客访问量下降,虽然本来每天就不多,这下可好,发现网站直接打不开,明白的人,都知道谷歌的服务器受影响了,所以博客就打不开了,估计很多wordpress中枪,临时解决方案就是将那些引用自谷歌服务器的文件取消,可是如何才能取消呢,小弟无才,自己未能解决,最终从网上找到两篇**,一篇是cnblogs上的**,写的好像很不错,不过没试成功,另一篇,更离谱,**修改functions.php的一段代码**,我却都没找到,也不知道是什么版本的.

最终还是用了插件,总算舒服了些,其实我不太喜欢给wordpress安装一大堆插件,等过几日有时间再来研究一下这个或许跟调用twentytwelve_get_font_url有关的函数吧.

有需要的可以安装此插件,插件名称: **Disable Google Fonts**

安装后启用即可,生在中国,要么忍要么...算了不想说了.还是乐观点吧.
