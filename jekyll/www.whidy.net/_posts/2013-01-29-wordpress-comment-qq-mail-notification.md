---
author: whidy
comments: true
date: 2013-01-29 07:55:49+00:00
template: post
link: http://www.whidy.net/wordpress-comment-qq-mail-notification.html
slug: /wordpress-comment-qq-mail-notification
title: wordpress评论后QQ邮箱提示再谈
wordpress_id: 1622
category: '开发'
tags:
- wordpress
- 技术
---

这个话题可能大家讨论过很多次了,但是总是会有很多奇怪的原因导致配置失败无法达到效果,或者是之前一直好好的,突然有一天发现,别人在自己博客上的评论就没了邮件提示作者.正巧我就遇到了这个问题.真是有点莫名其妙.

今天我来说说最近发现了这个问题我的解决办法,仅供大家参考.

**效果:** 我的博客一直以来都是**如果有人评论的话会自动发送我邮箱内提示,并且我回复别人的评论,别人也能收到我的回复提示的邮件**.我的邮箱是QQ的域名邮箱whidy@whidy.net,至于如何配置MX记录,大家自行研究,此文重点是**SMTP配置**.

<!-- more -->

**插件:** 一个是**WP SMTP**,另一个是**Comment Reply Notifier**,前者是配置邮件发送服务器的,后者就是提示留言的.

配置: Comment Reply Notifier这个就是安装上就行了,不需要做多余的工作,而这个WP SMTP,我要好好说说.我的配置如图:

![我的WP SMTP配置图](http://www.whidy.net/wp-content/uploads/2013/01/WP-SMTP-400x318.jpg)

之前我用的SMTP加密方式是SSL,端口按照腾讯邮箱里说的端口号465或587是可以的,但是现在好像不行了,我找了相关资料说用端口25.结果测试了一下,好像不是很稳定,有时候可以,有时候却是跳转到超时的错误页面了.我决定从各方面测试.测试过程就不多说了,我的测试结果就如图,我把**SMTP端口空着**.然后发现速度很快,而且一切功能都恢复正常了,如果其他朋友也是像我这样的问题,可以参考我的这样试试!~
