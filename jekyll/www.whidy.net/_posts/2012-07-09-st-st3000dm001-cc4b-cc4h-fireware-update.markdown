---
author: whidy
comments: true
date: 2012-07-09 13:18:45+00:00
layout: post
link: http://www.whidy.net/st-st3000dm001-cc4b-cc4h-fireware-update.html
slug: st-st3000dm001-cc4b-cc4h-fireware-update
title: 希捷3T硬盘ST3000DM001,CC4B升级固件至CC4H解决咔咔噪音办法
wordpress_id: 875
categories:
- 兴趣
- 评测
tags:
- 技术
- 教程
---

前不久在淘宝上买了一块硬盘3T的希捷的硬盘,可算是缓解了磁盘之急.拿回来用HDTUNE测了一下,感觉不错.爽了没多久...一阵阵咔嚓咔咔的声音从机箱内传出来,心中不禁疙瘩一下.太恐怖了.仔细听来,过个十几分钟就会响一下,这要是一直下去硬盘岂不是会坏掉?这声音有点像磁头归位的感觉,先不谈是个什么原因导致,就说怎么解决吧...

话说经过将近一个月的煎熬,终于希捷官方出了新的固件**CC4H**啊,简直是3T西粉的救命稻草啊.于是到处查阅资料,做好刷固件的准备,在此我做了以下总结:



	
  1. 问:刷硬盘固件,会影响数据么?
答:理论上来讲不会损坏硬盘上的任何数据,除非更新过程中发生意外,例如断电,地震导致硬盘剧烈震动,哈哈等等...

	
  2. 问:刷硬盘固件,简单么?
基本上比较傻瓜的方式,有两种:1.刻录启动光盘刷固件,不推荐! 2.有个程序运行后,点击确认,系统自动重启进行固件更新.

	
  3. 问:刷硬盘固件,能提高性能么?
答:请不要指望性能提高,性能跟硬件设备息息相关,顶多会提高稳定性! 据说能减小C1的增加速度.


那么开始按照以下步骤刷吧(因为我已经刷完了所以很抱歉没有截图,我尽可能详细的描述当时的情景

[caption id="attachment_883" align="aligncenter" width="400"][![固件刷新过程](/wp-content/uploads/2012/07/fw-update-400x223.jpg)](/wp-content/uploads/2012/07/fw-update.jpg) DOS环境下固件刷新过程[/caption]



	
  1. 官方下载刷硬盘固件的程序[Barracuda (1TB disk platform) Firmware Update](http://knowledge.seagate.com/articles/en_US/FAQ/223651en),官方称之为1TB专用,其实只要符合要求即可.当然不了解自己硬盘参数的,同样可以下载小工具[Drive Detect software](http://support.seagate.com/firmware/drive_config.html)进行检测.确保无误开始下一步操作.

	
  2. 运行Barracuda-ALL-GRCC4H.exe程序,按照提示点击下一步,一直到最后提示重启.整个程序会自动进行操作.

	
  3. 重启后,自动引到进入DOS环境,整个过程全自动,你只要保证不操作,电源供应不会出现问题即可.

	
  4. 最后,再次重启进入系统,一切升级过程完成.




当然,整个过程中据说也有失败的,例如:






[caption id="attachment_884" align="aligncenter" width="538"][![3T硬盘刷固件后简单测试](/wp-content/uploads/2012/07/st_fw_update.jpg)](/wp-content/uploads/2012/07/st_fw_update.jpg) 3T硬盘刷固件后简单测试[/caption]







	
  1. Barracuda-ALL-GRCC4H.exe程序最后一步,黑了下,提示错误.大概意思是

	
  2. 据说在AHCI模式下无法完成更新,需要在BIOS内设置成IDE后,才能更新,更新完后,重新设置成AHCI,当然我这个破主板居然找不到硬盘模式选择,也就没管了,总之是更新成功了,当然我这个破主板很诡异,WIN下用seatools检测不到硬盘.


最后,如果成功了,恭喜你.目前基本上解决了咔咔咔嚓的声音,当然要是仍然不满意,我在网上搜集到了另外一个办法调整AAM的,用DiskInfo中如图的设置AAM,开启并拖至最右边!当然我不是很在乎这个,没有噪音,整个世界都舒畅了,呵呵

[caption id="attachment_886" align="aligncenter" width="400"][![AAM调节](/wp-content/uploads/2012/07/AAM-400x364.jpg)](/wp-content/uploads/2012/07/AAM.jpg) AAM调节[/caption]
