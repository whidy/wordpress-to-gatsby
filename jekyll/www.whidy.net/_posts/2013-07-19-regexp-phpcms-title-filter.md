---
author: whidy
comments: true
date: 2013-07-19 03:01:20+00:00
template: post
link: http://www.whidy.net/regexp-phpcms-title-filter.html
slug: /regexp-phpcms-title-filter
title: 利用MYSQL正则表达式-PHPCMS标题筛选文章
wordpress_id: 1724
category: '开发'
tags:
- 技术
- 网站
---

有时候在用phpcms调用数据的时候,我并不想通过建立栏目或者推荐位等那么多复杂方法来分组一类文章,这类文章并不多,却有共同的特点.例如我们需要归类的文章都有个共同标题部分(或是前缀或是后缀),本文将举个小例子,大家活学活用.

正在表达式这个在计算机语言有着极其重要的作用,那么这次还是用它.先看看下面这段代码:


    
    ```php
    <ul>
      {pc:get  sql="SELECT * FROM v9_news WHERE title regexp binary '^Whidy\\.' ORDER BY id DESC" num="3" return="data"}
      {loop $data $v}
      <li>
        <a href="{$v['url']}"><img src="{thumb($v[thumb],306,110)}" alt="{$v['title']}"  width="306" height="110" /></a>
        <h3><a href="{$v['url']}">{str_cut($v['title'],88)}</a></h3>
      </li>
      {/loop}
      {/pc}
    </ul>
    ```



这里重点看的是第二行高亮部分中的**title regexp binary '^Whidy\\.'**,我解释一下获取该表中字段为title的数据,数据中需要严格(binary区分大小写)满足正则表达式(regexp)开头为Whidy后面字符无限制的文章.

那么举例可得到的结果可能是



	
  * Whidy的生活

	
  * Whidy's love

	
  * ...


而同样举例以下不可获取

	
  * whidy摄影集(大小写不符)

	
  * 爱Whidy,爱生活(非Whidy开头)

	
  * ...


大概就是这样的.同样我找了官方的文档大家可参考学习一下:[MySQL正则表达式](http://dev.mysql.com/doc/refman/5.1/zh/regexp.html)

好了,恐怕这也是我最后一片关于PHPCMS的文章了,即将离职了,对于这块也不知道会不会更新了,不过希望以后还能写一些实用更深度的文章分享给大家.
