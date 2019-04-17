---
author: whidy
comments: true
date: 2014-11-13 15:13:23+00:00
layout: post
link: http://www.whidy.net/css-css3-selector-summary.html
slug: css-css3-selector-summary
title: 是时候总结一下常用css选择器(包含CSS3)
wordpress_id: 2608
categories:
- IT技术
---

发觉CSS选择器用的实在是太平凡了...一直犹豫国内大量使用IE,致使很多初级前端开发人员对于很多CSS3的选择器比较陌生,这里我参考各方的文档及相关经验来总结一下CSS选择器的相关知识.


### CSS 2.1 选择器:




#### 通配符选择器


匹配任意元素,不建议使用,除非做DEMO测试之类


#### 类型选择符


一般来说就是常用的html标签 (_div_ , _p_ , _a_)


#### 后代选择符


选择所有被XX包含的xxx (_div a_ , _ul li_)


#### 子代选择符


选择XX元素子级第一级的元素xxx,切记是第一级 (div > p)


#### 相邻选择符


同级两个元素中第二个元素生效比如: XX和xx同级且相邻,那么XX + xx中的xx样式生效,看糊涂了吗哈哈哈(_h1 + p_)

<!-- more -->


#### 伪类和伪元素选择符


包括:link, :visited, :hover, :focus, :active, :first-child, :lang(), 其实一般也就用到a标签的hover,偶尔为了提高用户体验加个a的visited~再就是除了IE兼容较差的first-child了


#### 类选择符


就是class里面的xx没什么好说的了吧 (_.xx_ , _.xxx_ , _.header_)


#### ID选择符


同类选择符格式用id,优先级不同罢了,一般来说除非特别重要的会用来写进样式,不建议使用.( _#xx_ , _#xxx_ , _#page_)


#### 属性选择符


这个CSS2的比较简单,只有几种写法,我就不一一列举了


### CSS 3 选择器:




#### Following-sibling combinator


不知道怎么翻译,就是 XX ~ xx, XX和xx同级,且xx在XX后面的全都有效


#### 属性选择符


CSS3版的这个花招太多了...我懒得写简单说就是含有某个属性的标签才拥有的样式,自己去查下面的分享资料啦~(_a[title]_ , _img[alt]_)


#### nth-child


这有很多写法...

还有些应用于表单的**:enabled**, **:checked**...由于时间关系就不都写详细用法了.

作为活雷锋的人物,一次又一次把流量引走了.我不后悔,请看W3CSCHOOL的表格,[CSS 选择器参考手册](http://www.w3school.com.cn/cssref/css_selectors.asp)

一般支持css3的浏览器中,对于css2.1里的属性选择器兼容比较好,可以尝试了解一下,对于做页面帮助很大.我随便举几个例子:

a[href$=".pdf"] (选择a元素中href属性值内带有.pdf并以此结尾的标签)

img[alt^="figure"] (选择img元素内含有alt属性,并以figure开始的标签)

还有很多,其实跟正则写法有一定关系.大家自行研究

最后关于各个版本的选择器兼容性,可以看下面分享第三条.也就是说,并不是IE6,7,8不支持CSS3就完了,甚至连CSS2很多都支持不好,例如first-child这种,我这里就不多说了.

最后分享几个好东西,从第一个开始逐步增加难度...若是入门当然看第一条就够了,简单清晰



	
  1. [CSS 教程](http://www.w3school.com.cn/css/index.asp)

	
  2. 来自[smashingmagazine](http://www.smashingmagazine.com/2009/07/13/css-3-cheat-sheet-pdf/)的**[CSS3 Cheat Sheet (PDF)](http://coding.smashingmagazine.com/wp-content/uploads/images/css3-cheat-sheet/css3-cheat-sheet.pdf)**和**[CSS3 Quick Reference Guide (GIF)](http://coding.smashingmagazine.com/wp-content/uploads/images/css3-cheat-sheet/preview.gif)**

	
  3. CSS选择器兼容性表[**电脑终端**](http://quirksmode.org/css/selectors/)和[**移动终端**](http://quirksmode.org/css/selectors/mobile.html)

	
  4. [css2速查表](http://www.cheatography.com/davechild/cheat-sheets/css2/)

	
  5. [入门版30个需要牢记的CSS选择器](http://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048)

	
  6. [W3C官方CSS2.1选择器文档](http://www.w3.org/TR/CSS21/selector.html)

	
  7. 高级文档[Selectors Level 4](http://dev.w3.org/csswg/selectors4/)


好了,暂时就分享这么些东西了.更多的还是要熟练使用,多多记忆才好.

本来想写一个超级无敌完整的,发现完全没精力,就写这点东西花了2个多小时,眨眼便是晚上11点多了.不行要休息了.大家多多看我的分享好了~
