---
author: whidy
comments: true
date: 2014-04-08 13:15:19+00:00
template: post
link: http://www.whidy.net/xp-ie7-homepage-locked.html
slug: /xp-ie7-homepage-locked
title: XP下IE7浏览器主页总是微软网站无法锁定无法修改!!!
wordpress_id: 1892
category: '开发'
tags:
- 技术
- 教程
---

我一直以为我对XP灯操作系统的各种设置无所不知...虽然已经有6,7年没有使用XP了,想当年读高中时,每天研究注册表,研究优化,看电脑迷杂志,电脑报,网友世界,大众软件...的日子,怀念.

但是,今天我装完虚拟机,升级了XP的ie到7,却发生了一件让我震惊的事情,其实也许是那个我下的盗版XP系统问题= =...事情是这样的,我将默认的IE6升级到IE7后,每次打开IE7,主页都是微软的页面,修改了主页也没用.其实这并不是锁定之类的问题,而是第一次启动ie的问题.我找了半天资料,整理了如下解决方案.



	
  1. 开始-运行-gpedit.msc-用户配置-管理模板-windows components-internet xeplorer ,在它的右边框中找到"阻止执行首次运行自定义设置",并双击它,在打开的新窗口中选择"已启用"项,在选择菜单中有两个选项,在下面的"选择您的选择"框中选择"直接转到主页",关闭IE重新打开尝试.如果不行进行下一步.

	
  2. 开始-运行-regedit-"HKEY_CURRENT_USER\Software\Microsoft\Internet Explorer\Main"右侧Start Page内值改成需要的首页,若还不行,进行下一步.

	
  3. 对上一步main给权限everyone设置完全控制权限,再修改


好的问题解决,如果还有问题请留言!!!

为什么IE6,7,8还不死,中国人死守XP,守吧守吧,追求不同.

参考资料:
* [我用了正版ie后打开ie就变成http://go.microsoft.com/fwlink/?LinkId=74005这个网站了](http://zhidao.baidu.com/link?url=7bqEHps4rS9S2CCiRgi96lQeWLESt_iLX22EbM3ZqyXI1yjXuJS_XdQxkehhwKp8KxfCIRREqkRxw16b9wRH_a)(话说,IE还分正版盗版么= =!)
* [注册表里 First Home page 的值改不了怎么办?](http://zhidao.baidu.com/link?url=YxOuzSrAbqZz5PPnzuZASEbvixbBhYzF_KpAeBUaNgIp9WXlWd2-ktxuslg3OzYjUJMjZRwAYX8BkGULSpMP1q)
* [如何锁定主页](http://zhidao.baidu.com/link?url=4GfkKDiaCVxKfO4yGSrjseWSgYmMXVqBPvGRtkajscnqXZE1_2dfGWkzxRLZExbzRVzZm9-YWITp9_QPzwshAa)(需要锁定主页的可用)
