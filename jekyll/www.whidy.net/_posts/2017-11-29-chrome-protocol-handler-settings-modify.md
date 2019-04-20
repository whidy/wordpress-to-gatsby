---
author: whidy
comments: true
date: 2017-11-29 12:16:36+00:00
excerpt: 由于误操作，造成Chrome启动关联程序的协议链接被禁用，那么怎么重新修改设置，启动相关的程序呢，这里将为大家解答！
template: post
link: http://www.whidy.net/chrome-protocol-handler-settings-modify.html
slug: /chrome-protocol-handler-settings-modify
title: Chrome启动关联程序的协议链接误操作被禁用后如何修改设置重新开启
wordpress_id: 3047
category: '开发'
tags:
- 技术
- 教程
---

该文章适用于Windows 7 x64下Chrome版本 62.0.3202.94（正式版本） （64 位）的设置，其他设备不明。也许WIN10也可以，但是可能会由于Chrome版本区别而不可用。

今天回到宿舍，要用百度云盘下载点东西，结果，手误，勾选记住后，点了不要打开，为什么要高亮不要打开，泪奔。。。界面是这样的：

![百度云的链接协议设置protocol settings](https://www.whidy.net/wp-content/uploads/2017/11/protocol-400x129.png)

<!-- more -->而我居然点错了！！！怎么办，找不回来了。然后再次点击下载就只能干瞪眼：

![无法关联百度云盘程序](https://www.whidy.net/wp-content/uploads/2017/11/dl-400x235.png)

为了解决这个问题,第一反应去谷歌浏览器的设置里翻遍了，但也没有找到！只能搜索一下网上有没有解决方案，找了很多，唯一有用的估计就是这个2012年发表的一篇文章（具体原创不知道了，这里放两个内容相同的链接，以便于我下文的解决方案不可用时，大家尝试这个）：

[chrome用到外部程序的时候会出现一个对话框，启动或者拒绝（比如阿里旺旺和迅雷）。如何启动已经设置成永不启动的程序？](https://www.zhihu.com/question/20529039)

[chrome打开外部协议程序](https://www.chenyudong.com/archives/chrome-open-external-protocal.html)

好了，我这里想说，这个修改或者说直接删除**Local State**文件的方法在我的电脑上并不适用，我推测应该是Chrome版本更新的原因，相关配置已经不在这里了。

那怎么办呢，又去找了很多关于修改关联协议链接应用的设置也没有结果，索性，自己研究一下Chrome的**User Data**目录，功夫不负有心人，我找了很久（你们觉得我找了多久。。。），终于找到文件“**C:\Users\Whidy(你的用户名)\AppData\Local\Google\Chrome\User Data\Default\Preferences**”里发现了一个可能是修改配置（请用文本编辑器记事本之类的工具打开）：

![设置协议程序启动的配置](https://www.whidy.net/wp-content/uploads/2017/11/settings-400x282.png)

如果感觉阅读这些配置比较困难，可以将文档改成Javascript语言模式（当然改功能依赖各种编辑器，我这里是VSCode）就清晰了，有空的话也可以看看其他的有没有什么有趣的配置选项：

![排版后的效果](https://www.whidy.net/wp-content/uploads/2017/11/settings-2.png)

这个从英文中不难看出，协议处理(protocol_handler) > 排除的项列表(excluded_schemes) > 这里的**baiduyunguanjia**被设置为**true**，就是确认被排除，因此浏览器对于该协议的链接不做处理。那么，目前你有两个选择：



 	
  1. 在配置图一将相关配置代码（"baiduyunguanjia":false,）删除，并保存！

 	
  2. 在配置图一中，"baiduyunguanjia":false,修改为"baiduyunguanjia":**true**，并保存！


以上修改请在关闭chrome时进行！我才用了选择一，因为我的手残，我想再来一次！！！

果然，再次启动chrome后，百度云盘页面点击下载终于再次出现了：

![再次出现的配置](https://www.whidy.net/wp-content/uploads/2017/11/protocol-400x129.png)

这次不会点错了。我选择了**打开 BaiduyunguanjiaProtocol**，百度云盘软件成功启动，终于解决了！

当然这篇文章仅以百度云盘举例，还有其他的一些软件比如迅雷等等有协议关联的程序也可以重新设置，哇嗷，舒服了~我想这应该是网上第一篇吧关于修改协议配置启动程序的解决办法吧，希望能帮到大家~
