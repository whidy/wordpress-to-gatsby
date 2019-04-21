---
author: whidy
comments: true
date: 2015-01-18 09:47:42+00:00
description: 有个bug只会在ios的safari浏览器上出现,就是无法禁止底部浏览器自带区域的touchmove事件,这究竟是怎么回事呢
template: post
draft: false
link: http://www.whidy.net/ios-safari-bug-touchmove.html
slug: /ios-safari-bug-touchmove
title: ios safari浏览器底部touchmove事件无效的BUG?
wordpress_id: 2696
category: '开发'
tags:
- 技术
---

最近做一个wap页面需要一个层从右侧弹出类似菜单一样的东西,效果比较类似百度百科移动端页面[范例](http://wapbaike.baidu.com/view/3091.htm)里面的效果.

我仿照的做完后.发现有个很神奇的bug,这个bug只会在ios的safari浏览器上出现.就是无法禁止底部浏览器自带区域的touchmove事件,可能表达不太容易理解,首先用iphone(我测试过4s和6p)的safari浏览器打开这个页面[DEMO](http://www.whidy.net/demos/touchmove.html).然后我下面用图片来解释具体操作方式

![ios safari bug](https://www.whidy.net/wp-content/uploads/2015/01/demo_png.png)

将页面滑至黑色块刚好处于手机浏览器底部,然后触屏滑动发现页面跟着滚动了.本来黑色块属于灰色区域,已经禁止了touchmove事件,而左侧浅灰色区域是可以任意滑动的.

那么这个问题会导致页面看起来不正常.经过多次测试,发现百度百科的页面也是如此,也就是说safari底部有一块区域是无法禁止页面滚动的,除非将当前页面高度设置成屏幕大小相同.但是这个方法并不好.

那么至此,这个问题究竟是safari的问题还是另有其他方法解决呢,我还在研究中...

PS:ios下其他浏览器均正常,android各浏览器均正常
