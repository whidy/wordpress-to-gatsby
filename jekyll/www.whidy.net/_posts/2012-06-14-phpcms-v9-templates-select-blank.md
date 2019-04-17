---
author: whidy
comments: true
date: 2012-06-14 07:16:22+00:00
layout: post
link: http://www.whidy.net/phpcms-v9-templates-select-blank.html
slug: phpcms-v9-templates-select-blank
title: PHPCMS V9 栏目模版空白无显示解决方案
wordpress_id: 814
categories:
- IT技术
- Phpcms
- 技术分享
tags:
- 技术
- 网站
---

先看看问题截图:

![PHPCMS V9 栏目模版空白无显示解决方案](/wp-content/uploads/2012/06/tBlank.jpg)

很明显**栏目首页模板：**选择处什么都没有,该死的PHPCMS这次坑了我一大把啊.怎么会突然没有了?我还搜遍了全世界,跑论坛上找答案,结果论坛上的没有一个人回答是什么原因.当然提问贴不多,只有三个跟我的情况类似.于是推出结论,这个问题发生概率较小并且要么是奇迹诡异并且复杂的问题,要么是过于简单一般人能够处理的问题,而我最近脑袋卡壳,想不出来......

过了若干小时,突然想到做个测试,我把list_xxx全部移到别的地方,再来看栏目列表页模板,也没有了,说明读取模板正常,而category的模板里,有个是我用系统默认备份功能备份了一遍的,就是所谓的,选中某个文件按住ALT拖放,对的罪魁祸首就是这步操作.本来是想做个备份文件,而这个文件包含了中文字,那么就导致PHPCMS系统无法读出所有的模板,这也太2了啊!!!**解决方案很简单,把文件名改成全英文字符的就可以了.**
