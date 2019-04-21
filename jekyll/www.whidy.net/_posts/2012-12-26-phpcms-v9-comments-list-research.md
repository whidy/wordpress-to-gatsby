---
author: whidy
comments: true
date: 2012-12-26 02:05:49+00:00
template: post
draft: false
link: http://www.whidy.net/phpcms-v9-comments-list-research.html
slug: /phpcms-v9-comments-list-research
title: 关于PHPCMS V9显示评论数排行列表小研究
wordpress_id: 1519
category: '开发'
tags:
- 技术
- 网站
---

也不知道公司网站上的评论排行列表怎么写的,无奈不想做大的改动.先不谈调用数据,就说这个HTML和CSS还有调用数据的方式,,,不禁汗颜,有兴趣的可以研究下,先把这个原始的放出来大家看一下.


    
    ```php
    <ul class="hifi_List2">
      {php $i=0}
        {pc:comment action="bang" siteid="$siteid" num="1000"}
          {loop $data $b}
            {php $str=ltrim($b['commentid'],'content_'); $end=stripos($str,"-"); $cid=substr($str,0,$end);}
            {if $cid==$catid}
              {php $i++;}
              {if $i<=1}
                <li class="f">
                  {php $str=rtrim($b['commentid'],'-1'); $start=stripos($str,"-")+1; $aid=substr($str,$start)}
                  {php $db = pc_base::load_model('content_model'); $t = $db->get_one(array('id'=>$aid))}
                  <div class="tit"><a href="{$b['url']}">{$b['title']}</a></div>
                  <div class="fImg"><a href="{$b['url']}"><img src="{thumb($t['thumb'],80,55)}" alt="{$b['title']}" width="80" height="55" /></a></div>
                  <div class="fCon">{str_cut($t['description'],112)}[<a href="{$b['url']}">查看全文</a>]<br/><span class="fr hits">{$b['total']}</span></div>
                </li>
              {else}
                <?php if($i>15)break;?>
                <li class="li"><a href="{$b['url']}">{str_cut($b['title'],56)}</a><span class="hits">{$b['total']}</span></li>
              {/if}
            {/if}
          {/loop}
        {/pc}
      <div class="bk"></div>
    </ul>
    ```



<!-- more -->

一次性调用1000条判断到15跳出?不知道这样到底读了1000条没,还有li元素给.li样式的?反正这个我都准备作废了,就不管了,但是调用评论数并关联排行等方法比较复杂,苦逼百度..找到这样一文[<<phpcms v9 实现调用指定栏目下按评论数排序的新闻列表>>](http://blog.feshine.net/technology/767.html),在此感谢作者贡献,好像很好用的样子,不过样式比较简陋,我就进行了部分修改.先看我的改后的(基于原作者第一个,调用指定ID):


    
    ```html
    <ul class="hifi_List2">
      {pc:get sql="select * from phpcms_comment where commentid like 'content_$catid%' order by total desc" num="15" return="data"}
        {loop $data $b}
        <li class="li"><a href="{$b[url]}" title="{$b[title]}">{str_cut($b[title],60,'')}</a><span class="fr hits">{$b['total']}</span></li>
        {/loop}
      {/pc}
    </ul>
    ```



说明区别:



  
  1. 原作者的调用是死的,其实这里改成栏目ID变量是可以的,正如我这个**content_$catid%**

  
  2. 修改调用数量15条而不是row

  
  3. 增加评论数的数量显示**{$b['total']}**


这样就基本OK了.
