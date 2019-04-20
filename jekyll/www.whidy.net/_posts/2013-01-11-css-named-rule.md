---
author: whidy
comments: true
date: 2013-01-11 06:55:25+00:00
template: post
link: http://www.whidy.net/css-named-rule.html
slug: /css-named-rule
title: CSS命名规则经验之常用的CSS类名举例
wordpress_id: 1549
category: '开发'
tags:
- 技术
- 网站
---

最近又开始慢慢花更多静力去学习CSS了.好久没有看CSS的文章了,突然发现自己连CSS类名都不知道是什么了.于是随便找了一下资料,其实类名原来就是CSS类的命名嘛...

今天分享一篇常用CSS类名的举例.

首先说说这个敲代码,最忌讳的就是敲完后连自己都看不懂,那么命名很重要,规范更重要,英语不好的同学的确还是要好好的学习一下.当然好的class至少是要别人看得懂,更重要的是有自己的规范,方便,简洁,明了.



	
  * **class="fixed" fixed这个class几乎出现在没个样式文件中,用在为包含浮动子元素的容器元素清除浮动,样式如下:**


    
    ```css
    .fixed:after{content:".";display:block;height:0;clear:both;visibility:hidden;}
    .fixed{display:block;}
    /* \*/
    .fixed{min-height:1%;}
    * html .fixed{height:1%;}
    ```



这个样式就可以用在下面的情形，每个li都是浮动的：

<!-- more -->


    
    ```html
    <ul class="fixed">
    <li><img src="images/img_01.jpg" alt="First Thumb" /></li>
    <li><img src="images/img_02.jpg" alt="Second Thumb" />
    ...</li>
    </ul>
    ```





	
  * **class="alt"  alt是"alternative"(交替)的简称,这个class用在有一组样式一样的元素,需要为其中的某几个设定特别的样式,比如一组向左浮动的图片中需要有一张是向右浮动,可以这样:**


    
    ```css
    #content img{float:left;display:inline;margin-right:10px;border:1px solid #ccc;padding:1em 0;background:#fff;}
    #content img.alt{float:right;margin-right:0;margin-left:10px;}
    ```





	
  * **class="selected"  这个比较常见了,一般用于事件触发的样式,例如mouseover或选中元素的效果.**


    
    ```html
    <li class="selected"><a href="/about">About Us</a></li>
    <!-- 选项卡制作的时: -->
    <dl>
    <dt class="selected">Tag Cloud</dt>
    ...
    </dl>
    ```





	
  * **class="first", class="last"  毕竟目前:first-child和:last-child这两个伪类有时候的确不好用.这里不详解(可参考之前写过[CSS选择器](http://www.whidy.net/how-to-remove-margins-for-first-last-elements.html))**

	
  * **class="inner"  inner也是经常使用的class,而且大部分上是用来制造视觉上的额外效果,用来给嵌套在容器里的子容器定义样式(比如制作双背景图片效果).**

	
  * **class="section"  一般用在为指定内容中特定部分添加特定的样式:**


    
    ```html
    <div class="section">
    content here...
    </div>
    ```






差不多想到的就这么多了,部分也是从互联网上看到的,当然其实看到上面几个.也有很多人知道,也不可能全记下来.这里把网上找到的可能也不算特别完整的分享出来,自己也多看看加深印象.


<blockquote>

> 
> #### **样式文件命名规范
**
> 
> 
主要：master.css, style.css, main.css
布局：layout.css
专栏：columns.css
文字：font.css
打印：print.css
主题：themes.css


> 
> #### **CSS ID 的命名**
> 
> 
页头：header
登录条：loginbar
标志：logo
侧栏：sidebar
广告：banner
导航：nav
子导航：subnav
菜单：menu
子菜单：submenu
搜索：search
滚动：scroll
页面主体：main
内容：content
标签页：tab
文章列表：list
提示信息：msg
小技巧：tips
栏目标题：title
加入：joinus
指南：guild
服务：service
热点：hot
新闻：news
下载：download
注册：regsiter
状态：status
按钮：btn
投票：vote
合作伙伴：partner
友情链接：friendlink
页脚：footer
版权：copyright
外套：wrap
主导航：mainnav
子导航：subnav
页脚：footer
整个页面：content
页眉：header
页脚：footer
商标：label
标题：title
主导航：mainbav（globalnav）
顶导航：topnav
边导航：sidebar
左导航：leftsidebar
右导航：rightsidebar
旗志：logo
标语：banner
菜单内容1：menu1content
菜单容量：menucontainer
子菜单：submenu
边导航图标：sidebarIcon
注释：note
面包屑：breadcrumb(即页面所处位置导航提示）
容器：container
内容：content
搜索：search
登陆：Login
功能区：shop(如购物车，收银台)
当前的：current
</blockquote>


好了差不多就这么多了有空多看看多背背...这是初级知识哟
