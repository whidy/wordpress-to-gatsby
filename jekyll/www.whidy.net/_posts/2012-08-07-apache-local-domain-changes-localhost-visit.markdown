---
author: whidy
comments: true
date: 2012-08-07 15:04:25+00:00
layout: post
link: http://www.whidy.net/apache-local-domain-changes-localhost-visit.html
slug: apache-local-domain-changes-localhost-visit
title: 将做好的Apache本地域名的服务器还原成默认localhost访问方法
wordpress_id: 941
categories:
- IT技术
- 设计相关
tags:
- 技术
- 网站
---

话说,前两天重装了系统,因为最近研究php,js,本地装了个Zend Studio 9.0.3...但是每次建立一个项目都需要新建个访问目录,,那么之前我做的域名访问具体可参考[Apache创建本地域名的服务器(WAMP环境)](/build-server-with-local-domain-in-wamp.html),一下子就变得很麻烦了...我总不能做个小测试的项目就新建立一个域名吧,虽然这些小项目可能不会太多,不过我还是决定将本地的服务器还原.

那么这个之前装的wamp就成了绿色版了 :cool:...废话少说,开始还原(事实上,基本上是个反向操作的过程!):

1.再一次重新安装apache和mysql的服务.并启动它们

2. 修改**X:\wamp\bin\apache\Apache2.2.21\conf\extra\httpd-vhosts.conf**文件,删除不必要的虚拟域名配置例如:


    
    <code><VirtualHost *:80>
    ServerAdmin whidy@p.com
    DocumentRoot “E:/wamp/www/phpcms/”
    ServerName “p.com”
    ErrorLog “E:/wamp/www/phpcms/error.log”
    CustomLog “logs/dummy-host2.appservnetwork.com-access_log” common
    </VirtualHost>
    </code>



3.修改**X:\wamp\bin\apache\Apache2.2.21\conf\httpd.conf**文件内的


    
    <code>LoadModule vhost_alias_module modules/mod_vhost_alias.so
    Include conf/extra/httpd-vhosts.conf
    </code>



前面都加个**#**号

***重启所有服务***

测试一下看访问是否正常,如果无法正常访问http://localhost/phpmyadmin/那么请修改这个文件

[caption id="attachment_944" align="aligncenter" width="400"][![alias域名修改配置](/wp-content/uploads/2012/08/alias-400x232.png)](/wp-content/uploads/2012/08/alias.png) alias域名修改配置[/caption]

将


    
    <code><Directory "X:/wampx64/apps/phpmyadmin3.4.10.1/">
    Options Indexes FollowSymLinks MultiViews
    AllowOverride all
    Order Deny,Allow
    Deny from all
    Allow from 127.0.0.1
    </Directory>
    </code>



改成

<!-- more -->


    
    <code><Directory "X:/wampx64/apps/phpmyadmin3.4.10.1/">
    Options Indexes FollowSymLinks MultiViews
    AllowOverride all
    Order Deny,Allow
    Allow from all
    Allow from 127.0.0.1
    </Directory>
    </code>



好了再次重启服务器,一切安好! :o
