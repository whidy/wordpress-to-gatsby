---
author: whidy
comments: true
date: 2017-08-12 08:10:27+00:00
excerpt: 为了让wordpress支持markdown,重新升级了后台和主题还是没能像官方说明那样解决...最后才发现,那是给基于wordpress官方站点上创建的博客使用的...也真是醉了.
layout: post
link: http://www.whidy.net/wordpress-markdown-not-support.html
slug: wordpress-markdown-not-support
title: 为了Wordpress支持markdown...我重装了wordpress和theme,然而...
wordpress_id: 2966
categories:
- 其它
- 杂谈
tags:
- 网站
---

随着时代的推移,大部分文档开始使用markdown格式来编写了...我也打算把这些我排版好的markdown格式的文件直接弄到wordpress上面发表...我Google了一下,第一篇就是这篇文章[Markdown — Support](https://en.support.wordpress.com/markdown/).

满怀欣喜的按照里面的说明找到**设置 - 撰写**, 却没有看到那个开启markdown的选项.

我有点不爽,难道是版本过低.对于每次进入后台都看到升级提示已经令我很不爽了...好吧我更新一下吧.折腾了大半天更新完了...也就是现在看到的博客的新样子...有2015主题换成了2016主题,本来想2017的,完全不懂头部的那张大图的设计含义...小心翼翼的保证一切主题修改的没出错(其实我也不知道到底出错没).主要是插件,主题的部分php修改,还有自己添加的代码高亮组件.反正瞎倒腾好了...再次满怀欣喜的找到设置-撰写发现根本就跟之前一样的时候...

我觉得我经历了绝望.这什么破玩意哦...遂去查找有没有相关的Markdown插件,貌似也没一个比较好用的...

这次大的更新,就当作是升级了一下...找了很多为什么没有刚才那个选项,后来说只有在他们服务器上面开的wordpress站点才支持,并非wordpress这个程序支持...于是我在我在wordpress上面创建的博客后台找到了...真是坑爹.

![wordpress是不支持markdown的](http://www.whidy.net/wp-content/uploads/2017/08/markdown-400x335.png)

好吧,至此,如果实在是要的话,就只能用插件了...我不太想装插件,勉强就先这样了.如果你需要的话,据说比较好用的就是Jetpack了,大家自己尝试下下咯~


<blockquote>参考:

[How to use markdown for wordpress posts](https://stackoverflow.com/questions/44538043/how-to-use-markdown-for-wordpress-posts)

[在Wordpress中如何使用MarkDown编辑博文？](https://www.zhihu.com/question/28276750)</blockquote>
