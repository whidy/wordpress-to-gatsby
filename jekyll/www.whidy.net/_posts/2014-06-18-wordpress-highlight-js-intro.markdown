---
author: whidy
comments: true
date: 2014-06-18 01:09:50+00:00
layout: post
link: http://www.whidy.net/wordpress-highlight-js-intro.html
slug: wordpress-highlight-js-intro
title: wordpress高亮插件Highlight.js手动添加及使用说明
wordpress_id: 2429
categories:
- IT技术
- 技术分享
tags:
- wordpress
- 技术
- 网站
---

使用WORDPRESS已经有很多年了,作为一个以技术内容为主的网站,经常会在文章内引用到各种语法的代码,在wordpress插件管理中,我们同样能够找到很多关于语法高亮的插件,有的十分完美,体积却异常庞大,比如我之前使用的**Crayon Syntax Highlighter**,若果博主们对自己的服务器很有信心,又喜欢强大的配置管理,这款插件实在是省事,可是我总觉过于臃肿,因为很多功能用不到,于是后来我找到了另一个插件**SyntaxHighlighter Evolved**,这款插件相对来讲很简洁,并且它所使用的高亮JS是很多大型网站都在用的,可是不知道为什么我这里看起来感觉怪怪的,并且它使用起来需要用到类似`[html][/html]`的标签,如果一旦放弃使用这个插件,恐怕就杯具了.虽然之前经过慎重考虑,选用了此插件,但是高亮效果感觉并不满意,最终寻找到了或许更好的或说更适合我的"高亮插件"--**Highlight.js**(其实wordpress里面有个_wp-highlight.js_的插件不知道是不是这个js,我没装,只是看了下,其实也是有下文提到的问题的.而且还不精简,所以我就决定手动添加)!

今天我就来简单介绍一下如何使用这个**Highlight.js**(如果喜欢自己琢磨,可以直接访问官方网站[highlight.js](http://highlightjs.org/)查看相关说明)

_当然我也是看了官方文档说明,总结给懒人看的._


## 本地测试




### 一. 准备必要文件


既然是使用它,那必须是需要一个highlight.js了,这个js可以自定义生成,这一点非常适合我,毕竟我只是一个小小小小的前端工作者,我只需要高亮显示html,css,js,json,最多加个php,sql了.于是,在这里,自定义配置这个js--[Custom package](http://highlightjs.org/download/),此处勾上自己需要的,然后点击Download按钮,很快一个zip文件就下载好了.

<!-- more -->


### 二. 配置测试目录


然后,提取压缩包内的"highlight.pack.js"和"styles"目录,放在一个我稍后想要测试的效果的文件夹中,例如testHighlight,并创建一个测试用的index.html,那么该目录内就有index.html,highlight.pack.js和styles目录了,文件准备妥当,进行下一步.


### 三. 调试测试效果


最后,编辑index.html,按照[官方说明](https://highlightjs.org/usage/)我做了个[demo页面](http://www.whidy.net/demos/testHighlight/index.html),引用的是官方的示例代码,需要说明的是,我这里没有把所有的css文件放入styles目录,中间删除了大量的我不会用到的样式,省略,大家可自行通过官方[live demo](http://highlightjs.org/static/test.html)来取舍适量的样式.我这个demo中有个小问题,关于引用html的高亮代码时,由于嵌套关系,他会解析成其他的内容,那么本地测试时只好将标点转换成字符实体后,才可正常预览.当然一般来说wordpress的编辑器处于可视化模式下,粘贴源码后,自动会在文本模式下转换,我想可能不会有什么问题吧(后来发觉我实在是太天真了).

于是乎,关于本地静态页面中的highlight.js就算测试完成.接下来我测试整合入wordpress后的效果.


## wordpress测试


我将刚才用到的js和css文件放入博客的主题内,当然你也可以选择放在别处,只要你找得到绝对路径就行了.具体修改我就不多说了,修改主题文件**header.php**,将那三行代码加入**head**部分即可.

接下来,新建一篇日志进行测试,因为highlight.js是通过`<pre><code class="xxx">xxx表示语法类型</code></pre>`来识别的,所以按照此方式,我就不能再可视化区写日志了,而是在**文本**内通过源码写日志,我将html代码拷贝进去后,再来预览发现,一切都不如当初那样美好...我竟然忽略了一点,html代码在被解析了...而不是将我的源码正常输出了.

这下可就麻烦大了.思前想后,只能采取这样一种解决方案,把源码粘贴到可视化模式,然后再到文本模式下去添加`<pre><code class="xxx">.(被转换后的有很多字符实体的源码).</code></pre>`这样一切预览都正常了,只是文本模式下看到的内容就有点惨不忍睹了.(要是能直接引用到github的高亮就好了T_T)


<blockquote>后来我还想到其他解决方案,但是鉴于技术水平有限,也无法实现了,思路就是只要加个功能(JS?),遇到`&lt;code&gt;&lt;/code&gt;`内的内容直接输出,不解析即可(或者自动转换成字符实体),有时间的话,我会琢磨琢磨,再次,还可为自带编辑器添加一个添加代码的按钮,根据需要输入语法类型,它自动生成,这个主意很不错吧.</blockquote>


最后要说明的是,如果你也打算手动添加highlight.js,请注意你的主题自带的**pre**标签样式,进行适当修改哦~

哎,为了优美的代码,总是要付出代价的.看来又要把所有日志翻一遍了,因此之前所有引用源码的文章出现了[xxx][/xxx]的标签请不要拷贝,那头尾不是源码,中间的才是...真是突出一个苦逼呀...



* * *



花了两个晚上终于全改完了,却发现一个问题,当一行代码过长的时候,这个高亮代码显示会乱,虽然拷贝下来是正常的,但是看着很不爽.我有空再来改改,其他方面基本满意了~(2014年6月19日)
