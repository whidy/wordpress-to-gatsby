---
author: whidy
comments: true
date: 2014-04-07 10:00:33+00:00
template: post
link: http://www.whidy.net/absolute-element-scroll-without-blink.html
slug: /absolute-element-scroll-without-blink
title: 绝对定位元素随滚动条滑动无延时不闪烁的解决办法!
wordpress_id: 1884
category: '开发'
tags:
- 技术
- 网站
---

不得不说,清明放假,没什么好玩的,年纪来了,越发觉得打游戏也没意思,整天玩炉石被虐,为什么都喜欢跟风打鱼人流?我下午连续打了6盘有4盘是鱼人流,全败,基本不超过6个回合,我又是为了完成任务选的不常用的角色,打得我快吐,为了赢,为了刷排名?真是没意思,能不能打的有创意一点???更有甚者,明明是优势,确一个劲抽风似的对你说"打得不错",或者是嘲讽语,太脑残了!太脑残了!!!**这些玩炉石的人,太脑残了!!!**

好了,吐槽完毕,我不吐槽无法释放内心的不满.来说一说这两天的成果,搞得蛋都快碎了...

![绝对定位元素随滚动条滑动不闪烁DEMO](http://www.whidy.net/wp-content/uploads/2014/04/demo-400x225.jpg)

<!-- more -->

究竟是怎么回事呢?我来说说我做这件令我最后蛋疼的事情的原因.

我在做一个专题页,遇到了一个效果,这个效果就是某个内部元素随着浏览器滚动条上下移动,听起来不错哦~加个fixed属性?但是这个效果有几个条件限制,当这个元素超出父级元素高度后,隐藏,这个是fixed无法做到了,那么必然要用相对父级的元素进行绝对定位了.通过JS在每次触发浏览器滚动事件(**window.onscroll**)的时候进行一次重新定位.明白了思路后开始写代码,我做了个demo,实在受不了IETESTER各种BUG,本来昨晚就准备发布了,为了效果的完美性,我今天把虚拟机装了三个IE版本的XP,专门测试(途中在安装IE7还遇到了个[问题](http://www.whidy.net/xp-ie7-homepage-locked.html)).然后多次测试成完成了,先看效果:(或者[点击此页面查看](http://whidy.net/demos/demo_absoluteScroll.html)):

<del>http://jsfiddle.net/kingterrors/QkaB2/embedded/result,html,css,js/light</del>


    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <meta name="Author" content="whidy">
    <title>绝对定位元素随滚动条滑动不闪烁</title>
    <style>
    body {
    	background: #eee;
    	margin: 0;
    	padding: 0;
    }
    .container {
    	width: 1000px;
    	height: 5000px;
    	background: #ddd;
    	margin: 0 auto;
    }
    .wrapper {
    	height: 400px;
    	width: 998px;
    	background: #ccc;
    	border: 1px solid #aaa;
    	position: relative;
    	top:5%;
    	overflow: hidden;
    }
    .fixPos {
    	position: fixed;/* 解决CHROME不闪动的问题,不信你删了试试! */
    	visibility:hidden;
    }
    .content {
    	width:940px;
    	font: 100%/200% "Microsoft YaHei";
    	padding:0 30px;
    	position: absolute;
    	top: 50px;
    }
    .content h1 {
    	font:bold 150%/200% "Microsoft YaHei";
    }
    </style>
    </head>
    <body>
    <div class="container">
    	<div class="wrapper">
    		<div class="fixPos"></div>
    		<div class="content" id="con">
    			<h1>Solute an absolute elements scroll width no delay, no blink!</h1>
    			<P>I love you so much, whidy!</P>
    			<P>And you?</P>
    		</div>
    	</div>
    </div>
    <script type="text/javascript">
    window.onscroll = function(){
    	var con=document.getElementById('con');
    	// var scrollTopValue = document.documentElement.scrollTop || document.body.scrollTop;
    	// con.style.top = scrollTopValue/2 + 50 + 'px';
    	if(!document.body.scrollTop){//for IE 6,7,8 (8+版本未测试)
    		con.style.top = document.documentElement.scrollTop/2 + 50 + 'px';
    	} else {
    		con.style.top = document.body.scrollTop/2 + 50 + 'px';
    	}
    }
    </script>
    </body>
    </html>
    ```



我来简单说明一下:js里面有两条注释,实际上,是可以不用判断的,我不过为了让大家更清楚,IE8及以下版本和chrome等更标准的浏览器的差异性,旧版本的IE在新的文档声明内不能判断document.body.scrollTop值,所以需要使用document.documentElement.scrollTop来获取数值,这里有一篇文章可以给大家参考:[SD9013: 各浏览器对于 document、document.body、document.documentElement 对象的 onscroll 事件的支持存在差异](http://www.w3help.org/zh-cn/causes/SD9013).如果想省事,可以删掉判断语句,将注释去掉,也是可以的.对于这个效果说明就结束了.

如果细心的话,大家可以看到我demo内的CSS部分有一段**注释**,并且HTML内有个多余的**fixPos**的DIV,为什么要有这个?其实就这个小小的div,也把我弄了很长很长很长...的时间,写这个的原因?我本来一直使用chrome测试,而我参考的腾讯的页面[http://news.qq.com/zt2014/xzqne/index.htm](http://news.qq.com/zt2014/xzqne/index.htm)滚动流畅,为什么我一开始写的代码每次触发scroll事件都会闪动,或者说有延时呢?我当时以为其他浏览器都会闪动,后来才发现,原来这是chrome(版本号33.0.1750.154 m)的问题.其他的包括IE都是不会闪动的,为此我花了很长时间研究,终于找到了,这个东西,至于原理,我也不清楚,但是我要说的是,这个只是对chrome有效!如果其他人做类似的效果,遇到了同样的问题不妨试一下.

(刚才被朋友喊出去吃晚饭了,于是回来就忘记还有什么要写的了...= =!那就暂时写这么多吧.希望对大家有帮助.)

更新: Safari测试无效,和chrome在未加fixed效果相同.(2014年4月8日)
