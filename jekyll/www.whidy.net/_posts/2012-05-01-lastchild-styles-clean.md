---
author: whidy
comments: true
date: 2012-05-01 13:59:30+00:00
template: post
link: http://www.whidy.net/lastchild-styles-clean.html
slug: /lastchild-styles-clean
title: 列表中最后一个元素样式清除修改方法(jQuery)
wordpress_id: 707
category: '开发'
tags:
- 技术
- 网站
---

我们在做动态网站的时候,当遇到导航条的栏目列表或某区域内文章列表等含有大量重复内容区域时,通常会用循环将他们输出,而他们节点的样式都是相同的,比如下边距,外边框的分隔样式,通过循环输出的结果就是最后一个节点依然保留着所有的样式我们是不希望他有下边距或者外边框.

例如: 导航上每个**栏目标题(li)**右侧可能会用竖线分隔每个栏目标题,于是最后一个栏目右侧也出现了不想要的竖线,但是这些同级的**li**都是循环出来的 ,我们无法单独给最后一个元素添加特殊的样式,本来有个很简单的方法,那就是使用**CSS3的:first和:last选择器**,但是当IE6和IE7不支持:first和:last选择器的,有个简单的方法,通过Js(本文用的jQuery)去除或修改列表或循环内容的第一个和最后一个节点的样式,可以兼容所有浏览器,是比较方便的,其实用js可以轻松实现,但是我后来发现,jQuery来处理或许更加轻松些,也是正好我最近在学习jQuery,的确很好用.在body内最后加上一小段就可以了,比如下面这个简单的例子:


    
    ```html
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>LastChildStyleRemove</title>
    <script src="http://code.jquery.com/jquery-latest.js"></script>
    <style>
    #mainContent {background-color:#eee;}
    #mainContent ul.nav {list-style:none;font-size:12px;}
    #mainContent ul.nav li {float:left;padding:5px 15px;border-left:1px solid #fff;border-right:1px solid #ddd;}
    #mainContent ul.nav li a {color:#666;text-decoration:none;}
    </style>
    </head>
    <body>
    	<div id="mainContent">
    		<ul class="nav">
    			<li><a href="#">导航一</a></li>
    			<li><a href="#">导航二</a></li>
    			<li><a href="#">导航三</a></li>
    			<li><a href="#">导航四</a></li>
    		</ul>
    		<div style="clear:both;"></div>
    	</div>
    </body>
    <script>
    	$("#mainContent ul.nav li:first-child").css("border-left", "none")
    	$("#mainContent ul.nav li:last-child").css("border-right", "none")
    </script>
    </html>
    ```



这个例子除了用到最后一个元素样式清除,也用了首个元素样式清除,这个很好理解,这是两个方法,其实只用到一个函数[css( propertyName , value  )](http://api.jquery.com/css/#css2),而关于元素选择器可以查看jQuery的例子:[:first-child Selector](http://api.jquery.com/first-child-selector/)和[:last-child Selector](http://api.jquery.com/last-child-selector/).上面的例子也很简单清晰易懂...

当然我也在网上看到有这样的javascript写法,不过相对较为复杂,内容如下:


    
    ```javascript
    <script language="javascript" type="text/javascript">
      function addClassName(tag,classname){
       if(!tag.className){
        tag.className=classname;
       }else{
        tag.className+=" "+classname;
       }
      }
    
      function addFirstChild(){
       var olitems=document.getElementsByTagName("ol");
       var ulitems=document.getElementsByTagName("ul");
    
       for(var i=0;i<olitems.length;i++){
        addClassName(olitems[i].getElementsByTagName("li")["0"],"first-child");
       }
       for(var i=0;i<ulitems.length;i++){
        addClassName(ulitems[i].getElementsByTagName("li")["0"],"first-child");
       }
      }
      function addLastChild(){
       var olitems=document.getElementsByTagName("ol");
       var ulitems=document.getElementsByTagName("ul");
    
       for(var i=0;i<olitems.length;i++){
        addClassName(olitems[i].getElementsByTagName("li")[olitems[i].children.length-1],"last-child");
       }
       for(var i=0;i<ulitems.length;i++){
        addClassName(ulitems[i].getElementsByTagName("li")[ulitems[i].children.length-1],"last-child");
       }
      }
    
      if(document.all && !window.opera){
       window.onload=addFirstChild;
       window.onload=addLastChild;
      }
     </script>
    ```



如果有兴趣可以尝试,至此,大家也发现实际上用jQuery并不困难,用好就有讲究了,不过最好还是打好js的基础,下次我将介绍另外一个简单的效果,关于用jQuery控制下拉菜单悬浮,我用了一个很笨的嵌套方法,有空我在写一下.今天就写到这里希望大家能有所收获.



* * *



PS: 其实这个例子就是简单介绍了jQuery的两个用法,如果动态脚本支持判断首尾元素的话,其实直接在HTML内写个判断(例如:[phpcms文章列表循环不同样式制作方法](http://www.whidy.net/phpcms-list-with-different-style.html)),给首尾元素加个class="first-tag"和class="last-tag"之类的样式也是不错的选择,实际上现在已经不推荐这样的写法,因为你会发现有很多冗余的小代码,维护十分不方便,这里也就是举一反三,大家视情况来写吧( update: 2014年5月17日 )
