---
author: whidy
comments: true
date: 2018-03-17 03:13:37+00:00
excerpt: 自从坑爹的3TB希捷ST3000DM001突然暴毙，电脑上就只有一个480G的SSD了，这怎么能行呢。SSD肯定是不能做仓库盘的，毕竟还有很多不常用数据不适合放在SSD上，比如下载的电影，音乐，照片，视频教程之类。于是，鉴于历史的教训，我决定买故障率最低的东芝监控盘MD04ABA400V，
  回来装上后发现开机奇慢。于是又折腾了几天几夜。。。
layout: post
link: http://www.whidy.net/x79-4tb-hdd-boot-slow-gpt-uefi-bug.html
slug: x79-4tb-hdd-boot-slow-gpt-uefi-bug
title: X79SR主板安装4TB大容量硬盘后开机奇慢折腾数日小结
wordpress_id: 3126
categories:
- 其它
- 技术分享
- 杂谈
---

自从坑爹的3TB希捷ST3000DM001突然暴毙，电脑上就只有一个480G的SSD了，这怎么能行呢。SSD肯定是不能做仓库盘的，毕竟还有很多不常用数据不适合放在SSD上，比如下载的电影，音乐，照片，视频教程之类。于是，鉴于历史的教训，我决定买故障率最低的东芝监控盘MD04ABA400V， 回来装上后发现开机奇慢。于是又折腾了几天几夜。。。

最后无奈退货了。折腾的过程我就不详细说了，几天几夜的收获我简单总结下吧。


### 异常现象：


我的电脑主板是**Intel X79SR**，有**2个原生SATA3**，2个原生SATA2，**2个第三方SATA3控制器**，一个SSD（**WIN10，开启了AHCI且UEFI引导**）和4T新硬盘安装在原生SATA接口上，一直会开机的时候在BIOS自检后卡顿接近2到3分钟，此时硬盘等持续亮着，也就是一直在读取操作。


### 分析原因：


起初以为是主板对4T硬盘支持不好，自检时间过长，查阅主板说明书和相关相同主板有关资料，考虑到之前用的3T都没什么，认为与此无关。

换成第三方SATA3接口后，竟解决了开机慢的问题，然而出现新问题，关机时，硬盘断电异常，也就是无法正常停止硬盘供电，导致每次关机咔嚓一声响，SMART检测异常关机次数累加。因此该方案无效！

怀疑是硬盘问题，可是经过各方检测，一切属性良好，故排除。

怀疑过电源问题，供电不足导致，经过接口调换，单独供电等测试无效，故排除。

怀疑是硬盘分区格式问题，将4T硬盘的GPT改为MBR（此时仅可使用容量不到2T），似乎开机恢复正常，但是少了2T的容量是不可行的。

怀疑是UEFI问题，于是拔掉SSD，单装4T硬盘，通过U盘进入PE，依旧很慢，于是关闭UEFI，就好了。但是我SSD上WIN10系统用的是UEFI引导，又不想重装系统，于是十分纠结。


### 解决方案：


最后我还是很抱歉的退掉了4T的东芝神盘，决定买个2T的HDD，因为京东上希捷价格相对低一些，而且2T的故障率没有那么高了，最后还是买了希捷（我想用个几年就备份一次数据，还新硬盘吧）。

由于事情过去一个多月了，记不清楚是否装上开机就正常了，但是我清楚地记得，并可以得出一个准确的**结论**：

Intel X79TO/SI/SR系列的主板，对UEFI的支持是绝对很差的。当磁盘处于GPT分区状态下，会发生不可预料的异常（我记得当时UEFI下安装WIN10装不上，我后来通过特殊手段在PE下才装好）。

那么最好的方案是该主板安装WIN7，可以开启AHCI模式，**不要开启UEFI**！尽量使用MBR，如果硬盘容量过大，采用GPT也可（之前3T从未出现开机很慢的情况）。

如果非要安装WIN10（比如我玩游戏仅支持WIN10系统，所以才换了系统），也不要用UEFI，使用MBR引导方式来进行安装即可。如果系统盘是大硬盘，也可使用GPT，这个虽然后来没办法测试，但是理论上应该是可以的。

最后简单来说，Intel X79系列主板对UEFI支持很差，慎重使用！的确有些老主板说明支持一些新特性，但是实际上容易出现的问题很多，也就是说旧电脑即便配置性能达标，但是也不建议追新~




