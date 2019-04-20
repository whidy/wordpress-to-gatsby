---
author: whidy
comments: true
date: 2012-06-29 02:50:49+00:00
template: post
link: http://www.whidy.net/phpcms-data-website-to-website.html
slug: /phpcms-data-website-to-website
title: PHPCMS利用数据源对网站数据调用至其他网站方法
wordpress_id: 840
category: '开发'
tags:
- 技术
- 网站
---

话说,我工作上有个需要,公司论坛上想加个小区域,放一些公司的门户站的最新的新闻等等内容,问怎么解决?

情况: 两个站h.net(PHPCMS V9)是门户站b.net(DISCUZ 7.2)是论坛,当然这两个站都是拥有后台管理权限的!那么b.net有一个区域要放h.net的文章列表,OK,最初我以为是整合两个站,让其关联数据库.其实这个办法是错误的,对于PHPCMS V9这个系统来说,其实有个更好的解决办法,适合初级菜鸟使用,详细操作办法如下:

进入h.net后台,找到 **模块 > 模块管理 > 数据源 > 添加数据源调用** 弹出一个窗口

![数据源未填写](/wp-content/uploads/2012/06/datasource01-400x360.jpg)

这些选项大家应该看得懂吧,我简单说明一下,

1.先看数据源调用配置区,**调用方式**中模型配置其实就是大家常用的PC标签调用方式,而自定义SQL也就是get sql方式调用的,这里建议新手选择**模型配置**.**选择模型**下拉菜单,这个就更不用说了,一般我们如果调用栏目内文章列表,则选择**内容模块**,接下来选择**列表**,则出现一些关于调用范围的选项和条件,大家根据自己需要添加,其中值得说明的是,**调用附表**建议勾上.这个跟字段的是否为主键有关,此处不进行详细说明.

2.公共配置区域,**名称**可以随便写了,只要你自己看得懂,**输出方式**,这个比较复杂,如果对动态脚本不熟悉的同学,我建议使用**js**,我今天也已js为例给大家说一下,选中js后,弹出**选择模板**,这里我分享一下我得模板,


    
    ```html
    <h3>最新行业动态</h3>
    {loop $data $k $v}
        <li>· <a href="{$v[url]}">{$v[title]}</a></li>
    {/loop}
    ```



![数据源填好后](/wp-content/uploads/2012/06/datasource01-400x360.jpg)

其实跟普通的文章调用方式写的模板相同,缓存时间一般为0,数量自己决定,最后确定,于是就生成了一段代码.接下来我们将在论坛上放置此js代码.

打开论坛系统安装目录的模板目录,一般在安装根目录下的templates文件夹内的某个模板文件夹,我这里修改的是**discuz.htm**文件,此段代码我插入到


    
    ```html
    <!--{else}-->
    <div id="ad_text"></div>
    <!--{/if}-->
    ```



我进行简单修改如下:


    
    ```html
    <div id="ad_text"></div>
    <!--{/if}-->
    <style>
    .linkBox {
      padding-bottom: 10px;
      height:100px;
      width:98%;
      border: 0px solid #6595D6;
      background-color: #E6F6E6;
      clear: both;
      margin:10px auto;
    }
    .linkBox ul {
      float:left;
      text-align:left;
      width:32%;
    }
    .linkBox ul h3 {
      margin-left:10px;
    }
    </style>
    <div class="linkBox">
      <ul>
        <script type="text/javascript" src="http://h.net/index.php?m=dbsource&c=call&a=get&id=1"></script>
      </ul>
      <ul>
        <script type="text/javascript" src="http://h.net/index.php?m=dbsource&c=call&a=get&id=1"></script>
      </ul>
      <ul>
        <script type="text/javascript" src="http://h.net/index.php?m=dbsource&c=call&a=get&id=1"></script>
      </ul>
    </div>
    ```



我这是样本,所以重复三块.仅供大家参考用.最终效果图

![最终效果图](/wp-content/uploads/2012/06/previews-400x86.jpg)

对了忘记说了,我这个调用的代码其实调用了两个地方的- -!所以略有不同..z请谅解

PS:其实这个链接效果上虽然成功了,其实还有个小问题...就是链接地址不正确,我后来才发现,又经过半天时间研究,原来是这么个小问题,详情请见[<<PHPCMS数据源功能使用注意事项>>](/phpcms-data-website-to-website.html)
