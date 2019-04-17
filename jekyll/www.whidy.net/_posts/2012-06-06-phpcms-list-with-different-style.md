---
author: whidy
comments: true
date: 2012-06-06 08:51:33+00:00
layout: post
link: http://www.whidy.net/phpcms-list-with-different-style.html
slug: phpcms-list-with-different-style
title: phpcms文章列表循环不同样式制作方法
wordpress_id: 797
categories:
- IT技术
- Phpcms
- 技术分享
tags:
- 技术
- 网站
---

大家在用PHPCMS系统做网站的时候,有时候在列表循环可能希望用到不同的布局格式,而并不希望在整个列表中做好几个pc标签配合不同的start参数的时候,你可以试试我这个方法.

先来看看效果图:

![phpcms文章列表循环不同样式制作方法](/wp-content/uploads/2012/06/phpcms-400x248.jpg)

那么我这张图清晰的告诉大家,这个列表分为三个部分,而我将采用两个PC标签完成它(之所以用两个PC标签输出,目的在于温习[phpcms嵌套循环](/phpcms-speciallist-with-subarticle-loop.html)内容输出,当然你完全可以通过我的方法用一个PC标签搞定),因为CSS样式已经做好,这里大家只用看程序部分即可,先上代码部分:


    
    ```html
    <div class="hifi_PubArea">
      <div class="MainTitle">
        <div class="classTitle">
          <div><a href="{APP_PATH}cydiy/">创意DIY&nbsp;</a></div>
        </div>
        <div class="fr Blue_List_A"><a href="{APP_PATH}cydiy/" class="block_more"></a></div>
      </div>
      {pc:content action="lists" catid="40" order="id DESC" num="5" return="data"}
      <ul class="video_MainList">
        {php $num=0}
        {loop $data $r}
        {php $num++}
        {if $num==1}
        <li class="classMain">
        <a href="{$r[url]}"><img src="{$r[thumb]}" /></a>
        <h3><a href="{$r[url]}">{$r[title]}</a></h3>
        <p class="videoDpt">{$r[description]}</p>
        <p>栏目：<span>{$CATEGORYS[$r[catid]][catname]}</span></p>
        {php $keywords = explode(' ',$r['keywords']);}
        <p>书签：<span>{loop $keywords $keyword}<a href="{APP_PATH}{$r['catid']}-{urlencode($keyword)}.html" class="keywords">{$keyword}</a>{/loop}</span></p>
        <p>发布时间：<span>({date('Y-m-d',$r[inputtime])})</span></p>
        <div class="videoPart3">
          {pc:content action="lists" catid="40" order="id DESC" num="4" start="5" return="data"}
          <ul>
            {loop $data $v}
            <li><h4><a href="{$v[url]}">{str_cut($v[title],54,'...')}</a></h4></li>
            {/loop}
          </ul>
          {/pc}
        </div>
        <div class="clear"></div>
        </li>
        {/if}
        {if $num>=2}
        {php $num++}
        <li class="videoPart2">
        <a href="{$r[url]}"><img src="{$r[thumb]}" /></a>
        <h4><a href="{$r[url]}">{$r[title]}</a></h4>
        <p>栏目：<span>{$CATEGORYS[$r[catid]][catname]}</span></p>
        {php $keywords = explode(' ',$r['keywords']);}
        <p>书签：<span>{loop $keywords $keyword}<a href="{APP_PATH}{$r['catid']}-{urlencode($keyword)}.html" class="keywords">{$keyword}</a>{/loop}</span></p>
        </li>
        {/loop}
        {/if}
      </ul>
      {/pc}
    </div>
    ```



看不懂?好吧,我简单说明一下,其中图片中的**Part1**和**Part2**其实就是第一个PC标签所循环的内容,而循环出来的5篇文章,其中第一篇和后面四篇是不同的,那么,这里有个判断语句,给$num初始值定义为0,随着循环自增,当**$num==1**是输出第一个很特殊的结构样式,然后当**$num>=2**时,则开始输出剩余的4篇文章,**Part3**则穿插在Part1内,当然我有用了一个PC标签调用文章,这里就要增加一句**start="5"**了,当然如果你不想用PC标签,其实可以用Part2同样的方法来做,当然不要忘记在第8行内的num改成**9**,因为此栏目一共有9篇文章,那么就呈现了一个PC标签循环列表中可以采用三种不同的样式结构了.

其实这段代码理解起来也没有什么难度,基本上是基本语法,希望大家看了之后有所收获能够在其他所需要的地方活学活用.
