---
author: whidy
comments: true
date: 2013-01-23 05:49:52+00:00
layout: post
link: http://www.whidy.net/u880-flash-bin-rom.html
slug: u880-flash-bin-rom
title: U880线刷bin包的正确顺序
wordpress_id: 1556
categories:
- IT技术
- 技术分享
tags:
- 手机
- 技术
---

我的手机不慎掉马桶了.开不了机了,只能暂时用室友的U880了,他刚换荣耀2,碉堡了.

好了不得不说U880线刷其实还是很简单的.关键问题在于驱动,装驱动难倒了一片人,我经过简单的研究测试,将我的经验分享给大家!

我这里测试了两个系统,一个是**XP 32位**,一个**是WIN8 64位**.共遇到过两种问题,一个是**设备已插入,请稍后...**,另一个是,**下载中,请稍后...**.

[caption id="attachment_1557" align="aligncenter" width="400"][![WIN8 64位系统下安装好驱动状态](http://www.whidy.net/wp-content/uploads/2013/01/usbdriver-400x211.jpg)](http://www.whidy.net/wp-content/uploads/2013/01/usbdriver.jpg) WIN8 64位系统下安装好驱动状态[/caption]

<!-- more -->

刷机过程详细的正确顺序:



	
  1. 准备好必要的文件([**驱动和刷机程序下载**](http://sdrv.ms/10GLsYq))和操作环境(上面已经提到两种).

	
  2. 手机正常关机放置一边什么都不要做.

	
  3. 安装那个840K大小的驱动

	
  4. 进入蓝屏刷机模式(开机键+音量+键),插上数据线(切忌此时电池还在手机上!)

	
  5. 提示驱动安装,**XP**按照这个链接操作**[中兴U880线刷全过程图解](http://bbs.hiapk.com/forum.php?mod=viewthread&tid=3210983&extra=page%3D1%26filter%3Dtypeid%26typeid%3D2329&page=1)**或者**[最全面的U880刷机教程(线刷)十分钟搞定](http://wenku.baidu.com/view/d41b742ecfc789eb172dc825.html)**.而**WIN8**则在设备管理器找到感叹号的**TAVORL**,**更新驱动程序**,手动更新,在选择驱动目录的时候,这里可以选择刚才下载的驱动包里面的目录Driver,如果不行也可以选择装驱动程序时候的SP920平台下载驱动\Drivers\64bit目录内自动进行安装.这里也有一篇参考文**章[WIN7以上版本安装U880驱动教程](http://www.shuame.com/faq/manual-tutorial/246--u880.html)**,知道驱动安装完成USB出现可识别设备.

	
  6. 拔掉数据线,取出电池.运行刷机程序,选择BIN文件刷机包.

	
  7. 数据线插上手机,程序开始检测并等待开始刷机

	
  8. 执行刷机等待成功,关闭程序,拔掉数据线.

	
  9. 装上电池,开机(耐心等待)...圆满成功.


可能存在的问题.XP下一般不会出问题,如果有失败,请卸载驱动重新试过.而WIN8上则不好说,昨天晚上我在自己电脑上刷机一切OK,但是今天在办公室电脑刷就出现了前文提到的两个问题.初步怀疑是主板USB接口,或者是系统的问题(我家里的是原版的WIN8).所以,一旦出现这两个问题一般来说只能换一台电脑重新尝试了.还有人说可能是**IMEI号**不同的问题这里不多说,大家自行查找相关文章.

基本上想到的就这么多了.祝大家刷机愉快.我也悲催的暂时用用这个卡卡的手机了.
