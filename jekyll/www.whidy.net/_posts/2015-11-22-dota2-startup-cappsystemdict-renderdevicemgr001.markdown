---
author: whidy
comments: true
date: 2015-11-22 09:34:59+00:00
excerpt: 'dota2启动报错解决

  CAppSystemDict::LoadSystemAndDependecies():

  AppSystemDict: Error in init() of interface ''RenderDeviceMgr001''!'
layout: post
link: http://www.whidy.net/dota2-startup-cappsystemdict-renderdevicemgr001.html
slug: dota2-startup-cappsystemdict-renderdevicemgr001
title: dota2启动报错解决办法(CAppSystemDict::...RenderDeviceMgr001)
wordpress_id: 2833
categories:
- 兴趣
- 其它
- 精彩分享
tags:
- 技术
- 教程
---

好久没玩下dota2了.有几个朋友找起说耍一下.决定一起开开黑玩玩...经过几G的更新等待.准备启动游戏...却弹出了这个鬼玩意...

[![dota2error](http://www.whidy.net/wp-content/uploads/2015/11/dota2error-400x151.png)](http://www.whidy.net/wp-content/uploads/2015/11/dota2error.png)


<blockquote>CAppSystemDict::LoadSystemAndDependecies():
AppSystemDict: Error in init() of interface 'RenderDeviceMgr001'!</blockquote>


这到底是个什么鬼呢?百度一下...找到的都是以下几个无效方案(也许针对其他报错可能有用,但是如果你和我一样也是RenderDeviceMgr001错误,或许你就要用别的方法了).



	
  1. 检查文件完整性

	
  2. 找到安装目录的video.txt修改什么fullscreen为0还是1的什么鬼.

	
  3. 修改桌面分辨率.

	
  4. 还有不着边际的重装驱动,重装游戏或电脑(...)


反正都没用,也不知道他们怎么弄好的...

无奈用google查了下.可能有用的方法有以下的几个

	
  1. 删除游戏快捷方式的启动项或者是游戏设置的启动项,比如-console之类的

	
  2. **游戏启动项设置为-dx11**


我是用了第二个就终于进入游戏了...希望有其他人遇到此问题,并用坑爹的百度搜索能找到正确的解决方案... :roll:

参考资料

	
  1. [How to fix RenderDeviceMgr001 error](https://steamcommunity.com/app/570/discussions/0/530645446314717869/)

	
  2. [Custom mode error - RenderDeviceMgr001](https://steamcommunity.com/app/570/discussions/0/627456486341532078/)

	
  3. [Reborn: Getting a diff error message than everyone else](https://www.reddit.com/r/DotA2/comments/3a85oa/reborn_getting_a_diff_error_message_than_everyone/)


最后说明下我的配置: win10 64bit + GTX660M + 驱动359.0
