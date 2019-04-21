---
author: amo
comments: true
date: 2014-02-12 14:20:35+00:00
template: post
draft: false
link: http://www.whidy.net/double-oss-time-error.html
slug: /double-oss-time-error
title: 'ubuntu和win7双系统时间错误  '
wordpress_id: 1863
category: '开发'
tags:
- 技术
---

昨天的文章中没有解决的问题，今天百度了一下，找到了原因，直接copy下来吧，原文地址http://blog.163.com/imxle@126/blog/static/13312018620104264451156/

注：并非有意copy制造伪原创，实在是因为太多页面随着时间或是别的什么原因，就消失了，所以保留一个自己的版本。

win7的系统时间，机子没上网，每天开机时，总会慢8小时，不知道怎么回事，因为忙别的事情，所以过了那几天才找原因，后来发现windows time服务没有自动，所以想当然认为是这个原因。
用了几次也没发现什么异常，因为今天开机时候没插网线，直接进了ubuntu，发现时间快了8小时，插上网线就正常了，所以觉得不太正常，所以重启进了win7，发现慢了8小时，这才意识到可能是两个系统设置不同，导致的这个时间问题。于是google：
两个概念：
UTC即Universal Time Coordinated，协调世界时
GMT即Greenwich Mean Time，格林尼治平时

Windows 与 Mac/Linux 缺省看待系统硬件时间的方式是不一样的：
Windows把系统硬件时间当作本地时间(local time)，即操作系统中显示的时间跟BIOS中显示的时间是一样的。
Linux/Unix/Mac把硬件时间当作 UTC，操作系统中显示的时间是硬件时间经过换算得来的，比如说北京时间是GMT+8，则系统中显示时间是硬件时间+8。
这样，当PC中同时有多系统共存时，就出现了问题。
假如你的ubuntu设置的时区都为北京时间东八区，当前系统时间为9：00AM。则此时硬件中存储的实际是UTC 时间1:00AM。这时你重启进入Windows后，你会发现windows系统中显示的时间是 1:00AM，比ubuntu中慢了八个小时。同理，你在Windows中更改或用网络同步了系统时间后，再到Ubuntu中去看，系统就会快了8小时。在实行 夏令时的地区，情况可能会更复杂些。

解决这个问题的方法:
1. 可让 Ubuntu 不使用 UTC 时间与 Windows 保持一致。
ubuntu默认开启UTC,即协调世界时，而win7是使用这种计时方式，这将导致的结果就是Windows和Ubuntu时间计算有差异
你 可以使用以下方法得到一致的时间：
sudo gedit /etc/default/rcS
找到这一行：UTC=yes
把 yes改为no

2. 修改 Windows 对硬件时间的对待方式，这样只在 Windows 上修改后就无需在Ubuntu 上设置了。
让 Windows 把硬件时间当作 UTC
开始->运行->CMD，打开命令行程序(Vista则要以管理员方式打开命令行程序方 可有权限访问注册表)，在命令行中输入下面命令并回车


**代码:**







Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
