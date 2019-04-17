---
author: whidy
comments: true
date: 2014-12-03 13:37:39+00:00
excerpt: 这几天做东西发现chrome 39的多个版本上,在带有参数的url链接上出现无法调试的情况,而且相当频繁,实在是让人恼火又着急.本机的是版本 39.0.2171.71
  m,包括办公室的另一个chrome 39也这鸟样...
layout: post
link: http://www.whidy.net/chrome-39-connot-debug.html
slug: chrome-39-connot-debug
title: chrome 39 有时候出现无法调试?
wordpress_id: 2644
categories:
- IT技术
- 技术分享
tags:
- 技术
- 教程
---

这几天做东西发现chrome 39的多个版本上,在带有参数的url链接上出现无法调试的情况,而且相当频繁,实在是让人恼火又着急.本机的是版本 39.0.2171.71 m,包括办公室的另一个chrome 39也这鸟样...

不知道其他人有遇到过吗,尤其是这个error.竟然搜不到- -!也是醉了.

[caption id="attachment_2645" align="aligncenter" width="400"][![chrome_debug_error](http://www.whidy.net/wp-content/uploads/2014/12/chrome_error-400x153.png)](http://www.whidy.net/wp-content/uploads/2014/12/chrome_error.png) chrome_debug_error[/caption]

现实出现console面板带抖动,文字变得不清晰,然后刷新页面几次就出现Failed to get text for stylesheet  1 : No style sheet with given id found, 其中的数字会每次刷新后累加...莫名其妙!

要问我解决办法,只能带着淡淡的忧伤的心情告诉你,我开了两个chrome,新版的是为了同步数据,旧版的是为了调试 :cry:

PS: 

或者在地址栏输入chrome://flags 全部重置为默认值(不过不敢保证有效- -)

或参考[Error shows “Failed to get text for stylesheet (#): No style sheet with given id found”, what does this mean?](http://stackoverflow.com/questions/26894718/error-shows-failed-to-get-text-for-stylesheet-no-style-sheet-with-given-id)不过似乎也并未提出良好的解决方案
