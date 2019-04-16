---
author: whidy
comments: true
date: 2012-05-15 15:23:20+00:00
layout: post
link: http://www.whidy.net/build-server-with-local-domain-in-wamp.html
slug: build-server-with-local-domain-in-wamp
title: Apache创建本地域名的服务器(WAMP环境)
wordpress_id: 771
categories:
- IT技术
- 技术分享
tags:
- 技术
- 网站
---

最近在弄公司网站服务器上的数据库跟公司办公用的电脑的本地服务器的数据同步,可是弄得焦头烂额,直到现在还有个问题phpmyadmin里面的中文字符都成了乱码的问题没有解决,今天就说说搭本地服务器那点事.

安装好WAMP之后,这里以WampServer Version 2.2为例.安装到了E:\WAMP\
在www目录内有一个phpcms文件夹,存放着phpcms系统安装的所有文件,首先安装这个PHPCMS访问地址是http://localhost/phpcms/install,那么安装好后,本地通过访问http://localhost/phpcms/查看站点首页,而服务器上的却是顶级域名,明显会在本地测试上带来诸多不便.如果想改成浏览器内直接输入http://p.com即可访问的办法是什么样的呢?

首先修改本机的hosts文件，XP在C:\WINDOWS\system32\drivers\etc\hosts,,如下：
示例：
127.0.0.1 localhost
127.0.0.1 p.com

然后找到E:\wamp\bin\apache\Apache2.2.21\conf\extra\httpd-vhosts.conf,,添加:


<blockquote><VirtualHost *:80>
ServerAdmin whidy@p.com
DocumentRoot "E:/wamp/www/phpcms/"
ServerName "p.com"
ErrorLog "E:/wamp/www/phpcms/error.log"
CustomLog "logs/dummy-host2.appservnetwork.com-access_log" common
</VirtualHost></blockquote>


接着找到E:\wamp\bin\apache\Apache2.2.21\conf\httpd.conf
修改#LoadModule vhost_alias_module modules/mod_vhost_alias.so **去掉#,意思是启用apache的虚拟主机功能**
以及#Include conf/extra/httpd-vhosts.conf **去掉#,意思是从conf/extra/httpd-vhosts.conf这个文件导入虚拟主机配置**

最后重启服务器,试着在浏览器内输入p.com,看看是否成功了呢?

如果出现错误就继续修改E:\wamp\bin\apache\Apache2.2.21\conf\httpd.conf
此处的


<blockquote>Options FollowSymLinks ExecCGI Indexes
AllowOverride None
Order deny,allow
Deny from all
Satisfy all</blockquote>


更改为


<blockquote>Options FollowSymLinks ExecCGI Indexes
AllowOverride None
# Order deny,allow
# Deny from all
# Satisfy all</blockquote>


当然,如果你有多个站点需要用这样的方式管理,那么这里就需要通过添加端口达到目的.

例如本机IP为：192.168.1.88
那如何控制 80,81,82 来访问不同的文件目录，而达到多个站点同时访问的目的？

打开appserv的安装目录，找到httpd.conf文件，找到：
Listen 80
加入：


<blockquote>Listen 80
Listen 81
Listen 82</blockquote>


然后参照前文虚拟主机的设置方法.不同的是,这个后边的端口号按自己需求更改就成了(当然不要忘记修改hosts文件哟~).例如:


<blockquote><VirtualHost *:81>
ServerAdmin whidy@whidy.net
DocumentRoot "d:/wampx64/www/whidy"
ServerName w.net
ErrorLog "logs/w-error.log"
CustomLog "logs/w-access.log" common
</VirtualHost></blockquote>


好了今天就为大家讲解到这里,如有疑问,可留言或发至电邮与我讨论~
