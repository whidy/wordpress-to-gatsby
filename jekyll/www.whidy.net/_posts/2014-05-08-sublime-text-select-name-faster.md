---
author: whidy
comments: true
date: 2014-05-08 10:40:13+00:00
layout: post
link: http://www.whidy.net/sublime-text-select-name-faster.html
slug: sublime-text-select-name-faster
title: sublime text快速选择带有横线(连接符)的类名或ID名等
wordpress_id: 2062
categories:
- IT技术
- 技术分享
tags:
- sublime text
- 技术
---

其实sublime text的设置中有很多小秘密,例如本文介绍的,通过修改其中的一个配置,就可以实现直接**鼠标双击**或者快**捷键CTRL+D**,就能选中例如"sub-menu"这样的类名或者ID名,其实也是工作需要,代码规范要这样做,之前的驼峰式就废弃了,下划线显然不好,于是就用横线来连接关联起来了,直接来说怎么设置吧.

1. 打开SUBLIME TEXT(2和3都通用.)

2. 打开配置文件**Settings - User**

![快速选择带有横线连接符的类名或ID名](http://www.whidy.net/wp-content/uploads/2014/05/fast-select-400x175.jpg)

3. 在花括号内最后一行插入下面这段


    
    ```css
    "word_separators": "./\\()\"':,.;<>~!@#$%^&*|+=[]{}`~?"
    ```



好了,保存文件.试试效果吧.

最后简单说明一下,这行实际上是默认设置里改了,去掉了"**-**"字符,用用户设置覆盖默认设置,有兴趣可以打开**Settings - Default**,看其他更多设置
