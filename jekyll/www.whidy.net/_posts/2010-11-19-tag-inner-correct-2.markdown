---
author: whidy
comments: true
date: 2010-11-19 12:23:46+00:00
layout: post
link: http://www.whidy.net/tag-inner-correct-2.html
slug: tag-inner-correct-2
title: js修改标签内内容(下)
wordpress_id: 170
categories:
- IT技术
- Javascript
- 技术分享
tags:
- 技术
- 网站
---

经过彻夜和一上午的研究,现在总算是把最终效果弄出来了,我先上代码,老鸟不要笑话(这么简单的东西琢磨半天...),没办法,没有系统学习过这个玩意,很多东西都出问题.代码如下:


    
    <code><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>输入框焦点样式变化测试</title>
    <!--文本框样式可以忽略,不过为了增加特效的观赏性,我简单的加上了.-->
    <style>
    input {border:1px solid #eee;height:20px;width:100px;line-height:20px;}
    </style>
    <script type="text/javascript">
    window.onload = iSC; //加载iSC()函数
    function iSC() {
    inputs=document.getElementsByTagName("input");
    for(i=0;i<inputs.length;i++) {
    inputs[i].onmouseup = function(){this.style.backgroundColor='#fffab5';}
    inputs[i].onblur = function(){this.style.backgroundColor='#fff';}
    }
    }
    </script>
    </head>
    <body>
    <form>
      <input type="text" />
      <input type="text" />
      <input type="text" />
    </form>
    </body>
    </html>
    </code>



当然这只是一个简单的示例,效果也很简单.那段JS也不难理解,这里并没有用到之前所想的用setAttribute()来解决,而后来的多次测试,不知道是不是我代码不对还是其他原因,通过这个方法无法达到目的.总之,通过这个简单的东西我总结出了几个需要注意的问题:



	
  1. _inputs[i].onmouseup = function(){this.style.backgroundColor='#fffab5';}_不能通过_inputs[i].setAttribute("__onmouseup__","__function(){this.style.backgroundColor='#fffab5';__")_来实现.

	
  2. _window.onload = iSC;_千万不能忘记!否则,你会发现,他根本没有运行这个js.当然你同样可以在测试的时候,写一个按钮,测试这个js是否读取了所有的input标签,方便调试.


关于此次学习的其他方面总结包括,在查找问题的同时,我学到了其他的一些特效,特别分享给大家.

其实,在一些高级的浏览器(我基本是把除了IE6(包括相同核心),其他的都算高级了,IE7那不伦不类,IE8稍有长进~)中,input设置一个伪类,十分简单的就可以实现以上效果:

	
  * 看这个就知道了(除了IE6不行,我测试过IE8和chrome都是没有问题的,我想其他的比如FF,OPERA应该也没有问题吧)

    
    <code><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>最简单的输入框变化方法</title>
    <style>
    input:focus {background-color:#FF9;}
    </style>
    </head>
    <body>
    <input type="text" />
    <input type="text" />
    <input type="text" />
    </body>
    </html>
    </code>





	
  * 另外还有许多其他的效果,比如跟这个类似的,并非样式变化,而是当光标焦点处于输入框时,输入框默认value改变,比如,默认value="请在此处输入用户名",当焦点在此时,value=""等待用户输入,,等等效果,这里不一一列举,为了方便大家学习,我顺便将其打包,部分代码摘自互联网,版权的话,我也找不到了,反正大家学习嘛,我想这小东西不会还说我侵权吧...z当然以上我自己总结的东西,大家尽管拿去,有什么疑问也可以发邮箱与我联系交流.

	
  * 其他部分特效源码打包下载([skydrive网盘地址下载](http://cid-3eb8edff1814d075.office.live.com/self.aspx/Documents/input%E8%BE%93%E5%85%A5%E6%A1%86%E5%8F%98%E5%8C%96%E5%90%84%E7%A7%8D%E7%89%B9%E6%95%88%E5%AD%A6%E4%B9%A0.zip))(除了我这两种之外的源码在内,还有其他三种比较简单的效果)

	
  * 百度可参考的资料,其实后来我发现,这个不就是我那个差不多的嘛,汗我研究这么久,[http://baike.baidu.com/view/1710146.htm](http://baike.baidu.com/view/1710146.htm)


