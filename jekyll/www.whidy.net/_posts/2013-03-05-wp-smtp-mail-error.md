---
author: whidy
comments: true
date: 2013-03-05 03:12:54+00:00
template: post
link: http://www.whidy.net/wp-smtp-mail-error.html
slug: /wp-smtp-mail-error
title: WP SMTP邮件转发出错解决
wordpress_id: 1636
category: '开发'
tags:
- 技术
- 网站
---

好吧,我的博客经常会出现无法收到评论邮件提醒的问题,也不知道是哪里配置错了.最近又出现了这个情况,检查来检查去也多次进行测试,还是失败,提示错误为"**发生了一些错误**",也不知道什么原因.

后来我又换了个后台经过同样的设置,总算弄好了,其实没有什么设置上的变化,但是为什么一个是好的一个是坏的呢?我没有进行更为详细的测试,不过根据猜测,原因是**因为我在之前WP版本下安装了WP SMTP可以正常,后来更新了WP,导致WP SMTP出现问题**,所以我这次弄好了的方法是:**停用WP SMTP并清除原有设置,重新启用WP SMTP,并进行设置即可**.我的配置如下:

![WP SMTP设置图](http://www.whidy.net/wp-content/uploads/2013/03/WP-SMTP-400x321.jpg)

很遗憾,后来测试发现还是有问题...........当然不排除按照我这个方法解决问题的可能性!

3月13日再次更新:我这样设置又可以用了...我觉得就是QQ SMTP有问题,时好时坏...如下图

![再次设置成功的配置方法](http://www.whidy.net/wp-content/uploads/2013/03/QQ-SMTP-400x346.jpg)


