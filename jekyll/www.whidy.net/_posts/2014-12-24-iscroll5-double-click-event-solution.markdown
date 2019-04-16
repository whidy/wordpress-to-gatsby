---
author: whidy
comments: true
date: 2014-12-24 15:27:42+00:00
excerpt: 前阵子做WAP端的项目,用到了iScroll插件,结果发现有很多问题,起初并未用多个设备进行测试,以为并没有什么问题,结果进入项目尾声进行测试的时候,竟被这个插件折腾了好几天简直让人抓狂.
layout: post
link: http://www.whidy.net/iscroll5-double-click-event-solution.html
slug: iscroll5-double-click-event-solution
title: IScroll的click单击事件变为双击多次触发解决
wordpress_id: 2628
categories:
- IT技术
- Javascript
tags:
- 技术
- 教程
- 网站
---

前阵子做WAP端的项目,用到了iScroll插件,结果发现有很多问题,起初并未用多个设备进行测试,以为并没有什么问题,结果进入项目尾声进行测试的时候,竟被这个插件折腾了好几天简直让人抓狂.其间收集了一些资料,但是苦于项目上线后一直都比较忙,也就没有什么时间总结这个iscroll插件的一些问题,距离项目上线已经有了半个月了,我下文写的不好还请见谅.

首先iscroll是为了让wap端页面的的某个层内能够固定滚动而特别制作的,我起初想这个东西使用好像还是比较广泛的,问题应该不多吧.之前同事也有使用过,不过基本上使用的是简单的功能,而我这次进行的更多是复杂的交互效果,因此,让我纠结了很久的就是android手机在不同系统版本上,在不同浏览器上以及不同系统版本和不同版本浏览器这三种情况都可能发生各种问题.

参考资料:

https://github.com/cubiq/iscroll/issues/674

https://github.com/cubiq/iscroll/issues/547



* * *



以上内容是一个月前写的...我已记不清了,大概是处理不同设备的click事件遇到了很多问题,,,这篇文章放在草稿箱许久了,是时候终结了!

这个iscroll插件的确有很多需要注意的地方,仔细阅读了文档重要部分好几遍,结果写的代码还是问题很多,本文就iscroll使用上的一些问题总结一下与大家分享分享.

我们先来看一个[demo](http://www.whidy.net/demos/IScrollDemo/index_b.html)(从项目中提出可能有部分冗余代码),主要用于分类选择,菜单弹出功能,(实际应用效果见太平洋电脑网手机端[产品库页面](http://g.pconline.com.cn/product/mobile/),当然后期可能改版,实际效果与demo略有差异)如,用到zepto库,iscroll插件.其中iscroll主要是处理固定高度的滑动效果,它能够自适应并兼容很多设备,所以我选择了插件.

当然每个可以上下滑动的区域都需要创建一个IScroll实例,只需要简单的一句话即可,但是要遵守它的HTML代码结构,详细可以参考官方文档.这里就不讲基本的使用方法了,底部有资料写的很清楚了.我就简要说一下关于这个DEMO中的注意事项.

首先是这是一个带有弹出层的页面,每次点击导航会有一个向下滚出的层,那么弹出后就会创建对应的一个或两个iscroll实例,当点击顶部收回的时候,容易忽略一点,刚创建的实例依然存在,假设收回不销毁新建的实例,就会出问题!

其次,iscroll内的的click事件处理,默认是false,这在ios系统的手机上会出现click执行两次,也就无效的情况,需要改成true,所以需要对创建的示例增加参数.但是问题在于兼容了ios后,android各个版本会出现同样的问题.解决方案,对不同的安卓设备采取不同的click属性值处理,但是经过大量机器测试,依然可能出现无法兼容的情况(实际上是通过一个正则处理的,见代码)

    
    <code class="js">function iScrollClick(){ //设备识别来控制iscroll的click真假
        if (/iPhone|iPad|iPod|Macintosh/i.test(UA)) return true;
        if (/Chrome/i.test(UA)) return (/Android/i.test(UA));
        if (/Silk/i.test(UA)) return false;
        if (/Android/i.test(UA)) {
            var s = UA.match(/Android [\d+.]{1,5}/)[0].replace('Android ','');
            return parseFloat(s[0]+s[2]+s[4]) <= 442 && parseFloat(s[0]+s[2]+s[4]) > 430 ? true : false;
        } //测试大量机器总结的规律,可能会有极小部分机器在选择功能上依然出现问题
    }</code>


其实官方文档中有一个options.preventDefault的属性可以配置,但是不知道是哪里出了问题,经过反复测试都没起到作用.于是这个问题折腾了很久...直到有一天...

虽然早起处理这个问题的时候就知道有fastclick,或许可以解决,但是又是一个插件,毕竟一个项目中用太多的插件不好,所以未采纳,前几天研究移动端的touch事件和普通的pc端click等事件时,更清楚的明白了一些东西,例如事件冒泡等...反复琢磨测试,觉得fastclick或许也是可行的,既然之前的方案不够完美,不妨试试这个[demo](http://www.whidy.net/demos/IScrollDemo/index_a.html),去掉了iscroll对click的配置(即默认都是false),并添加了fastclick插件及全局配置后,测试了很多机器,发现,并未出现问题.那么目前来看针对iscroll出现的双击,穿透,或是点击延时等问题应该全部处理好了!

毕竟这个内容过去太久,凭借回忆来写的,可能有些混乱,建议有遇到类似问题的朋友仔细看看两个demo的区别,一个是[正则处理iscroll的click属性的demo](http://www.whidy.net/demos/IScrollDemo/index_b.html),一个是用[fastclick插件的iscroll demo](http://www.whidy.net/demos/IScrollDemo/index_a.html),只需要注意两个demo的js的区别即可!

最后附上相关参考资料:

官方资料: [IScroll官方网站](http://iscrolljs.com/) [IScroll PDF参考手册](http://iscrolljs.com/iscroll-doc.pdf) [IScroll Github](https://github.com/cubiq/iscroll/)

其他: [iScroll 5 API 中文版](http://iiunknown.gitbooks.io/iscroll-5-api-cn/)



* * *



后来发现,原来这不是万金油,总会有些坑爹的情况.比如魅族原生浏览器,还有chrome...竟然也会出问题,太失望了.

也就是说,在魅族原生浏览器下,需要设置为click : true才能正常运作,魅族原生浏览器如果false则会出现两次点击,而产生意外情况.而chrome则是当false时,整个iscroll容器内的事件全部被阻止了..没有办法只得打补丁了.于是加了以下代码...

    
    <code class="js">var clickBoolean = false;
    if (/Chrome/i.test(UA)) clickBoolean = true;
    if (/534.30/i.test(UA)) {
        if (/UCBrowser/i.test(UA)) clickBoolean = false; //覆盖同版本
        else clickBoolean = true; //魅族原生?
    }</code>


我本来想通过UA标识来区分魅族浏览器,因为我这个写了534.30来区分魅族的方法风险太大因为UC也是这个版本,所以又加了一条如果是uc还是要用false,想在魅族的UA上处理,但是魅族原生浏览器真的很坑,UA上面根本无法下手.只能临时采用下策了.

这几点是需要大家注意的...(2015年2月2日18:54:00)
