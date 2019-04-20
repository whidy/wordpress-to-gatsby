---
author: whidy
comments: true
date: 2012-05-31 04:55:58+00:00
template: post
link: http://www.whidy.net/seagate-3t-install-os.html
slug: /seagate-3t-install-os
title: 希捷新3T硬盘老主板也能装系统
wordpress_id: 784
category: '硬件'
tags:
- 技术
- 教程
---

无奈我的几个硬盘都已经满了除了双系统的还剩5G空间,我这2200G的硬盘剩下不到20G了...憋屈了很久,想买硬盘,可是硬盘迟迟不降价.今天突然看到中关村一篇文章,叫做[硬盘价格轰然倒塌](http://memory.zol.com.cn/297/2975625.html),于是忍不住偷笑,这小编肯定又要挨骂了.进去看看果然不出所料,不过这次很惊喜我一直想买的3T降到1000以内了,不过,之前了解到老主板只能支持2T硬盘做系统盘,于是乎对于3T硬盘估计只能做存储盘了.

不过紧接着看到一篇文章,感到惊喜,这篇同样来自中关村的文章[3TB硬盘首破千元 性能价格PK谁最出众](http://memory.zol.com.cn/297/2972767_all.html),不仅了解到了硬盘性能简单比较和评测,同样也学到了3TB硬盘如何安装到旧主板上.这里我就直接转载过来备用收藏了吼吼...<!-- more -->

以下内容摘自中关村...详细请见[http://memory.zol.com.cn/297/2972767_all.html](http://memory.zol.com.cn/297/2972767_all.html)

[caption id="" align="alignnone" width="500"]![3TB硬盘~~~~~ ](http://2a.zol-img.com.cn/product/83_500x2000/78/ce0e54f9TidPM.jpg) 3TB硬盘~~~~~[/caption]

在普通的Win7/XP[操作系统](http://detail.zol.com.cn/os_index/subcate121_list_1.html)下，3TB[硬盘](http://memory.zol.com.cn/)采用传统分区工具，如果没有特殊工具或者BIOS的帮助，有高达746.52GB的硬盘容量无法使用。

**传统MBR分区只能识别[2TB](http://detail.zol.com.cn/hard_drives/index266692.shtml)空间，3TB硬盘有多达746GB空间无法识别**
微软在开发Windows Vista/7/8操作系统的时候，就充分考虑了大容量硬盘的完整支持问题，针对目前的MBR和GPT两种主流硬盘格式，毅然抛弃MBR格式，选择更先进的GPT格式。在GPT格式中，不但可以整建制的3TB容量作为系统盘；还可以进行多个分区，选择其中一个区作为系统盘，其他硬盘分区根据客户需要划分容量使用，3TB硬盘物尽其用。
除了BIOS的限制，操作系统对于新3TB硬盘也存在许多弊端：
<table cellpadding="0" width="100%" align="center" cellspacing="0" border="1" >
<tbody >
<tr >

<td bgcolor="#c0c0c0" align="center" height="25" width="33%" >
</td>

<td bgcolor="#c0c0c0" align="center" height="25" width="33%" >数据盘
</td>

<td bgcolor="#c0c0c0" align="center" height="25" width="34%" >系统盘
</td>
</tr>
<tr >

<td bgcolor="#c0c0c0" align="center" height="25" width="33%" >Windows XP 32bit
</td>

<td width="33%" align="center" height="25" >不支持 GPT分区
</td>

<td width="34%" align="center" height="25" >不支持 GPT分区
</td>
</tr>
<tr >

<td bgcolor="#c0c0c0" align="center" height="23" width="33%" >Windows XP [64bit](http://detail.zol.com.cn/vga_index/subcate6_list_s257_1.html)
</td>

<td width="33%" align="center" height="23" >支持 GPT分区
</td>

<td width="34%" align="center" height="25" >不支持 GPT分区
</td>
</tr>
<tr >

<td bgcolor="#c0c0c0" align="center" height="27" width="33%" >Windows Vista 32bit
</td>

<td width="33%" align="center" height="27" >支持 GPT分区
</td>

<td width="34%" align="center" height="25" >不支持 GPT分区
</td>
</tr>
<tr >

<td bgcolor="#c0c0c0" align="center" height="25" width="33%" >Windows Vista [64bit](http://detail.zol.com.cn/vga_index/subcate6_list_s257_1.html)
</td>

<td width="33%" align="center" height="25" >支持 GPT分区
</td>

<td width="34%" align="center" height="25" >GPT分区需要UEFI BIOS
</td>
</tr>
<tr >

<td bgcolor="#c0c0c0" align="center" height="25" width="33%" >Windows 7 32bit
</td>

<td width="33%" align="center" height="25" >支持 GPT分区
</td>

<td width="34%" align="center" height="25" >不支持 GPT分区
</td>
</tr>
<tr >

<td bgcolor="#c0c0c0" align="center" height="25" width="33%" >Windows 7 64bit
</td>

<td width="33%" align="center" height="25" >支持 GPT分区
</td>

<td width="34%" align="center" height="25" >GPT分区需要UEFI BIOS
</td>
</tr>
<tr >

<td bgcolor="#c0c0c0" align="center" height="25" width="33%" >Windows 8 64bit
</td>

<td width="33%" align="center" height="25" >支持 GPT分区
</td>

<td width="34%" align="center" height="25" >GPT分区需要UEFI BIOS
</td>
</tr>
<tr >

<td bgcolor="#c0c0c0" align="center" height="25" width="33%" >Linux
</td>

<td width="33%" align="center" height="25" >支持 GPT分区
</td>

<td width="34%" align="center" height="25" >GPT分区需要UEFI BIOS
</td>
</tr>
</tbody>
</table>
![单碟1.5TB诞生 细数3TB硬盘分区技巧 ](http://2f.zol-img.com.cn/product/83_500x2000/305/ce28ZwGQLyQ.jpg)

![单碟1.5TB诞生 细数3TB硬盘分区技巧 ](http://2d.zol-img.com.cn/product/83_500x2000/309/ce0aHoUpj9pdE.jpg)

所以我们右键3TB的磁盘，出现的对话框中选择转换成GPT磁盘就可以了。

**系统通过转换磁盘来支持更大容量硬盘**

**转换完后的磁盘显示**
通过GPT的转换，系统自动识别了3TB硬盘，此时实际容量为2794.39GB。这也就可以在3TB硬盘上正常存储数据了。这种方法适合将3TB硬盘作为仓库盘使用，方法简单易懂。


### 附录：3TB硬盘分区之MBR格式篇


[caption id="" align="alignnone" width="500"]![希捷硬盘工具](http://2e.zol-img.com.cn/product/83_500x2000/860/ceJmPWPyCiu.jpg) 希捷硬盘工具[/caption]

![希捷硬盘工具安装界面](http://2c.zol-img.com.cn/product/83_500x2000/858/cefTJ8qGljeu6.jpg)

![希捷硬盘工具](http://2a.zol-img.com.cn/product/83_500x2000/868/cehL61Fybq3E.jpg)

![希捷硬盘工具](http://2a.zol-img.com.cn/product/83_500x2000/880/ceQvyye9TRHDQ.jpg)

![希捷硬盘工具](http://2b.zol-img.com.cn/product/83_500x2000/887/ceFNaZSHBgmQ.jpg)

![希捷DiscWizard软件“分配空间”](http://2e.zol-img.com.cn/product/83_500x2000/902/cez72Ufrv72qE.jpg)

![希捷硬盘工具模拟另一块硬盘](http://2a.zol-img.com.cn/product/83_500x2000/916/ce0ho7zb6SZcA.jpg)

![硬盘工具](http://2c.zol-img.com.cn/product/83_500x2000/918/ceb3ul5EUnsc.jpg)

我们之前提到了早期32位Win7和WinXP[操作系统](http://detail.zol.com.cn/os_index/subcate121_list_1.html)不能识别3TB[硬盘](http://memory.zol.com.cn/)，GPT硬盘格式+手动操作UEFI BIOS+64位操作系统等等一系列要求对于普通用户来说实在麻烦，并且大量早前购买的[主板](http://mb.zol.com.cn/)并没有UEFI BIOS。为此希捷专门开发了一款软件，针对希捷3TB或者更大容量的硬盘无法安装系统使用，操作界面非常简单，下面就来详细介绍一下希捷3TB硬盘的破解方法。
首先我们需要从希捷官网下载一个[**DiscWizard工具**](http://www.seagate.com/staticfiles/support/downloads/discwizard/DiscWizardSetup-14387.zh-cn.exe)。

**希捷DiscWizard软件安装界面**

按照步骤下一步，直到“完成”
点击希捷DiscWizard软件进行安装，选择第一项安装“Disc DiscWizard”，接着按步骤点击“下一步”，直到“完成”，即可完成安装。

**选择“扩展容量管理器”**
开启希捷DiscWizard软件后，开始自动扫描所有磁盘，选择“扩展容量管理器”。

**选择右下角的“分配空间”按钮**

**希捷DiscWizard软件“分配空间”正在运行**

**通过软件模拟出另外一块硬盘，需要选择MBR或者GPT格式**
通过20秒左右的等待，我们发现一只没有被识别的700多GB的容量限制已经被解禁。然后用户可以进去磁盘管理器进行分区。

**被模拟出的746.52GB空间**
在磁盘管理其中，我们发现之前的3TB硬盘被分割成两块单独的硬盘，之后可以右键新建磁盘分区进行使用，不过分区格式依然为MBR。

**DiscWizard软件将多余的容量虚拟成SCSI硬盘运行**
早在3TB硬盘问世之前，对现有BIOS系统的扩展性造成了一些恐慌，不过随着3TB硬盘的不断成熟，其实问题很容易解决。除了希捷的解决方案以外，不少高端主板均提供了破解3TB硬盘容量的软件，如技嘉的3TB+ Unlock、华硕Disk Unlocker软件均可以实现全部容量，所以随着主板BIOS的升级以及更多破解软件的发布，为来硬盘的容量增长将不再受到限制。
**小贴士：**[希捷硬盘](http://detail.zol.com.cn/hard_drives_index/subcate2_164_list_1.html)的解决方案 – DiscWizard无论是在WinXP还是windows 7 下，无论主板是否BIOS支持UEFI，利用希捷的DiscWizard工具，都可以实现让3TB希捷硬盘做为数据盘或者系统盘。

好了就说这么多了...这几天小小失踪几天...
