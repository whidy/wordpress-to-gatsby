---
author: amo
comments: true
date: 2014-02-11 12:46:12+00:00
layout: post
link: http://www.whidy.net/double-disks-double-oss.html
slug: double-disks-double-oss
title: 4740g笔记本固态加机械硬盘，安装双系统，及非常规拯救措施
wordpress_id: 1860
categories:
- IT技术
- 技术分享
tags:
- 技术
---

年前因为对linux系统的兴趣和电脑更新的需要，买了一块120g的ssd和一个光驱位转硬盘位托架，还有一根2G的1066的尔必达内存条（配合原来的2G双通道），是考虑了最近内存还是比较贵，及兼容和速度的原因。我的笔记本是3i的配置，是宏碁4740G里面配置最低的了。笔记本的主板支持两个sata2，但是ssd还是买了支持sata3的三星的，当然还是看你们自己的需要了。

原来的机械硬盘还是放在原来的位置，这是考虑机械硬盘的抗震和散热的需求，光驱位则装了ssd。可以选择把linux和win7都装在ssd上，我没有尝试过，不知道引导会出什么问题。我是选择的ssd安装win7，HDD安装linux。说下步骤（使用U盘引导安装）：

1.先将机械硬盘拆下来，在SSD上安装win7，这个没有问题，单独启动也没有问题。

2.将固态硬盘拆下来（不需要把电脑拆散，背面有一个螺丝，是固定光驱位的，卸下即可将光驱位硬盘拖出），安装Ubuntu12.04，当然系统你自己选，我两个系统都是装的64位的。安装的时候可以断网安装，这样快一些。

3.安装完之后把SSD装上，开机，发现没有win7的引导项。两个办法，第一，进入Ubuntu后升级所有可升级的软件，重启应该会有win7的引导项了。如果没有，第二个办法：更改/boot/grub/grub.cfg文件，将以下代码添加在文件的第一个menuentry之前或者之后都可以。不懂什么意思可以百度“grub.cfg详解”。

=================代码开始==================

menuentry 'Windows 7 (on /dev/sdb1)'{
load_video
insmod gzio
insmod part_msdos
insmod ntfs
set root='(hd1,msdos0)'
search --no-floppy --fs-uuid --set=root 1C2E1CB12E1C85C4
chainloader +1
}

=================代码结束==================

注意“set root='(hd1,msdos0)'”是win7在ssd的安装位置，如果你是将win7安装在第一分区的话就没有什么问题，下面的uuid话说可以删掉。其实是跟“set root='(hd1,msdos0)'”这句话相同的意思。grub.cfg这个文件是不建议修改的，但是我们就是开机用一下，改改也无所谓了，文件权限为只读，请自行修改权限。

说说自己碰到的一些问题。用win7安装oracle 11g的时候忘记在安装完之后把oracle的服务自启动关掉了，结果再进win7的时候cup和内存的资源都被oracle的服务占用，无法打开注册表、配置、和电脑管理，也就是想病毒一下，让你无法控制电脑了。

不知道使用winpe有没有办法，我当时没有winpe，准备进win7的安全模式，发现引导是由ubuntu的grub控制的，想百度查下有没有grub添加win7安全模式的方法，大都答非所问。好吧，直接拆机械硬盘，开机按F8，但是根本没有理财我，直接进了win7，还是那个样子。试了好几次都没有办法进安全模式，只能用绝招了，在进入win7后将锂电池拆掉，然后直接拔适配器的电，再重启电脑，就出现安全模式的选项了，进入安全模式，把所有的oracle自启动服务关掉，重启，一切恢复原样。

现在还有一个问题，一直没有找到原因，进Ubuntu之后在进win7，系统时间就出错了，但是日期没有问题。进ubuntu也是同样的问题。win7是用小马软件破解的。一直不知道为什么。。。。