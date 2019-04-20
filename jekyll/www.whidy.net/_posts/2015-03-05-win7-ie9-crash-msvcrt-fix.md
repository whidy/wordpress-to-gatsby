---
author: whidy
comments: true
date: 2015-03-05 10:18:07+00:00
excerpt: '莫名其妙的win7下IE9打开页面就会无限崩溃,重置ie,卸载重装,停用插件,等办法均无效.最后通过设置"使用软件呈现而不使用 GPU 呈现*"修好了,还真是奇怪呢,也不知道错误模块名称:
  msvcrt.dll,然后就是异常代码: 0xc0000005了这些都是什么鬼'
template: post
link: http://www.whidy.net/win7-ie9-crash-msvcrt-fix.html
slug: /win7-ie9-crash-msvcrt-fix
title: win7下IE9打开页面无限崩溃解决办法
wordpress_id: 2759
category: '开发'
tags:
- 技术
- 教程
---

最近有个同事的电脑,ie总是崩溃,我说我去看看吧,结果弄了一个来小时.也没搞定,重置ie,卸载重装,停用插件,等办法均无效.于是怀疑是不是压根不是系统ie文件问题了..

可是百度搜出来的哪些解决方案,可用率大家也是知道了,基本上还没我懂- -...突然想到去查看**事件查看器**,那里对于崩溃原因有详细的说明.于是打开**管理工具**的**事件查看器**,找到**Windows 日志** > **应用程序**,找到ie报错的大红感叹号,,,看看咋说的.好像看不懂饿,不过有效信息是错误模块名称: msvcrt.dll,然后就是异常代码: 0xc0000005了...见图

![IE crash error info](http://www.whidy.net/wp-content/uploads/2015/03/IE_ERROR-400x445.png)

那么有了这个再去查似乎好办多了...很快找到问题所在了.废话不说,说说这个方案:


<blockquote>Win + R > "inetcpl.cpl" > "高级" > 在**设置**里面找到"**加速的图形**" > 勾选"**使用软件呈现而不使用 GPU 呈现***" > 确定 > 重启电脑</blockquote>


再来打开ie测试一下,据说这个方法适用于ie9和ie11.当然测试环境是win7,据说不限于32位还是64位系统或者各种版本号...

另外值得思考的是,为什么硬件渲染会出问题呢,因为是公司电脑也不方便测试,初步怀疑是不是跟显卡驱动有关.如果有兴趣的话,建议尝试卸载旧的驱动,重新安装新的最稳定的显卡驱动进行尝试.

参考来源:
[IE9 crash after opening any site](https://social.technet.microsoft.com/Forums/ie/en-US/cc4c40c1-9222-4819-b2c7-5222cb283f26/ie9-crash-after-opening-any-site)
[Internet Explorer 9 crashes - APPCRASH, Application Name: iexplore.exe, Fault Module Name: msvcrt.dll](http://answers.microsoft.com/en-us/ie/forum/ie9-windows_vista/internet-explorer-9-crashes-appcrash-application/dddd387e-be6a-e011-8dfc-68b599b31bf5)
[如果您无法卸载 Internet Explorer 9 该怎么办](http://support.microsoft.com/kb/2579295)
