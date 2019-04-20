---
author: whidy
comments: true
date: 2014-04-21 14:49:11+00:00
template: post
link: http://www.whidy.net/sublime-text-sftp-connection-timeout.html
slug: /sublime-text-sftp-connection-timeout
title: sublime text的插件SFTP连接超时
wordpress_id: 2000
category: '开发'
tags:
- sublime text
- wordpress
- 技术
- 教程
- 网站
---

这几天看到关于sublime text的一个连接FTP的插件SFTP,居然能直接修改同步上去.那可是省事多了,以后改内容,直接通过这个修改后上传,也不用FTP工具了.可是省事了,可是在设置正确使用的时候出了点小问题,总是提示连接超时,什么原因呢?

先来说说安装吧,之前很多文章提到了安装插件的过程,这里就不复述了,装好SFTP插件,先要对着需要同步到服务器的目录右键-"**Map to remote...**",接着会弹出一个配置文件,我按照经验简单设置了一下,测试连接,却始终连不上去.于是我又仔细查阅了官方的关于SFTP的官方说明,详见:[Sublime SFTP Settings](http://wbond.net/sublime_packages/sftp/settings),却还是不行,改端口,改密码,改改改...都不行,最后索性试一下这个连接方式改成FTP,效果如何,结果一下就连上了,只知道FTP有主动传输和被动传说,真不知道这个S是用来做啥的,最可恶的是,官方文档说,除特殊情况,请保持默认SFTP...真是服了.

最后上我的配置图:

![SFTP设置图](http://www.whidy.net/wp-content/uploads/2014/04/SFTP-settings-400x342.jpg)

如果嫌每次敲密码麻烦,这里可以输入密码就可以了,至于其他配置,可以根据个人需求来设置.

PS:后来发现这个插件总是报错,兼容性有点问题还是怎么回事,大家自行考虑是否使用(2014年6月19日)
