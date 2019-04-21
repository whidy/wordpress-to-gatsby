---
author: whidy
comments: true
date: 2012-12-18 05:23:41+00:00
template: post
draft: false
link: http://www.whidy.net/js-time-line-pictures-slider.html
slug: /js-time-line-pictures-slider
title: 带进度条(时间轴)的焦点图切换特效(jQuery)
wordpress_id: 1495
category: '开发'
tags:
- 技术
- 教程
---

首先恶搞一下,电脑性能不佳者误入(其实我本来想用jsFiddle展示的,因为调用外部的速度太慢了.所以还是传到服务器给大家看).点击查看"[高速幻灯片](/demos/timeLineSlider/)"...好了,来说说正常点的.先看正常效果.

<del>http://jsfiddle.net/kingterrors/xGvkK/embedded/result,html,css,js/</del>

看完效果,代码什么的自己研究一下.当然这个效果部分是我写的,另外一部分是参考的网上的几个demo,以前收集的,也分享给大家:

<!-- more -->


    
    ```html
    <!doctype html>
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=gb2312">
    <script type="text/javascript" src="http://code.jquery.com/jquery-1.8.3.min.js"></script>
    <title>JS幻灯片插件</title>
    </head>
    <body>
    <style>
    br {clear:both;}
    .frame {width:600px;height:240px;background-color:#CCC;overflow:hidden;}
    .frame .list {list-style:none;padding:0;margin:0;width:10000px;}
    .frame .list li {width:600px;height:240px;float:left;}
    .frame #big_list2 {height:10000px;}
    .frame #big_list2 li {clear:both;}
    .frame #big_list4 {height:10000px;}
    .frame #big_list4 li {clear:both;}
    
    .l_frame {width:260px;height:80px;background-color:#CCC;overflow:hidden;float:left;}
    .l_frame .list {list-style:none;padding:0;margin:0;width:10000px;}
    .l_frame .list li {float:left;width:76px;height:76px;cursor:pointer;border:solid 2px #cc3910;}
    .l_frame .list .cur {border:solid 2px #0FF;}
    .l_frame2 {height:208px;width:80px;background-color:#CCC;overflow:hidden;}
    .l_frame2 .list {list-style:none;padding:0;margin:0;height:10000px;}
    .l_frame2 .list li {width:76px;height:76px;cursor:pointer;border:solid 2px #cc3910;}
    .l_frame2 .list .cur {border:solid 2px #0FF;}
    .slide_nav {height:80px;width:16px;display:block;float:left;background-color:#2A0;text-indent:-10000px;}
    .slide_nav2 {width:80px;height:16px;display:block;background-color:#2A0;text-indent:-10000px;}
    </style>
    <h3>A、大图：向左轮转；小图：向左轮转</h3>
    <div id="big_frame" class="frame">
    	<ul id="big_list" class="list">
    		<li style="background-color:#332f29;">aaaa</li>
    		<li style="background-color:#f1f2c0;">bb</li>
    		<li style="background-color:#ccc59e;">cc</li>
    		<li style="background-color:#8fa68e;">dd</li>
    		<li style="background-color:#cc3910;">eeee</li>
    	</ul>
    </div>
    <br />
    <a id="back" class="slide_nav" href="#">left</a>
    <div id="small_frame" class="l_frame">
    	<ul id="small_list" class="list">
    		<li class="cur" style="background-color:#332f29;">aaaa</li>
    		<li style="background-color:#f1f2c0;">bb</li>
    		<li style="background-color:#ccc59e;">cc</li>
    		<li style="background-color:#8fa68e;">dd</li>
    		<li style="background-color:#cc3910;">eeee</li>
    	</ul>
    </div>
    <a id="forward" class="slide_nav" href="#">right</a>
    <br />
    <br />
    <br />
    <br />
    <h3>B、大图：向上轮转；小图：向左轮转</h3>
    <div id="big_frame2" class="frame">
    	<ul id="big_list2" class="list">
    		<li style="background-color:#d57d50;">aaaa</li>
    		<li style="background-color:#cc3910;">bb</li>
    		<li style="background-color:#f1f2c0;">cc</li>
    		<li style="background-color:#ccc59e;">dd</li>
    		<li style="background-color:#8fa68e;">eeee</li>
    		<li style="background-color:#332f29;">FFF</li>
    	</ul>
    </div>
    <br />
    <a id="back2" class="slide_nav" href="#">a</a>
    <div id="small_frame2" class="l_frame">
    	<ul id="small_list2" class="list">
    		<li class="cur" style="background-color:#d57d50;">aaaa</li>
    		<li style="background-color:#cc3910;">bb</li>
    		<li style="background-color:#f1f2c0;">cc</li>
    		<li style="background-color:#ccc59e;">dd</li>
    		<li style="background-color:#8fa68e;">eeee</li>
    		<li style="background-color:#332f29;">FFF</li>
    	</ul>
    </div>
    <a id="forward2" class="slide_nav" href="#">b</a>
    <br />
    <br />
    <br />
    <br />
    <h3>C、大图：向左轮转；小图：向上轮转</h3>
    <div style="float:left;">
    	<div id="big_frame3" class="frame">
    		<ul id="big_list3" class="list">
    			<li style="background-color:#d57d50;">aaaa</li>
    			<li style="background-color:#cc3910;">bb</li>
    			<li style="background-color:#f1f2c0;">cc</li>
    			<li style="background-color:#ccc59e;">dd</li>
    			<li style="background-color:#8fa68e;">eeee</li>
    			<li style="background-color:#332f29;">FFF</li>
    		</ul>
    	</div>
    </div>
    <div style="float:left; margin:0 0 0 8px;">
    	<a id="back3" class="slide_nav2" href="#">a</a>
    	<div id="small_frame3" class="l_frame2">
    		<ul id="small_list3" class="list">
    			<li class="cur" style="background-color:#d57d50;">aaaa</li>
    			<li style="background-color:#cc3910;">bb</li>
    			<li style="background-color:#f1f2c0;">cc</li>
    			<li style="background-color:#ccc59e;">dd</li>
    			<li style="background-color:#8fa68e;">eeee</li>
    			<li style="background-color:#332f29;">FFF</li>
    		</ul>
    	</div>
    	<a id="forward3" class="slide_nav2" href="#">b</a>
    </div>
    <br />
    <br />
    <br />
    <br />
    <h3>D、大图：向上轮转；小图：向上轮转</h3>
    <div style="float:left;">
    	<div id="big_frame4" class="frame">
    		<ul id="big_list4" class="list">
    			<li style="background-color:#d57d50;">aaaa</li>
    			<li style="background-color:#cc3910;">bb</li>
    			<li style="background-color:#f1f2c0;">cc</li>
    			<li style="background-color:#ccc59e;">dd</li>
    			<li style="background-color:#8fa68e;">eeee</li>
    			<li style="background-color:#332f29;">FFF</li>
    		</ul>
    	</div>
    </div>
    <div style="float:left; margin:0 0 0 8px;">
    	<a id="back4" class="slide_nav2" href="#">a</a>
    	<div id="small_frame4" class="l_frame2">
    		<ul id="small_list4" class="list">
    			<li class="cur" style="background-color:#d57d50;">aaaa</li>
    			<li style="background-color:#cc3910;">bb</li>
    			<li style="background-color:#f1f2c0;">cc</li>
    			<li style="background-color:#ccc59e;">dd</li>
    			<li style="background-color:#8fa68e;">eeee</li>
    			<li style="background-color:#332f29;">FFF</li>
    		</ul>
    	</div>
    	<a id="forward4" class="slide_nav2" href="#">b</a>
    </div>
    <br />
    <br />
    <br />
    <br />
    <script type="text/javascript">
    //初始化
    function C_slider(frame, list, Lframe, Llist, forwardEle, backEle, scrollType, LscrollType, acitonType, autoInterval) {
    	this.frame = frame;
    	this.list = list;
    	this.Lframe = Lframe;
    	this.Llist = Llist;
    	this.forwardEle = forwardEle;
    	this.backEle = backEle;
    	this.scrollType = scrollType;
    	this.LscrollType = LscrollType;
    	this.acitonType = acitonType;
    	this.autoInterval = autoInterval;
    
    	this.slideLength = $("#" + this.Llist + " > li").length; //总的slider数量
    	this.currentSlide = 0;
    	this.FrameHeight = $("#" + this.frame).height();
    	this.FrameWidth = $("#" + this.frame).width();
    	this.lFrameHeight = $("#" + this.Lframe).height();
    	this.lFrameWidth = $("#" + this.Lframe).width();
    	this.lListHeight = $("#" + this.Llist + " >li").eq(0).outerHeight(true);
    	this.lListWidth = $("#" + this.Llist + " >li").eq(0).outerWidth(true);
    
    	var self = this;
    
    	for (var i = 0; i < this.slideLength; i++) {
    		$("#" + this.Llist + " > li").eq(i).data("index", i);
    		$("#" + this.Llist + " > li").eq(i).bind(this.acitonType,
    		function() {
    			self.go($(this).data("index"));
    		});
    	};
    
    	//给“上一个”、“下一个”按钮添加动作
    	$("#" + this.forwardEle).bind('click',
    	function() {
    		self.forward();
    		return false;
    	});
    	$("#" + this.backEle).bind('click',
    	function() {
    		self.back();
    		return false;
    	});
    
    	//定论鼠标划过时，自动轮换的处理
    	$("#" + this.frame + ",#" + this.Lframe + ",#" + this.forwardEle + ",#" + this.backEle).bind('mouseover',
    	function() {
    		clearTimeout(self.autoExt);
    	});
    
    	$("#" + this.frame + ",#" + this.Lframe + ",#" + this.forwardEle + ",#" + this.backEle).bind('mouseout',
    	function() {
    		clearTimeout(self.autoExt);
    		self.autoExt = setTimeout(function() {
    			self.extInterval();
    		},
    		self.autoInterval);
    	});
    
    	//开始自动轮换
    	this.autoExt = setTimeout(function() {
    		self.extInterval();
    	},
    	this.autoInterval);
    }
    //执行运动
    C_slider.prototype.go = function(index) {
    	this.currentSlide = index;
    	if (this.scrollType == "left") {
    		$("#" + this.list).animate({
    			marginLeft: ( - index * this.FrameWidth) + "px"
    		},
    		{
    			duration: 600,
    			queue: false
    		});
    	} else if (this.scrollType == "top") {
    		$("#" + this.list).animate({
    			marginTop: ( - index * this.FrameHeight) + "px"
    		},
    		{
    			duration: 600,
    			queue: false
    		});
    	}
    
    	$("#" + this.Llist + " > li").removeClass("cur");
    	$("#" + this.Llist + " > li").eq(index).addClass("cur");
    
    	//对于缩略图的滚动处理
    	if (this.LscrollType == "left") {
    		if (this.slideLength * this.lListWidth > this.lFrameWidth) {
    			var spaceWidth = (this.lFrameWidth - this.lListWidth) / 2;
    			var hiddenSpace = this.lListWidth * this.currentSlide - spaceWidth;
    
    			if (hiddenSpace > 0) {
    				if (hiddenSpace + this.lFrameWidth <= this.slideLength * this.lListWidth) {
    					$("#" + this.Llist).animate({
    						marginLeft: -hiddenSpace + "px"
    					},
    					{
    						duration: 600,
    						queue: false
    					});
    				} else {
    					var endHidden = this.slideLength * this.lListWidth - this.lFrameWidth;
    					$("#" + this.Llist).animate({
    						marginLeft: -endHidden + "px"
    					},
    					{
    						duration: 600,
    						queue: false
    					});
    				}
    			} else {
    				$("#" + this.Llist).animate({
    					marginLeft: "0px"
    				},
    				{
    					duration: 600,
    					queue: false
    				});
    			}
    		}
    	} else if (this.LscrollType == "top") {
    		if (this.slideLength * this.lListHeight > this.lFrameHeight) {
    			var spaceHeight = (this.lFrameHeight - this.lListHeight) / 2;
    			var hiddenSpace = this.lListHeight * this.currentSlide - spaceHeight;
    
    			if (hiddenSpace > 0) {
    				if (hiddenSpace + this.lFrameHeight <= this.slideLength * this.lListHeight) {
    					$("#" + this.Llist).animate({
    						marginTop: -hiddenSpace + "px"
    					},
    					{
    						duration: 600,
    						queue: false
    					});
    				} else {
    					var endHidden = this.slideLength * this.lListHeight - this.lFrameHeight;
    					$("#" + this.Llist).animate({
    						marginTop: -endHidden + "px"
    					},
    					{
    						duration: 600,
    						queue: false
    					});
    				}
    			} else {
    				$("#" + this.Llist).animate({
    					marginTop: "0px"
    				},
    				{
    					duration: 600,
    					queue: false
    				});
    			}
    		}
    	}
    
    }
    //前进
    C_slider.prototype.forward = function() {
    	if (this.currentSlide < this.slideLength - 1) {
    		this.currentSlide += 1;
    		this.go(this.currentSlide);
    	} else {
    		this.currentSlide = 0;
    		this.go(0);
    	}
    }
    //后退
    C_slider.prototype.back = function() {
    	if (this.currentSlide > 0) {
    		this.currentSlide -= 1;
    		this.go(this.currentSlide);
    	} else {
    		this.currentSlide = this.slideLength - 1;
    		this.go(this.slideLength - 1);
    	}
    }
    //自动执行
    C_slider.prototype.extInterval = function() {
    	if (this.currentSlide < this.slideLength - 1) {
    		this.currentSlide += 1;
    		this.go(this.currentSlide);
    	} else {
    		this.currentSlide = 0;
    		this.go(0);
    	}
    
    	var self = this;
    	this.autoExt = setTimeout(function() {
    		self.extInterval();
    	},
    	this.autoInterval);
    }
    //实例化对象
    var goSlide1 = new C_slider("big_frame", "big_list", "small_frame", "small_list", "forward", "back", "left", "left", "click", 3000);
    var goSlide2 = new C_slider("big_frame2", "big_list2", "small_frame2", "small_list2", "forward2", "back2", "top", "left", "click", 5000);
    var goSlide3 = new C_slider("big_frame3", "big_list3", "small_frame3", "small_list3", "forward3", "back3", "left", "top", "click", 3000);
    var goSlide4 = new C_slider("big_frame4", "big_list4", "small_frame4", "small_list4", "forward4", "back4", "top", "top", "click", 2000);
    </script>
    </body>
    </html>
    ```



其实我的那个效果就是基于此文件制作的.当然我的效果还是有许多不足之处的.不过勉强能用~

最后互联网上也有这个关于进度条的效果,有兴趣可以看看比如瘾科技英文站,甚至还有网上关于类似此效果的源码,不过我发现不兼容CHROME我就不在这里放出来了.纠纷像我这个效果供讨论学习吧.

对了,我这个好像对IE6兼容有点问题???没测试哟.电脑IETESTER老报错,不兼容就让IE6去死吧.z

PS: 回头看到这篇文章,我真是佩服自己,现在连原生的都没搞明白,我之前怎么做出来这玩意的,,,有机会还是改良一个好点的,这个东西就供大家参考吧(2014年5月23日)
