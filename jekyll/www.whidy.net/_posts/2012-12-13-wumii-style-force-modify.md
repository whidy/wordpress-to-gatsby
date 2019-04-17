---
author: whidy
comments: true
date: 2012-12-13 07:22:04+00:00
layout: post
link: http://www.whidy.net/wumii-style-force-modify.html
slug: wumii-style-force-modify
title: wumii相关文章插件样式暴力修改
wordpress_id: 1475
categories:
- IT技术
- jQuery
- Phpcms
tags:
- 技术
- 网站
---

话说无觅的一个相关文章的插件好像的确能够带来很多流量,如此来说不愧是个好插件,但是,这个插件内置到了PHPCMS的show.html模板中后,那效果简直惨不忍睹,我经过大量研究测试修改,终于让这个插件展示效果变得美观,而这种通过js修改的方式是不是很友好的,先来看看效果图:

[caption id="attachment_1476" align="aligncenter" width="400"][![wumii插件修改效果预览](http://www.whidy.net/wp-content/uploads/2012/12/killWumii-400x294.jpg)](http://www.whidy.net/wp-content/uploads/2012/12/killWumii.jpg) wumii插件修改效果预览[/caption]

<!-- more -->自我感觉这个修改后的效果改变应该还是相当大的,之前的间距,边框什么的简直是一团糟..那么究竟怎么样才能改变默认样式呢?并不是在自己网站上写个CSS就能搞定的!下面我细细说来...

首先,这个wumii插件是通过JS调用的,因为安装此插件的人不是我,所以我在写这个的时候可能有些地方有些漏洞,望谅解.费尽周折找到装插件的人要倒了无觅插件的账号,看了看效果的设置选项,那就是少得可怜.完全不能达到我们想要的效果.于是只能通过自己网站内部来变更,而更让人抓狂的是,wumii的插件竟然不掉用外部CSS.将每个CSS全部写到元素内部,更要命的是,竟然有的还加了!important...想到修改这个的第一方法就是js,而且要写到末尾,让页面读取完最后读取这个修改样式的js,结果效果并不理想,可能是页面读取数据顺序或者延时了导致有时候有效有时候无效,经过反复研究测试,当把js写在body的onload事件里面可以让页面最后读取这个js...这下问题迎刃而解,利用写了个killWumii方法,加载到body内...具体见代码:



  
  1. body里加个onload="killwumii()"就成了


    
    ```javascript
    <body onload="killwumii()">
    ```





  
  2. 添加一段js,我还是写在末尾了


    
    ```javascript
    <script type="text/javascript">
    function killwumii() {
    $(".wumii-image-block").attr({ style: "border:none;display: block;float: left;text-decoration: initial;border-bottom-style:none;cursor: pointer;position: relative;padding: 10px;width: 126px;text-align: left;outline: none;background-image: none;"});
    $(".wumii-image").attr({ style: "padding:1px;border: 1px solid #CCC;background-image: none;visibility: visible;padding: 1px;width: 120px;height: 120px;clip: rect(0px 120px 120px 0px);"});
    $(".wumii-internal").next().remove();
    $("#wumiiBtnDiv").remove();
    $(".wumii-image-border").remove();
    }
    </script>
    ```





  
  3. 因为有几个经常变动的css我还是写到了外部CSS样式里..不过加了!important...


    
    ```css
    /* wumii 稀烂插件 */
    .wumii-related-items-div {padding:0 20px !important;}
    .wumii-image-row {height:200px!important;}
    .wumii-image-title {color:#888 !important;}
    .wumii-widget-title {padding:20px 0 5px 10px !important;}
    ```






好了,就这样,问题解决,效果如图,讨厌的无觅2字去掉了...图片也对齐了...其实我不懂为什么wumii插件的开发者要把边框弄个绝对定位来做,,还有各种结构我不懂.明明有更好的方法..算了,改成自己喜欢的就行了.

PS: 现在回头来看其实给js加个window.onload就可以了,没有必要在body上面加事件,另外,这其实是简单的dom操作,也没啥意思了.(2014年5月23日)
