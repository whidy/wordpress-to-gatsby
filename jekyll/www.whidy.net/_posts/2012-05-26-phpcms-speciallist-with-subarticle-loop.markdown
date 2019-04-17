---
author: whidy
comments: true
date: 2012-05-26 03:28:35+00:00
layout: post
link: http://www.whidy.net/phpcms-speciallist-with-subarticle-loop.html
slug: phpcms-speciallist-with-subarticle-loop
title: PHPCMS页面专题汇总列表内调用该专题内文章方法
wordpress_id: 782
categories:
- IT技术
- Phpcms
- 技术分享
tags:
- 技术
- 网站
---

好吧,由于工作需求,外加自己过分追求完美,晚上研究了一下,PHPCMS专题总列表页内的某个专题含有该专题的几篇文章的方式,其实原理很简单,核心思想是
1.嵌套循环.
2.数据库中存储总列表内某专题的id值等于该专题某文章列表的id值.



* * *



昨晚其实最后效果还有点问题,今天上午一上班继续解决,终于弄好了,现在跟大家分享心得.

前文可能这样说大家看不大明白,我先截取两张图片给大家看:

[![PHPCMS页面专题汇总列表内调用该专题内文章方法](/wp-content/uploads/2012/05/20120525previews1.jpg)](/wp-content/uploads/2012/05/20120525previews1.jpg)

**想实现的效果:**通俗点讲就是假设你后台有5个专题,而且这5个专题内有若干篇相关文章,你希望这个专题列表页面不单单显示出这5个专题信息,在列表中每个单独的专题区域能够显示该专题下的文章.

**实现原理:**很显然从逻辑上来讲就是一个嵌套循环,大循环,循环的是有多少个专题,挨个输出,而在每个已经输出的专题中,再次运行一次小循环,来循环当前专题内的所有文章.

**准备工作:**当然理解了原理,有了思想之后,就好办了,先看看PHPCMS V9专题管理的数据库表.这里有两个表"**v9_special**"和"**v9_special_content**",一看就知道了,前者是管理有多少个专题的,后者是存放这些专题的所有内容的.而两个表如何关联起来,由于我数据库和php学的都不好(大家都知道我之前做网页设计和前端的--!),所以代码也许略有不合理的地方.我之前尝试用系统默认的PC标签"**pc:special**"来写,但是未能实现,于是只好用我认为最暴力的方式,直接读取数据库的"**pc:get sql=' '**",接着观察两个表的字段.他们功能连接的方式是**v9_special**的**id**和**v9_special_content**的**specialid**.那么再循环过程中将这两个值关联起来就可以了.

**实现方法:**由于这个站展示在公司网站上了,所以就不写CSS出来了,大家只需要理解了,可以自己想怎么用就怎么用.我的代码是这样写的:


    ```php
    <div class="hifi_PubArea">
      <!--嵌套循环输出专题及专题内文章By小白-->
      {pc:get sql="SELECT * FROM v9_special ORDER BY createtime DESC" num="10" return="data"}
      <ul class="hifi_ListPage_MainList">
        {loop $data $r}
        {php $sid=$r['id']}
        <li>
          <div class="Title">
            <div class="LeftTitle">{if time()-$r['createtime'] <= 24*3600}<img src="{IMG_PATH}hifidiy/hifi010.gif" />{else}{/if}<a href="{$r['url']}">{$r['title']}</a><span>[<a href="{$CATEGORYS[$catid]['url']}">{$catname}</a>]</span></div>
            <div class="RightTitle"> <span class="author">{if $r['username']}{$r['username']}{else}hifidiy{/if}</span> </div>
          </div>
          <div class="Content">
            <div class="DivImg"><a href="{$r['url']}"><img src="{thumb($r['thumb'],165,95)}" alt="{$r['thumb']}" /></a></div>
            <div class="DivContent">{str_cut($r['description'],240)}[<a href="{$r['url']}">查看</a>]
              <div class="subArticle">
                {pc:get sql="SELECT * FROM v9_special_content WHERE specialid = '$sid'  ORDER BY updatetime ASC" num="4" return="data"}
                <ul>
                  {loop $data $t}
                  <li><a href="{$t['url']}">{$t['title']}</a></li>
                  {/loop}
                </ul>
                {/pc}
              </div>
            </div>
          </div>
        </li>
        {/loop}
        <div class="bk"></div>
      </ul>
      <div id="pages">{$pages}</div>
      {/pc}
    </div>
    ```



关键部位我已经做了高亮,方便大家查看.我顺便简单讲解一下, 第一行高亮表示从v9_special表获取所有字段内容,当然里面有个**id**字段的所有值也获取了,接下来将这个值赋值给**sid**,那么在第一个循环内,$sid==id,并继续执行下个循环(第二条高亮部分),从v9_special_content内获取所有字段的内容,当然这里加了个条件因为这个表内包含了不止一个专题的文章,因此我将条件设定为specialid==$sid,这样就不会出现文章调用问题了.至于数量顺序什么的就很简单了,这里不再熬述.

好了,其实写完这篇文章想想,好像很简单的一个自定义功能,但是为什么昨天晚上做了半天效果出不来呢,呵呵,还是编程语言基础不扎实,还得努力啊!
