---
author: whidy
comments: true
date: 2017-11-10 03:35:09+00:00
excerpt: 罗技G930，配置强大，7.1环绕，还有不错软件驱动支持，使用过程中，也遇到了些一问题，比如，经常无故断开重连，软件电量指示不准，无法作为次要设备不休眠使用等等。
layout: post
link: http://www.whidy.net/logitech-g930-always-disconnect.html
slug: logitech-g930-always-disconnect
title: 罗技G930耳机经常自动断开重连等问题解决方案及使用感受
wordpress_id: 2981
categories:
- 兴趣
- 评测
tags:
- 技术
- 评测
---

一直想买个PC的无线耳机，因为之前买的罗技带麦克风的摄像头，每次打游戏他们都说很吵。。。

正巧（四个月前）碰上亚马逊海外购的活动，买了这款罗技G930，配置描述超级强大，外观超酷炫，7.1环绕，还有强大的软件驱动支持，一心动就拿下了，等了半个月到了迫不及待试试，过程中，也遇到了些一问题，比如，经常无故断开重连，软件电量指示不准，无法作为次要设备不休眠使用等等。就这几个问题我简单聊聊。

**经常无故断开重连**，困扰了我很久，也是严重影响我的使用体验的。每次语音团战，突然听不到了。很闹心，查了大量资料似乎很多人都有这种情况。我总结下可能存在的原因：



 	
  * 无线设备干扰，比如WiFi干扰，蓝牙干扰，设备过多造成影响，有人说把路由信道调整一下，我觉得不太靠谱。我尽可能的关闭了无线设备，似乎未见好转。

 	
  * USB供电不足导致蓝牙接收器信号不稳定，我前面后面都插了似乎没见过什么改善。

 	
  * 驱动版本问题，似乎有点效果，也不知道是偶然的，我试过很多个版本的驱动（因为我用了多个罗技设备，其中有个版本的罗技设备管理软件，似乎切到耳机设备就会报错，莫名其妙呢！？）。


我后来有查到是驱动版本问题，我这里使用的是WIN10 64bit，我试了这个版本的驱动似乎好了，https://download01.logitech.com/web/ftp/pub/techsupport/gaming/LGS_8.58.183_x64_Logitech.exe

有兴趣可以尝试，当然安装前请卸载旧的。

参考：[Logitech G930 Disconnect Fix - Windows 10](https://www.youtube.com/watch?v=nA-kvcvZ40M)

<!-- more -->
也可以参考一下官方论坛上的一个帖子：[G930 will not stay connected](https://community.logitech.com/s/question/0D53100006iBRfiCAG/g930)
如果有电流声或者奇怪的噪音可以参考：[NASTY 7.1 AUDIO 100% WORKING FIX / WORKAROUND](http://steamcommunity.com/app/91310/discussions/0/828925216535994327/)

**软件电量指示不准**，说是有9个小时，貌似经常7，8小时就没电了。。。有时候剩余几个小时也不准，这个没办法，没电就插着耳机边充边用了。

**无法作为次要设备不休眠使用**，这个有点蛋疼，因为我还有一对外置音箱，不用耳机输出音频的时候，我会把外置音箱设为主音频设备，但是我还是想用G930的麦克风的，可是这样的话G930大概过15分钟，就会自动关闭，并不会保持开启，我一开始以为是系统的设备自动休眠机制，去改了电源选项，也没有效果。后来查了下，有这样的解决方法，大家可以试试（可能因驱动系统等原因无效）：



 	
  1. 关闭罗技设备管理程序(G图标那个鬼)

 	
  2. 找到C:\Program Files\Logitech Gaming Software\Resources\G930\Manifest folder
（文件夹也有可能是**Manifest**，我的版本是**8.94.108**）

 	
  3. 拷贝Device_Manifest.xml到桌面或其他你有权限修改保存的位置，如果你在当前目录也有写入权限可直接修改保存

 	
  4. 文本编辑器打开这个xml文件，搜索battery附近找到turnOffInterval

 	
  5. 将默认值900修改为0，保存文件（如果拷贝出来修改的请覆盖原路径文件）

 	
  6. 重新启动罗技的软件G


![罗技软件相关信息及设置](http://www.whidy.net/wp-content/uploads/2017/11/Logitech-400x232.jpg)

参考：[Disable auto turn off on G930](https://community.logitech.com/s/question/0D53100006jfuiSCAQ/disable-auto-turn-off-on-g930)

好了，这个耳机总的来说的音质还是可以的。我早就想写评测感受了，放在草稿一直没发布，目前使用了4个月左右了，打打OverWatch什么的效果还行，听歌也还不错，其他各项还算优秀，当然现在最新出来的是G933，如果有钱不妨试试这个，或者其他蓝牙耳机。也许会更好~如果你在使用G930的时候遇到了以上的一些问题，希望这个能给大家带来帮助:-P，对了我的是WIN7 64BIT最新的罗技驱动~
