---
author: whidy
comments: true
date: 2012-04-28 06:06:32+00:00
layout: post
link: http://www.whidy.net/phpcms-keywords-search-problem.html
slug: phpcms-keywords-search-problem
title: PHPCMS无法搜索文章内容中的关键字解决
wordpress_id: 679
categories:
- IT技术
- Phpcms
- 设计相关
tags:
- 技术
- 网站
---

最近工作上维护公司的网站,其后台用的是PHPCMS V9,以前曾用过PHPCMS2008,用这个还算能够快速上手.不过使用过程中也有很多问题,比如这个最近网站遇到的搜索功能的问题,经常搜不到文章,除非是标题或者关键字有相同的,而文章内容部分是搜索不到的,编辑需要找相关文章来进行SEO优化也不是很方便,于是我便研究了一下PHPCMS自带的搜索功能,首先要说的是后台可以对搜索进行设置和调整的区域主要包括



	
  1. **模块 > 模块管理 > 全站搜索 > 模块管理 > 全站搜索**

	
  2. **内容 > 内容相关设置 > 模型管理 > 文章模型字段管理**


第一个很简单,直接查看模块配置,如果没有选中全站搜索的果断选中,这样可以避免一些搜索不到信息的情况,后面两个我也选中是了,至于选不选,看个人需要了.提交之后建议重建索引,这里需要提到的是,有时候重建索引出错,出错内容大致是这样的


    ```sql
    MySQL Query : DELETE FROM 'phpcmsv9'.'v9_search' WHERE 'siteid' = '1'
    MySQL Error : Incorrect key file for table '.\phpcmsv9\v9_search.MYI'; try to repair it
    MySQL Errno : 126
    Message : Incorrect key file for table '.\phpcmsv9\v9_search.MYI'; try to repair it
    Need Help?
    ```



这个解决办法也十分简单,同样在后台找到 **扩展 > 扩展 > 数据库工具 > **在**请选择数据链接池**处选择数据库后,会展现出该数据库的结构,找到**v9_search**和**v9_search_keyword**表,后面有修复,点击**修复**,然后重新回到重建索引处,就不会出错了.

另一方面如果有些关键字是你需要在搜索结果中显示的,比如**作者**,**内容**等等,先说如何搜索到作者吧,找到 **内容 > 内容相关设置 > 模型管理 >** 进入**文章模型**的**字段管理**,找到**作者**字段,点击**修改**,在下面单选选项处可以看到**作为搜索条件**,此选项,选择**是**即可.

同样的,**内容**字段也是这个方法,不过有个问题,内容字段的**作为搜索条件**处是**灰色不可更改**,这要怎么办是好?这种情况下,如有需要,那就要强行修改数据库内的值了,以**内容**字段为例,打开数据库,这里我用的phpmyadmin,找到相应数据库的表**v9_model_field**,找到其中**name**为**内容**(**field**为**content**)的地方,点击编辑,其中有个字段叫做**issearch**,当前值为**0**,于是我们将它修改为**1**即可.再次返回后台,会发现**作为搜索条件**已经是**是**了.

此时,你可以尝试搜索一些关键字,会发现问题得到解决,如果你还有什么问题,可以发电子邮件给我,我会抽时间与你一起讨论.

好了暂时写到这里,谢谢大家的关注.如果想了解sphinx全文索引可以看一个PHPCMS官方论坛的帖子,写的不错,点击进入[phpcms中应用sphinx全文索引](http://bbs.phpcms.cn/forum.php?mod=viewthread&tid=149380)
