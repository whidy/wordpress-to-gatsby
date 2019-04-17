---
author: whidy
comments: true
date: 2013-10-30 02:23:52+00:00
layout: post
link: http://www.whidy.net/bf4-directx-function-error-solution.html
slug: bf4-directx-function-error-solution
title: 战地4运行提示directX function错误解决方案
wordpress_id: 1817
categories:
- 其它
- 杂谈
tags:
- 技术
---

作为FPS爱好者,战地4的发布必然第一时间下载下来玩一下,可是却遇到了问题,下载的硬盘版解压后运行,出现以下错误提示:

directX function "m_dxgiFactory->CreateSwapChain(m_device,&sd,&screen->swapC......(后面一大堆省略,没有截图...)

那么先上百度查,基本上都说是改为兼容模式就行了,对于我来说完全是扯淡,没用.

我的配置: WIN 8.1 64BIT + GTX660M , 最新的显卡驱动,才出的优化了BF4的N卡驱动,最新的DX,所有游戏组件已安装,,,那么究竟是什么问题导致呢.还是谷歌给力.找到了解决方案,虽然不知道是不是全部都适用,至少我的问题解决了.有调整为兼容模式仍然无法运行的可以试试,这个办法:

![战地4解决DX错误](http://www.whidy.net/wp-content/uploads/2013/10/bf4-400x264.jpg)

在控制面板 - 区时钟,语言和区域 - 区域 - 管理(选项卡) - 更改系统区域设置 - 然后如图改成**英语(美国)**重启后就可以了.

内容参考: [BF4 DirectX Error](http://battlelog.battlefield.com/bf3/en/forum/threadview/2955064766441724035/last/)

当然后来也有人说使用Microsoft AppLocale解决地区模拟的问题,不过我好像弄失败了.如果有兴趣大家也可参考:[百度搜索出很多结果,自己看咯](http://www.baidu.com/s?ie=UTF-8&wd=%E6%88%98%E5%9C%B04+applocale)
