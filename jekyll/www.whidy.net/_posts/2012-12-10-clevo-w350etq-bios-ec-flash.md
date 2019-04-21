---
author: whidy
comments: true
date: 2012-12-10 12:29:09+00:00
template: post
draft: false
link: http://www.whidy.net/clevo-w350etq-bios-ec-flash.html
slug: /clevo-w350etq-bios-ec-flash
title: Clevo W350ETQ 刷BIOS和EC图文详细教程
wordpress_id: 1427
category: '开发'
tags:
- 技术
- 教程
---

前几天有人放出了w350etq的最新的BIOS固件和EC固件,事实上我也不知道究竟有哪些实质的变化,究竟提升了些什么,但是貌似对WIN8的新功能支持的更好,虽然手头暂时没有固态硬盘,不过还在观望250G的固态硬盘,准备买了就用上这新功能,呵呵.闲话少说,进入正题,当然**刷固件有风险,菜鸟勿模仿,建议有SSD和有经验的玩家刷****.菜鸟刷毁后果自负.**



	
  1. **准备工作一:下载固件,制作可用的启动U盘**
下载固件很不容易.我的bios来源于超频NB网的帖子[W3x0ET-BIOS（1.02.18）及EC（1.02.08）[2012-11-27]](http://www.ocnb.cn/thread-11945-1-1.html),在此表示感谢,虽然不知道固件来源,不过测试过是没有问题的.(为了避免干涉BIOS版权问题,如有需要此固件请留言或电邮我.)除了有了固件文件,还有个不可少的就是纯DOS环境,好的,很显然,WIN98做DOS很简单的,不过软盘也装不下BIOS的固件,哈哈,开个玩笑.准备好一个U盘和一个制作U盘启动的工具,比如老毛桃之类的.(说明:请使用4G一下的U盘制作启动盘,至少我的两个16G的U盘是无法正常在DOS识别的.也是折腾了半天).这些准备工作做好了,咱就可以开始下一步了.

	
  2. **准备工作二:了解刷机过程,确保万无一失**
要知道刷固件可不是好玩的,一旦刷毁...你懂得 :cry: 那么,我们先看看摘自OCNB的说明:
<!-- more -->




使用机种： Terrans Force W3x0ET （Mobile Intel® HM77 Express Chipset）

备注：
BIOS 1.02.18版本说明：
1. System BIOS 1.02.18 (can't work with all 1.00.xx EC firmware).
2. Define e-SATA device as external device.
3. It is necessary to update system's EC firmware to 1.02.xx first.
4. It is necessary to refer to the instruction of readme.txt to update firmware.

EC 1.02.08版本说明：
1. EC firmware 1.02.08.
2. support both Windows 7 and Windows 8.
3. It is necessary to refer to the instruction of readme_EC.txt to update firmware..

风险及免责声明：
刷BIOS有一定风险，所以刷BIOS及EC导致笔记本电脑无法启动等一切失败后果，均自己承担。本人或其他方面均不为此负责。如您不同意该条款，请不要下载此软件刷新。

额外说明：
1.此版本支持windows 8系统
2.必须在DOS环境下刷新BIOS和EC
3.必须先刷EC，然后按照readme.txt更新BIOS
4.BIOS及EC版本不可以降级刷




好的,请读三遍后接着看将EC和BIOS解压出来后的readme_EC.txt和readme.txt,我将两个写到一起.


**How to flash EC firmware:**
1. Plug in AC adaptor.
2. Run ECFlash.bat under pure DOS to start EC flash procedure, the system will shut down automatically when the procedure is finished.
3. Plug off AC adapter for 5 seconds then plug in AC adapter.
4. Power on system and enter CMOS setup to check EC firmware version.
**How to flash whole ROM that include ME:**
1. Plug in AC adaptor.
2. Run MeSet.EXE under pure DOS, the system will auto cold boot.
3. Run FlashME.bat under pure DOS.
4. The system display flash complete message after flash success, if the system doesn't shut down automatically please press power button to power off.
5. Plug off AC adapter for 5 seconds then plug in AC adapter.
6. Power on system, the system will shut down automatically.
7. Power on system and enter CMOS setup to check BIOS version and load system defaults.


请仔细读三遍并牢记,^*%#^@&*%^*#&@%^&看不懂?什么 :shock: ?看不懂不要刷了...算了,不忍心,给大家简单翻译一下= =...


**如何刷EC的固件:**
1. 插上电源!
2. 纯DOS下运行ECFlash.bat开始刷入EC固件,刷完后电脑会自动关掉滴.
3. 拔掉电源5秒后再插上电源.
4. 开机看看EC版本
**如何刷整个ROM,包括ME?什么玩意我也搞不清楚反正就是刷BIOS:**
1. 又是插上电源!
2. 纯DOS下运行MeSet.EXE电脑会重启
3. 再进入纯DOS下运行FlashME.bat
4. 刷入完成后系统会提示成功, 如果电脑没有自动关闭请按电源键手动关机.
5. 又要拔掉电源5秒后插上
6. 启动电脑后电脑会自动关闭
7. 再进入BIOS看看版本呗...


不要偷懒中文的也读三遍,这里**小提示一下从运行MeSet.EXE开始,风扇狂转**,接下来上几张图片:

![未刷BIOS之前的版本](https://www.whidy.net/wp-content/uploads/2012/12/01biosInfo-1-400x300.jpg)

	
  3. **开刷EC**
用这个4G的U盘做好的DOS工具箱,进入纯DOS环境,先来刷EC.

![U盘的DOS工具(4G U盘)](https://www.whidy.net/wp-content/uploads/2012/12/02uTools-400x300.jpg)

![进入纯DOS环境](https://www.whidy.net/wp-content/uploads/2012/12/03pureDos-400x300.jpg)

![找到U盘内的存放固件的目录](https://www.whidy.net/wp-content/uploads/2012/12/04dosDirError-400x300.jpg)

![进入EC文件夹准备刷EC](https://www.whidy.net/wp-content/uploads/2012/12/05cdEc-400x300.jpg)

这里按照说明输入ECFlash.bat一切自动完成,风扇转一下就完事了.我们来看看版本,ok,good job! :razz:

![EC刷好后查看版本](https://www.whidy.net/wp-content/uploads/2012/12/06ecOk-400x300.jpg)

	
  4. **开刷BIOS**
这个稍稍有点麻烦,慢慢来.我算比较坑爹,我命名的02.BIOS目录名字居然在DOS下识别成这鸟样,怎么都进不去...没有办法只好重新进入系统,修改目录成了BIOS才得以顺利进行.刷机过程中会重启多次,完全按照那个说明文档来的.请严格遵守!

![坑爹的,居然不识别我这个目录命名](https://www.whidy.net/wp-content/uploads/2012/12/07biosError-400x300.jpg)

![这都不识别,不就是个02.BIOS](https://www.whidy.net/wp-content/uploads/2012/12/08folder-400x300.jpg)

![改名后DOS下进入BIOS目录](https://www.whidy.net/wp-content/uploads/2012/12/09cdBios-400x300.jpg)

![查看BIOS目录内文件](https://www.whidy.net/wp-content/uploads/2012/12/10dirBios-400x300.jpg)

![全部刷完检查刷新后版本](https://www.whidy.net/wp-content/uploads/2012/12/11ecBiosOk-400x300.jpg)

至此刷新结束,可以尽情享受还没有固态硬盘也没装WIN8的屌丝的快乐吧= =!

	
  5. **刷机完成有什么变化?**
最后给大家看看BIOS里面的变化,应该说其实这个刷机是为了给SSD用新的引导模式,开启UEFI后,配合SSD,能更快的启动计算机还有很多更复杂更强大的功能,我查阅了相关文献,暂时也还不大明白,目前也正在观察市场的固态硬盘到时候入手了,装上WIN8体验一下可以带来的快乐.

![刷后BIOS的一些变化](https://www.whidy.net/wp-content/uploads/2012/12/12changes-400x300.jpg)

![刷后BIOS的一些变化](https://www.whidy.net/wp-content/uploads/2012/12/13changes-400x300.jpg)

![刷后BIOS的一些变化](https://www.whidy.net/wp-content/uploads/2012/12/14changes-400x300.jpg)


好了,本次介绍的就是刷BIOS了所以其他更深奥的学问今天就不说了,毕竟弄这个全球第一W350ETQ刷机教程也是不太容易,本来是用单反的,结果被借出去了,又不想等,于是在双休就用手机变弄边录制,还有一些刷机过程的视频,我已经传到优酷上了,有兴趣可以看看(作者**小白来看看**,因为还在上传呢),那个不是教程,所以实际意义不大.如有看不明白的请与我联系.另外还有W350ETQ其他相关评测文章有兴趣的话请自行搜索...好了,研究别的去了.

视频传好了我不内置进来了.

[视频一: W350ETQ刷EC过程(不好意思,手机拿倒了- -!)](http://v.youku.com/v_show/id_XNDg2NjAzMzU2.html)

[ 视频二: W350ETQ刷BIOS过程(嘿嘿这次没拿反: )](http://v.youku.com/v_show/id_XNDg2NjA3NzY0.html)
