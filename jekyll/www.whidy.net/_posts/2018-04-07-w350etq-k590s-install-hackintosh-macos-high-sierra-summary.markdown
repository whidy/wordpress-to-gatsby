---
author: whidy
comments: true
date: 2018-04-07 10:29:31+00:00
excerpt: 作为一名爱瞎折腾的前端来说, 学会使用MacOSX, 或许是有必要的, 于是想着去买一台MBP, 可是无奈电脑太多, 不想再添置, 于是把我的神级Clevo W350ETQ(也是神舟后来出的K590S)忍痛的挂在了闲鱼上,
  自己一直保养很好, 后来怒加4G条子和SSD, 所以卖的比一般的二手贵, 无人识相, 遂继续自用.
layout: post
link: http://www.whidy.net/w350etq-k590s-install-hackintosh-macos-high-sierra-summary.html
slug: w350etq-k590s-install-hackintosh-macos-high-sierra-summary
title: Clevo W350ETQ(神舟K590S)安装黑苹果10.13总结
wordpress_id: 3133
categories:
- IT技术
- 其它
- 技术分享
- 杂谈
tags:
- 下载
- 技术
- 教程
---

<blockquote>
  
> 
> 2018年7月16日更新
> 
> 
</blockquote>





经过了长达半年的折腾。陆陆续续修修补补，终于把这个机型的黑苹果给完善了。此文档主要做备份说明和分享。我将相关Clover配置和补丁文件发布到了Github，有兴趣可以直接访问：





**[准系统W350ETQ（神舟K590S）的黑苹果Clover](https://github.com/whidy/W350ETQ-Clover)**





下载下来直接尝试使用。





以下内容是之前4月写的，有兴趣可以阅读。





* * *





<blockquote>
  
> 
> 作为一名爱瞎折腾的前端来说, 学会使用MacOSX, 或许是有必要的, 于是想着去买一台MBP, 可是无奈电脑太多, 不想再添置, 于是把我的神级[Clevo](http://www.clevo.com.tw/index-tw.html) W350ETQ(也是神舟后来出的K590S)忍痛的挂在了闲鱼上, 自己一直保养很好, 后来怒加4G条子和SSD, 所以卖的比一般的二手贵, 无人识相, 遂继续自用. 我的电脑配置及相关评测曾经也在博客([相关索引](https://www.whidy.net/?s=w350))中提到. 在当年来说是非常强悍的一款游戏本, 至今依然能算一台中端性能笔记本, 只是便携性太差, 一直以来都作为办公台式机使用, 我这台配置如下:
> 
> 
</blockquote>




    ```
    处理器名称: Mobile QuadCore Intel Core i7-3612QM, 3000 MHz (30 x 100)
    主板名称: Clevo W35_37ET
    主板芯片组: Intel Panther Point HM77, Intel Ivy Bridge
    系统内存: 8084 MB (4 GB * 2 DDR3-1600)
    显示适配器:
      Intel(R) HD Graphics 4000
      NVIDIA GeForce GTX 660M
    显示器: LG Philips LP156WF1-TLC1 [15.6" LCD]
    音频适配器: Realtek ALC269 @ Intel Panther Point PCH - High Definition Audio Controller [C-1]
    IDE 控制器: Intel(R) 7 Series Chipset Family SATA AHCI Controller
    IDE 控制器: Realtek PCIE CardReader
    硬盘驱动器: OCZ-VERTEX4
    硬盘驱动器: ST9500423AS
    光盘驱动器: TSSTcorp CDDVDW SN-208AB
    键盘: PS/2 标准键盘
    鼠标: ELAN Input Device
    网络适配器: Realtek PCIe GBE Family Controller
    网络适配器: Realtek RTL8723AE Wireless LAN 802.11n PCI-E NIC (192.168.31.248)
    USB 设备: BisonCam, NB Pro
    USB 设备: Realtek Bluetooth 4.0 Adapter
    USB 设备: TouchStrip Fingerprint Sensor (WBF advanced mode)
    DMI 系统制造商: CLEVO CO.
    DMI 系统产品: W35_37ET
    ```





只有先弄清楚配置才能接下来进行黑苹果的安装, 其实几年前我尝试过安装黑苹果, 最终以失败告终, 然而本来是抱着看看的心理, 又跑去看远景论坛, 看到一个帖子: 





[【初春之献】macOS High Sierra 10.13.4 17E199 With Clover 4423修正原版镜像](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1780088), 一下子又动了心, 于是这清明几天假又没有休息好, 为了安装上黑苹果简直比上班工作的状态还要投入, 一下子三天过去了, 我后背越发疼了. 心想这几天本来可以好好休息顺便学习下`Vuex`, 计划泡汤! 好在, 最后还是折腾出来了点结果. **基本上算比较完美了.** 接下来我就对这几天的研究做个总结. 先上图两张图过过瘾. <!-- more -->





[![系统截图](https://raw.githubusercontent.com/whidy/daily/master/sources/images/2018-04-07-1.png)](https://raw.githubusercontent.com/whidy/daily/master/sources/images/2018-04-07-1.png) [![W350ETQ和红苹果](https://raw.githubusercontent.com/whidy/daily/master/sources/images/2018-04-07-2.jpg)](https://raw.githubusercontent.com/whidy/daily/master/sources/images/2018-04-07-2.jpg)





## [](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)%E9%BB%91%E8%8B%B9%E6%9E%9C10.13.md#%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C)准备工作







  * 和我型号相同的电脑并开启了UEFI启动


  * 可能需要注册[远景论坛](http://bbs.pcbeta.com/)账号来下载附件, 需要查阅[tonymacx86](https://www.tonymacx86.com/)来解决问题


  * 需要有极高的耐心去谷歌相关错误代码


  * 需要具备一定的英文基础来阅读英文章或者有耐心对英文文章自行翻译研究


  * 一个用来制作启动盘的U盘


  * 一块硬盘或者预留好的可用的分区


  * 一个下载好的并集成了Clover的[macOS High Sierra 10.13.4](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1780088)镜像


  * Windows下使用的两个软件`TransMac`和`DiskGenius`


  * Mac下的`MaciASL`, `Clover Configurator`, 可选安装`MultiBeast`





### [](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)%E9%BB%91%E8%8B%B9%E6%9E%9C10.13.md#%E5%88%B6%E4%BD%9C%E5%8F%AFefi%E5%90%AF%E5%8A%A8%E7%9A%84macos%E5%AE%89%E8%A3%85%E7%9B%98)制作可EFI启动的macOS安装盘 上文提到过安装盘的下载地址, 下载好了, 使用





`TransMac`制作一个安装Mac的U盘, 详细参考[[下载] El Capitan 带引导安装介质下载和制作教程](http://bbs.pcbeta.com/viewthread-1640907-1-1.html)中提到的制作U盘方法





### [](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)%E9%BB%91%E8%8B%B9%E6%9E%9C10.13.md#%E5%87%86%E5%A4%87%E4%B8%80%E4%B8%AA%E5%AE%89%E8%A3%85macos-high-sierra%E7%9A%84%E7%A1%AC%E7%9B%98%E7%A9%BA%E9%97%B4)准备一个安装macOS High Sierra的硬盘空间 你可以准备一块硬盘, SSD或HDD, 或者一个可用的分区, 硬盘必须是





**GUID**格式. 使用`DiskGenius`将硬盘或可用的分区再划出两个分区, 一个是用来引导的(ESP), 一个是用来安装MacOS系统的(HFS+)





## [](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)%E9%BB%91%E8%8B%B9%E6%9E%9C10.13.md#%E5%AE%89%E8%A3%85macos-high-sierra-10134)安装MacOS High Sierra 10.13.4 插上你制作好的U盘, 启动U盘, 会进入到Clover引导界面, 其实这个镜像中集成的Clover已经近乎完美了, 这里稍作调整.





### [](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)%E9%BB%91%E8%8B%B9%E6%9E%9C10.13.md#%E5%B1%8F%E8%94%BD%E7%8B%AC%E7%AB%8B%E6%98%BE%E5%8D%A1)屏蔽独立显卡 在





`Config - Graphics Injector`中取消`NvidiaWeb`的勾, 并勾选下面的`Intel`, 再回到安装Mac的选项, 按空格键, 进入菜单, `boot - args`中选中`Verbose`和`Set nVidia to VESA`, 接着切换到`Boot MacOS with selected options`. 其他选项含义参阅[Clover配置](https://blog.daliansky.net/clover-user-manual.html)





### [](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)%E9%BB%91%E8%8B%B9%E6%9E%9C10.13.md#%E5%BC%80%E5%A7%8B%E5%AE%89%E8%A3%85)开始安装 如果顺利的话就进入安装过程了, 安装过程很简单. 此处省略.





<blockquote>
  
> 
> 我在安装中键盘部分功能无法使用, 我只好外接鼠标完成安装, 这里吐槽下远景论坛的官方QQ群, 在里面请教问题, 无人鸟你, 经过几天的观察, 这群分明和一个死群没啥区别.
> 
> 
</blockquote>





### [](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)%E9%BB%91%E8%8B%B9%E6%9E%9C10.13.md#%E9%A9%B1%E5%8A%A8%E5%AE%8C%E5%96%84)驱动完善 系统顺利装好后, 可能出现没声音, 触摸板不能用, 不能上网等等很多问题, 就要去论坛里面一个个找了. 查到同型号的笔记本(W350ETQ是没人是知道了)K590S, 学习前辈的经验, 一个个





`kext`测试. 这里需要用到`Clover Configurator`来编辑修改`config.plist`文件, 当然修改好后, 也要将`EFI`分区挂载, 将自己修改好的配置文件和别人的`kext`驱动包放在对应的目录. 反复重启测试, 直至各项成功.





<blockquote>
  
> 
> 有时候不小心改错了, 可能再次需要使用U盘的Clover来引导进入系统. 有一些功能例如电源, 屏幕亮度完善需要涉及到DSDT的一些修改, 这个就复杂了. 我花了一两天都没有自己做好ACPI Patching, 研究了其他的示例代码, 却总是失败, 不过最后经过反复测试和前辈提供的DSDT, 我总算还是解决了电源和屏幕亮度问题. 如果有兴趣可以阅读本文末尾提到关于DSDT, ACPI相关的文章, 这里不详细讲解.
> 
> 
</blockquote>





## [](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)%E9%BB%91%E8%8B%B9%E6%9E%9C10.13.md#%E5%A4%A7%E5%8A%9F%E5%91%8A%E6%88%90)大功告成 目前在这台笔记的本大部分问题已经解决, 当然也有小部分问题是无法解决的.





### [](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)%E9%BB%91%E8%8B%B9%E6%9E%9C10.13.md#%E5%B7%B2%E8%A7%A3%E5%86%B3)已解决







  * CPU识别正确


  * 核显使用正常


  * SATA设备检测正常


  * USB2.0设备正常


  * 声卡使用正常


  * 有线网卡使用正常


  * 电源检测正常


  * 触摸板使用正常


  * Fn功能调节屏幕亮度正常


  * 摄像头识别正确


  * HDMI外界尚未测试(理论上正常)





### [](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)%E9%BB%91%E8%8B%B9%E6%9E%9C10.13.md#%E6%9C%AA%E8%83%BD%E8%A7%A3%E5%86%B3)未能解决







  * 无线网卡及蓝牙无法驱动


  * 独立显卡GTX660M无法使用


  * USB 3.0仅达到2.0 独立显卡的问题确实没办法了. 无线网卡的话, 大家可以购买其他支持Mac系统的USB网卡, 反正USB接口很多. 因此总的来说算比较完美了. 当然键盘的话, 由于是windows键盘, 可能会有些操作方面的不适应. 文中提到的所有参阅文章汇总:



  * [[下载] 【初春之献】macOS High Sierra 10.13.4 17E199 With Clover 4423修正原版镜像](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1780088)



  * [[分享] 最完美的战神k590s的黑苹果](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1485776)



  * [[下载] K590S 战神 10.8.3黑苹果指南](http://bbs.pcbeta.com/viewthread-1308539-1-1.html)



  * [[分享] 神州k590s OS X Yosemite 90%完美黑苹果 文件分享](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1555418)


  * [[教程] [授权翻译] 使用补丁修改DSDT/SSDT [DSDT/SSDT综合教程]](http://bbs.pcbeta.com/viewthread-1571455-1-1.html)


  * [[原创内容] ［2015.1.2 更新］[DSDT/SSDT视频教程] ACPI文件处理与屏蔽独显、亮度调节](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1517830)


  * [[交流] Clover介绍 及 新版 config.plist 代码作用详解.](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1423598)


  * [黑苹果引导工具Clover 配置详解- 简书](https://www.jianshu.com/p/b156b0177a24)


  * **[黑果小兵 - clover使用教程](https://blog.daliansky.net/clover-user-manual.html)**


  * [[Guide] Booting the OS X installer on LAPTOPS with Clover By RehabMan](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/)


  * **[Mac OS之程序员 - `黑苹果`](https://www.kancloud.cn/chandler/mac_os/480595)**


  * [猫叔博客](https://www.maoshu.cc/)


  * [RehabMan的github](https://github.com/RehabMan)


  * [[Guide] Using Clover to "hotpatch" ACPI By RehabMan](https://www.tonymacx86.com/threads/guide-using-clover-to-hotpatch-acpi.200137/)


  * [ACPI配置介绍 - 英文](https://clover-wiki.zetam.org/Configuration/ACPI)


  * [ACPI patching, done the easy way](https://github.com/RevoGirl/RevoBoot/wiki/ACPI-patching,-done-the-easy-way)





<blockquote>
  
> 
> 老实说, 总结起来似乎没有那么复杂, 可是做好这些竟然花了我整整三天, 真是有点累. 不过目前来看我的W350ETQ能基本正常使用Mac了也算是令人开心的. 至于到底好不好用还有待观察. 我的原文发表在[github](https://github.com/whidy/daily/blob/master/articles/W350ETQ(K590S)黑苹果10.13.md)上 * * *更新2018年6月6日 有人经常问我的clover配置. 其实我这个后来发现外接HDMI总有一个黑屏, 怎么改都没成功, 搞了两个星期也没弄好, 身心疲惫, 工作又忙, 就放下了. 不过还是有人想要我的这个配置, 我传到百度网盘了. 有兴趣的就试试看吧
> 
> 
</blockquote>





**链接：[https://pan.baidu.com/s/1RtMqwcccDf0kqrgwFJiKag](https://pan.baidu.com/s/1RtMqwcccDf0kqrgwFJiKag) 密码：t6hn**  



