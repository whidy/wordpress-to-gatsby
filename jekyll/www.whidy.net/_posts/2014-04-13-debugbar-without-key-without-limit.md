---
author: whidy
comments: true
date: 2014-04-13 12:44:14+00:00
template: post
draft: false
link: http://www.whidy.net/debugbar-without-key-without-limit.html
slug: /debugbar-without-key-without-limit
title: debugbar无需注册码无限使用办法
wordpress_id: 1931
category: '软件'
tags:
- 技术
- 教程
---

直到前几天我才发现我的那个破烂IETESTER的debugbar插件居然不让我免费使用全功能了,限制在于无法查看元素宽高,也无法修改CSS样式来测试了,虽然这些功能都不是很好使,不过IE下勉强就只能用一下这个了.

原来是我使用了一个月就不能使用全部功能了,原来debugbar居然是共享软件...公司要求不允许使用盗版,这可怎么办呢...我突然想到一个办法,尝试了一下,有效,特分享出来,不过要说这个办法的完整步骤,我也不知道.大家可按照下面三个步骤依次测试.准备工作,一款卸载程序和CCleaner就够了.



	
  1. 我电脑装了QQ电脑管家我就用那玩意自带的卸载工具卸了,如果没装的有360可以尝试.QQ电脑管家先会使用原版的卸载程序卸载完debugbar后执行残余清理,当全部完成后,可以尝试再次安装debugbar,看看能否使用全功能...若不行,重新执行此项操作后,进行下一步.

	
  2. 开启CCleaner执行注册表清理.提示备份前,请备份.然后全部修复.完成后,可以尝试再次安装debugbar,看看能否使用全功能...若不行,重新执行第一步和此步,并进行下一步...

	
  3. 其实我估计前面两步就够了,但是我当时是做了最后一步才重新安装debugbar测试的,所以我还是说一下吧.打开注册表编辑器(运行-regedit),搜索debugbar的所有项,并删除...至此尝试再次安装debugbar,这次一定能成功的.


当然为了保险起见,可以尝试完成三步后再安装debugbar..我的测试环境为WIN7 32BIT最新版的IETESTER和最新版的debugbar.现在又可以愉快的调试IE了...



* * *



今天又到期了,于是重新安装,此次试图摸清最佳方式,经过测试,以下方式可能更为快捷.



	
  1. 正常卸载DebugBar插件(无论你用系统自带卸载还是专门的卸载软件)

	
  2. 打开注册表(运行-regedit),<del>找到HKEY_LOCAL_MACHINE\SOFTWARE\Core Services\DebugBar,找到该项(**DebugBar**)</del>,直接删除该项!

	
  3. 重装DebugBar进行测试...


PS: 更新日期2014年6月18日



* * *



以上第二条如果无效请参考该路径

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Core Services\DebugBar

并删除,适用版本DebugBar 7.5.1

PS: 更新日期2015年5月25日
