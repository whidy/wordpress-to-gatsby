---
author: amo
comments: true
date: 2013-09-21 01:02:35+00:00
template: post
link: http://www.whidy.net/location-of-wordpress-functionprototype.html
slug: /location-of-wordpress-functionprototype
title: wordpress函数原型的位置
wordpress_id: 1762
category: '开发'
tags:
- wordpress
- 技术
- 教程
---

wordpress经常会用到内部定义的一些函数，你经常想要查看，但是又不知道放在哪里。又是用中文百度，又是用英文google，找到一个网页[http://phpdoc.wordpress.org/tags/3.6.1/](http://phpdoc.wordpress.org/tags/3.6.1/)这里面有wordpress所有函数的介绍了，然后在这里面搜索你要查看的函数，比如你要找get_header,就在浏览器上按ctrl+f，搜索get_header，找到左侧栏中的get_header

[![findFunction](http://www.whidy.net/wp-content/uploads/2013/09/findFunction.jpg)](http://www.whidy.net/wp-content/uploads/2013/09/findFunction.jpg)

左侧栏的函数

单击就看到右侧栏中get_header的介绍了

[![functionIntroduce](http://www.whidy.net/wp-content/uploads/2013/09/functionIntroduce-400x152.jpg)](http://www.whidy.net/wp-content/uploads/2013/09/functionIntroduce.jpg)

右侧栏的函数介绍

这时把右边栏拉到最上端，就可以看到函数原型的路径了

[![functionDirectory](http://www.whidy.net/wp-content/uploads/2013/09/functionDirectory-400x58.jpg)](http://www.whidy.net/wp-content/uploads/2013/09/functionDirectory.jpg)

打开路径中的文件查看函数原型即可。

[![functionPrototype](http://www.whidy.net/wp-content/uploads/2013/09/functionPrototype-400x169.jpg)](http://www.whidy.net/wp-content/uploads/2013/09/functionPrototype.jpg)
