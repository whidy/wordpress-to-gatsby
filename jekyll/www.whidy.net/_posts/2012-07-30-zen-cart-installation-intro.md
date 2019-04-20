---
author: whidy
comments: true
date: 2012-07-30 06:16:18+00:00
template: post
link: http://www.whidy.net/zen-cart-installation-intro.html
slug: /zen-cart-installation-intro
title: Zen Cart 1.5 图文安装过程全说明
wordpress_id: 907
category: '开发'
tags:
- 技术
- 教程
- 网站
---

最近公司需要我来维护一个zen cart后台系统的电子商务网站.说目前的网站问题很多,包括很多系统模块功能都出现问题.好吧,既然如此我又要在本地装个zen cart后台系统了.第一次装这个,还是跟大多数一样,从官方下载了[zen-cart-v150-utf8-20120309.zip](http://www.zen-cart.cn/download/products_extra_files/zen-cart-v150-utf8-20120309.zip )安装包后,解压所有文件(2222个文件共12MB= =!)并放置在你的本地PHP服务器环境的网站访问目录,例如:"E:\wamp\www\mall",在没有设置本地域名直接访问本地网站的情况下,通过输入"http://localhost/mall"可以访问,或是你希望通过设置本地域名访问,例如"http://m.net",当然具体办法不再复述,不会的话可以看看此文[Apache创建本地域名的服务器(WAMP环境)](/build-server-with-local-domain-in-wamp.html).我为了方便,我也简单修改了hosts文件和httpd-vhosts.conf.那么此刻输入http://m.net,将会提示下面内容:

![Zen Cart 1.5 未安装时访问效果](/wp-content/uploads/2012/07/01-400x285.jpg)

于是继续点击安装:

<!-- more -->

![安装步骤:第一步](/wp-content/uploads/2012/07/02-400x312.jpg)

勾上同意,进行下一步:

![安装步骤:第二步](/wp-content/uploads/2012/07/03-400x340.jpg)

接下来,对本地配置进行检测(这次是第二次安装所以环境完全符合,记得第一次安装的时候提示PHP_cURL不支持,如果你的电脑也出现了这种情况,请修改PHP配置):

![安装步骤:第三步](/wp-content/uploads/2012/07/04-361x400.jpg)

![安装步骤:第三步出现cURL错误时,请修改](/wp-content/uploads/2012/07/05-360x400.jpg)

再就是这关键的一步,进行数据库连接,当然前提是你已经在mysql中新建立好了这个数据库,例如我建了一个mall数据库.于是我如下图填写:

![安装步骤:第四步](/wp-content/uploads/2012/07/06-371x400.jpg)

于是点击进行安装,跳转到一个漫长的波浪线安装过程~~~(大概经过了6,7,8行...)

![安装步骤:第五步](/wp-content/uploads/2012/07/07-400x230.jpg)

最后一步对本地服务器的访问进行配置,这里我将默认的https修改成http,如果安装到服务器上,当然用默认的是比较安全的:

![安装步骤:第六步](/wp-content/uploads/2012/07/08-363x400.jpg)

保存系统设置后,配置你的网站信息.

![安装步骤:第七步](/wp-content/uploads/2012/07/09-400x374.jpg)

配置网站后台管理信息.

![安装步骤:最后一步](/wp-content/uploads/2012/07/10-393x400.jpg)

至此安装结束,赶紧登陆后台试试吧...

当你直接登陆后台的时候,它会提示错误:

删除 zc_install 目录。
修改后台目录名称。

按照说明修改后,再次登录(首次登录它要求你更换密码,修改完新密码后...),于是:

![安装完成,登陆后台效果](/wp-content/uploads/2012/07/11-400x395.jpg)

好了,,赶紧看看这个强大的后台管理系统吧...关于zen Cart模板修改,功能修改等等,目前还在研究中.

(对了如果还提示:**CURL SSL功能 = CURL需要SSL支持，请联系主机商。 28 => SSL connection timeout**, 请在Apache模块中勾选**ssl_module**,它会自动重启.就行了)
