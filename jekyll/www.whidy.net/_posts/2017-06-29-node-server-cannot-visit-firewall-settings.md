---
author: whidy
comments: true
date: 2017-06-29 02:23:09+00:00
template: post
draft: false
link: http://www.whidy.net/node-server-cannot-visit-firewall-settings.html
slug: /node-server-cannot-visit-firewall-settings
title: node搭本地服务器局域网内其他设备无法访问的问题
wordpress_id: 2941
category: '开发'
tags:
- 技术
---

最近公司网络调整,本来记得之前手机访问电脑的服务器好端端的,突然就不好使了...

找了公司网络维护来看看,一时也没看出来.不过测了一下其他人的电脑搭建的服务器是可以访问的.于是推测是本机问题...可是一直没有对本机的网络有修改调整,怎么就突然不行了.只好自己动手查问题.

初步推测防火墙设置.简单暴力的办法关闭防火墙.果然通了...但是个人不喜欢关防火墙,感觉不安全了哈哈哈,其实是觉得小题大做,应该从根本解决问题.

回忆之前本地maven服务器,wamp搭建的服务器都好好的.大概是幻觉,也就是node搭建的服务器我或许没测过.好吧废话少说.不能访问的地址是192.168.1.107:9000,我就查一下什么程序用9000窗口,如下:

![占用9000端口的是node.exe](https://www.whidy.net/wp-content/uploads/2017/06/node-400x252.png)

防火墙状态写了不允许,我猜大概就是这里了.

回到防火墙设置,在允许的应用中,我发现,**专用网络**的勾没有勾上(如下图),估计问题就在这里,于是勾上,确认后,BINGO...

![防火墙node设置规则](https://www.whidy.net/wp-content/uploads/2017/06/firewall-400x289.png)

拿出手机刷新一下,好了~

问题就解决了,问题其实解决起来很简单,不过对于网络这块不是很懂的,也遇到类似问题的可以通过类似的办法处理试试.

(话说出现这样的问题会不会是因为我第一次使用node启动服务器时候,弹出来的防火墙提示我误点了不允许导致的- -)
