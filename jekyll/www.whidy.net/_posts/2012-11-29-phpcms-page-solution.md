---
author: whidy
comments: true
date: 2012-11-29 05:46:30+00:00
layout: post
link: http://www.whidy.net/phpcms-page-solution.html
slug: phpcms-page-solution
title: phpcms单页面模板获取栏目数据翻页无效解决办法
wordpress_id: 1144
categories:
- IT技术
- Javascript
- jQuery
- Phpcms
tags:
- 技术
- 网站
---

不得不说有时候为了做一些很奇特的页面,或者说为了解决一些很蛋疼的功能,我们不得不做一些不正常的工作...比如,我把PHPCMS的单页面模板做成了一个读取某个限定条件类的文章列表.限定条件的字段已经添加到数据库内.编辑器中只要选中它属于哪一类即可,这里不多说.

发表相关思路之前先给大家看看效果,觉得还不错的,那么你可以继续看看 :lol:

![PHPCMS单页面模板列表作弊](/wp-content/uploads/2012/11/moreBtn-400x107.jpg)

那么既然是单页面模板,它就有个问题,这个问题就是,单页面模板内是不能使用翻页的功能的.起初我是不知道的,找了一些资料也没解决.那么我就只有想别的办法了.经过一番思索,我认为,可以仿照腾讯微博看到页面底部,自动无限刷新.那么代码的思路就是:

打开该页面获取指定数目的数据(比如20条) > 跟踪坐标当用户拖到页面底部触发事件(js) > 自动生成一段新的异步获取数据下一批数据的代码并更新当前坐标重新计算 > 循环.

<!-- more -->

但是事实是,我的技术无法达到 :sad:

于是,我又想一个伪效果,通过单击底部的更多来展示更多数据.最后做出来感觉效果还不错.虽然代码方面写的很2...所以,真正值得讨论的东西应该是思想了.先上代码:


    
    ```php
    <div class="hifi_PubArea">
      {pc:get  sql="SELECT * FROM v9_news WHERE nrxs=\'0\' GROUP BY TITLE ORDER BY inputtime DESC" num="500" return="data"}
      {php $num=0}
      {php $sep=20}
        <ul class="hifi_ListPage_MainList">
          {loop $data $r}
          {php $num++}
          <li>
            <div class="Title">
              <div class="LeftTitle">{if time()-$r['inputtime'] <= 24*3600}<img src="{IMG_PATH}hifidiy/hifi010.gif" />{else}{/if}<a href="{$r['url']}" target="_blank">{$r['title']}</a></div>
            </div>
            <div class="Content">
              <div class="DivImg"><a href="{$r['url']}"><img src="{thumb($r['thumb'],165,95)}" alt="{$r['title']}" /></a></div>
              <div class="DivContent">{str_cut($r['description'],262)}[<a href="{$r['url']}">查看全文</a>]
                  {php $keywords = explode(' ',$r['keywords']);}
                  <div class="DivLink">[书签]:
                      {loop $keywords $keyword}
                      <a href="{APP_PATH}{{$r['catid']}-{urlencode($keyword)}.html" class="blue">{$keyword}</a>
                      {/loop}
                  </div>
              </div>
            </div>
          </li>
          {if $num%$sep == 0}
          <div class="readMore" style="clear:both;line-height:30px; height:30px; background-color:#eee;border-bottom:1px #AFAFAF dashed; text-align:center; color:#0651AB; font-weight:bold; cursor:pointer;">查看更多</div>
          <li></li><!-- 这里空一个,因为特效将隐藏下一个li -->
          {/if}
          {/loop}
         <div class="bk"></div>
        </ul>
      {/pc}
    </div>
    <script>
      $(".hifi_ListPage_MainList li").eq(19).nextAll("li").hide();
      $(".hifi_ListPage_MainList li").eq(20).nextAll(".readMore").hide();
      $(".readMore").click(function () {
      $(this).slideUp("slow");
      $(this).nextUntil(".readMore").fadeIn("slow"); 
      $(this).nextUntil(".readMore").next().fadeIn();
      $(".readMore:last").hide();
      });
    </script>
    ```



因为测试,我暂时把相关css写到元素内了.看完后大家带着疑问应该不少,我也简单说明一下.首先,这个是一次性调用了500条数据,这个可以根据个人需求进行调整.并将每20条作为一组数据展示.顺便对查看更多和新的数据展示添加了一点效果:D 每循环一次判断整除余数是否为0,执行判断语句.然后一直到最后数据输出完成.其实这段代码是一次性将500条数据全部读出来了,只看到20篇是因为我用js将其隐藏,每点击一次查看更多自动刷新后面20条.整个过程就是这样.一直"刷新"到所有元素显示完毕...看到这里是不是感到十分坑爹= =!

好吧,关于这个嘛,以后有时间我在研究一下,进行优化.毕竟这个办法不是长久之计.有兴趣的朋友可以参考后根据个人需要进行调整咯.

PS:后来发现BUG, ie 不兼容,正在解决中.

<!-- 最后不得不说我被上一个写模板的程序员击败了- -...只因为这一条写在head里面的代码,我经过无数测试,找出来了
<meta http-equiv="X-UA-Compatible" content="IE=7" />
其实,我上面的这个效果是不兼容IE6和IE7的,这个问题似乎并不是很大了.有空我还会解决下,当然因为这短短的一句导致全部IE都无法正常运作,最后删除了这一句一切完美.此文至此就算是结束了.在调试这个问题的时候将这个效果精简了代码,有兴趣的同学可以去看看-[利用jQuery点击显示更多元素演示代码](http://www.whidy.net/jq-more-demo.html).毕竟这个代码演示看着有点花呵呵~~~为了展示这个思路嘛.
