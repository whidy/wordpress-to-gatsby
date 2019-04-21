---
author: whidy
comments: true
date: 2013-10-17 15:12:00+00:00
template: post
draft: false
link: http://www.whidy.net/chrome-codecademy-font-size-10px.html
slug: /chrome-codecademy-font-size-10px
title: Chrome无法正确显示小于12px的问题思考解决
wordpress_id: 1784
category: '开发'
tags:
- 技术
- 网站
---

很多东西都是有时效性的啦...正巧我又遇到一个设计做的10px汉字,来翻以前写的东西,实际上发现这个还是有作用的,给需要设置10px的标签加上这个就ok啦,至少chrome 39是OK的啦~

    
    ```css
    -webkit-text-size-adjust:none;font-size:10px;
    ```


ps: 2015年1月23日



* * *



想必很多计算机自学者都在CodeCademy学习过,作为入门学习的免费网站,的确做得不错,这几天闲来无事本来是想在上面学点别的,看到有HTML教程顺便也想快速通过,却发现在控制字体大小卡壳了.一般来说我使用chrome浏览器,其中有一个小的CodeCademy的练习,要求设定字体大小10px,chrome始终无法通过,不过似乎之前遇到过这个问题,所以思考了片刻解决了.首先看图,通过不同浏览器运行此练习效果:

![chrome和ie下的区别](https://www.whidy.net/wp-content/uploads/2013/10/CodeCademy-400x202.jpg)

<!-- more -->

那么为什么chrome不通过,而IE是可以通过呢,当然还有其他浏览器我没有进行测试,因为作为这个问题,不必对多个浏览器进行检测.

如果没有经验的人,肯定绞尽脑汁都想不出来,或许能想到沾点边的原因,比如说是不是chrome的默认字体跟IE是不一样的呢,chrome默认字体恰好不支持10px大小的字体导致呢?那么我们可以尝试做个测试,在p标签的样式内添加一句**font-family:Arial;**我想这样应该没问题了吧,提交发现仍然无法通过.

其实,告诉大家,这是由于chrome浏览器本身问题导致.那么如何解决这个问题呢?相信大家一定会搜百度,其实我也是这样做的,但是似乎搜出来的结果都是说这样一个方法.添加一条样式,只有chrome才能识别的:

    
    html,body {-webkit-text-size-adjust:none;}


似乎我用了这个不管用,也不知道是几年前的方法了.那怎么办还是找google靠谱些吧.于是找到这篇文章[Font-size <12px doesn't have effect in Google Chrome](http://stackoverflow.com/questions/2295095/font-size-12px-doesnt-have-effect-in-google-chrome)有个人的回复大家可以自己看看,我尝试了一下,还是有一些问题.具体是修改一个选项文件内容如下:

    
    ```json
    "webkit": {
          "webprefs": {
             "default_fixed_font_size": 11,
             "default_font_size": 12,
             "fixed_font_family": "Bitstream Vera Sans Mono",
             "minimum_font_size": 12,
             "minimum_logical_font_size": 12,
             "sansserif_font_family": "Times New Roman",
             "serif_font_family": "Arial",
             "standard_font_is_serif": false,
             "text_areas_are_resizable": true
          }
      	}
    ```


但是似乎这个是适应国外英文网站的,我经过无数次的调试测验,终于可以正常使用了,在不影响中文文字大小的情况下,最小的设置为8px,我想应该没有什么网站会设置更小的字体了吧.那么我是这样改得:

    
    ```json
    "webkit": {
          "webprefs": {
             "uses_universal_detector": true,
             "minimum_font_size": 8,
             "standard_font_is_serif": false,
             "text_areas_are_resizable": true
          }
      	}
    ```


大家可以试试,目前来说是可以在chrome 30的版本下正常使用的, 好像说了半天没有说是修改那个文件,其实就是chrome安装目录里,以我的电脑(WIN 8.1)举例:
**C:\Users\Whidy\AppData\Local\Google\Chrome\User Data\Default\Preferences**
修改**Preferences**文件,末尾处即可.(其他系统自行查找此文件咯~)

虽然这个问题解决了,但是实际上还有个IE下却有些不同,如图

![不同浏览器字体显示效果](https://www.whidy.net/wp-content/uploads/2013/10/fontsize-400x274.jpg)

IE的确还是很奇怪...那么这个问题下次来研究下,不早了,要睡觉了...(哈哈,逗大家玩的,其实我缩放了百分比的...)

相关阅读: **[默认css字体大小单位及样式研究](http://www.whidy.net/wp-admin/post.php?post=748&action=edit)**
