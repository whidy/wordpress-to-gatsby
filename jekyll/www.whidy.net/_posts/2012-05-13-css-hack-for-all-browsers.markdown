---
author: whidy
comments: true
date: 2012-05-13 12:28:43+00:00
layout: post
link: http://www.whidy.net/css-hack-for-all-browsers.html
slug: css-hack-for-all-browsers
title: 主浏览器CSS HACK(IE6,IE7,IE8,IE9,Chrome,FF)
wordpress_id: 671
categories:
- CSS
- HTML
- IT技术
tags:
- 技术
---

三月底,在匆匆找到工作后,立即开始了新的生活,在和程序员简单的交接后,开始了程序员的职业生涯.

昨天在对公司新做的专题页面制作工程中,我仔细的测试了IE6,IE7,IE8,Chrome,Firefox兼容性,发现没有问题,上传至服务器,刚发布完成,有同事说有个地方标题换行了,我走过去一看,的确是的,不过十分好奇的是IE9,居然会跟Chrome等浏览器解析效果不同.于是我回到我的办公桌查阅了一些关于IE9方面CSS HACK的文章.现在总结如下:

其实关于IE6,IE7,IE8的CSS HACK方式我想大家耳熟能详了,这里就不复述了,需要查看的话可以参考下面的[CSS HACK文档](https://skydrive.live.com/redir.aspx?cid=6bac6bd5babf7270&resid=6BAC6BD5BABF7270!253&parid=undefined),这里我主要说明一下IE9的做法.

你可以通过给某个样式前面加个_:root_,例如:


    
    <code class="css">:root #element { font-size: 24px; } /* IE9 */
    </code>



最后附上一篇摘自网络的关于CSS hack 文档:[直接查看或下载](https://skydrive.live.com/redir.aspx?cid=6bac6bd5babf7270&resid=6BAC6BD5BABF7270!253&parid=undefined)(内含CSS HACK兼容表以及一些简单的兼容性技巧)

最后献上我经过反复测试的源码,大家也可以试试,不过注意css书写的顺序,免得出现问题.


    
    <code class="html"><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>ie9 css hack sample</title>
    <style>
    #element {
    	font-size: 30px;
    }
    #element {
    	font-weight: bold\9;/* IE */
    }
    #element {
    	*font-size: 14px;/* IE6+7, doesn't work in IE8/9 as IE7 */
    }
    #element {
    	_font-size: 10px;/* IE6 */
    }
    #element {
    	font-size: 18px\0;/* IE8+9  */
    }
    :root #element {
    	font-size: 24px;/* IE9 */
    }
    </style>
    </head>
    
    <body>
    <div>
    	<p id="element">IE font should be bolded</p>
    	<p id="element">IE6 font size should be 10px</p>
    	<p id="element">IE7 font size should be 14px</p>
    	<p id="element">IE8 font size should be 18px</p>
    	<p id="element">IE9 font size should be 24px</p>
    	<p id="element">Other should be 30px</p>
    	<em>This is a simple example for IE9 CSS Hack by <a href="/about">whidy</a>.</em>
    </div>
    </body>
    </html>
    </code>



<del>http://jsfiddle.net/kingterrors/LQhEr/embedded/result,html,css/</del>

当然有人会说,要用这么多不同的浏览器进行测试,尤其是IE9不支持XP,很麻烦,其实对于XP用户我推荐你们用Adobe的一个[BrowserLab](/dreamweaver-cs5-new-features-introduce.html)功能,之前也有过介绍,大家自己去看看,当然有装IE TESTER的朋友也可以测试多个不同的浏览器,不过XP依然不能用此软件测试IE9的效果,所以如何在XP下测试IE9的效果,那么只有用Adobe的BrowserLab,当然必须是在线的.如果大家有其他XP下测试IE9的CSS的办法欢迎发邮箱一起讨论.

最后上一张BrowserLab在线测试截图.

[caption id="attachment_758" align="aligncenter" width="400"][![IE9CssHack和BrowserLab测试](/wp-content/uploads/2012/05/IE9CssHack-400x250.jpg)](/wp-content/uploads/2012/05/IE9CssHack.jpg) IE9CssHack和BrowserLab测试[/caption]

如有错误欢迎大家指正!~

PS: 随着时间的推移,对于IE9, IE10以及IE11的hack越来越不好用了,实际上,对于IE9以上的版本就不建议hack了.尽量按照WEB规范标准来做,一般是不会有错的.(2014年5月19日22:52:40)
