---
author: whidy
comments: true
date: 2012-06-14 14:47:37+00:00
layout: post
link: http://www.whidy.net/htpc-graphic-card-with-8-channel.html
slug: htpc-graphic-card-with-8-channel
title: HTPC显卡选购(HDMI接口支持TrueHD,LPCM等7.1声道等)
wordpress_id: 819
categories:
- IT技术
- 兴趣
- 技术分享
tags:
- 技术
- 教程
---

最近给老爸装机,因为装机主题是HTPC,那么自然离不开发热小功率小,噪音小,散热好,并且外观时尚,本来想把自己的旧电脑给老爸做HTPC,谁知我买来TT V3 BLACX的机箱发现,前置USB 3.0接口居然插不到旧主板上面,并且我的旧显卡GT240 512M GD5不支持7.1声道的所谓的次世代音频!

关注过前几天我写的一篇[装机指南(上)](/pc-diy-i5-htpc-1.html)可能会知道我本来打算自己用新的,老爸用旧的,不过由于旧的电脑对我爸来说限制太多,再三思考自己还是用旧的好了,当然今天的主题是显卡,我先不谈我装机之事,经过数日夜晚的研究探索,搜集了大量资料与大家分享,先来说说什么是次世代音频.


<blockquote>“次世代”是日本话“劣った代々”的中文译音，杜比公司（Dolby Digital）和DTS公司(Digital Theatre System)的音频最新格式，即杜比公司的TrueHD技术和DTS公司的DTS-HD技术，可以传输7.1声道或以上更高品质的音频。“次世代”音频就是无压缩编码。“次世代”功放机一般具备HDMI输入和输出接口。

杜比（Dolby）TrueHD技术
TrueHD是专为高清光盘媒体所开发的下一代无损压缩技术，配合高清晰度的影像，杜比TrueHD技术能够提供前所未有的家庭影院体验，让您能够享受与高清晰度图像一样令人惊叹的新特性:
1.100%无损的编码技术。
2.码率高达18 Mbps。
3.支持多达八个分离式24比特/96 kHz全频带声道。
4.获选为HD DVD的强制性音频标准，以及Blu-ray光盘的可选音频标准。
5.杜比TrueHD技术可以支持八个（7.1）以上的声道。

DTS-HD
DTS是“Digital Theatre System”的缩写，是“数字化影院系统”的意思，数字影院系统DTS推出的新编码格式叫DTS-HD，它以7.1声道为起步。支持1.5Mbps以上的高比特率，是现在普通DVD影碟所采用的768kbps的近两倍。取样频率范围从8-192kHz(16/24bit)。最重要的好处是能与现有的DTS解码器下兼容。
DTS HD技术与DolbyTrueHD类似，都是以7.1声道为起点，在家庭影院方面用支持次世代音效的高清播放机配合次世代的功放，能带来真正的高清娱乐体验。</blockquote>


那么其中蓝光光盘一般是1080P高清视频和7.1声道无损编码音频的.按照蓝光的规范,蓝光节目的高清音频格式有三种,分别是 LPCM,True-HD,DTS-HD MA,都能实现 7.1 声道 24-bit 192KHz 输出,其中 LPCM 属于非压缩的格式,一条 8 声道 24-bit 192KHz 的 LPCM 音轨需要占用 16.6GB/小时 左右的空间,即使是 8 声道 16-bit 48KHz 的话也要 2.76GB/小时.
由于 LPCM 占用空间较大,所以人们引入了 True-HD,DTS-HD MA 这两种无损压缩音频格式,同样是 8 声道 16-bit 48KHz DTS-HD MA/TrueHD 的码率只有 LPCM 的 1/2 左右,这意味着需要占用的空间大约是 1/2.
DTS-HD MA,TrueHD 属于专利技术,因此在早期的蓝光时代 PC 视频玩家更多的是寄望厂商的光盘集成 LPCM,这样无需专门的解码器就能实现高清音频数码输出.

所以对于一般热爱家庭影院的玩家来说,家里音响功放设备全部齐全的情况下组个HTPC,必然少不了7.1声道,然而,国内找了大量的资料,却极少有显卡参数有写是否支持7.1声道输出等信息,更加难以找到核心显卡或是集成显卡能否支持了.当然我也发现了一篇不错的文章,想要了解一下的可以看看[21款显卡决战次世代音频源码输出功能](http://www.pcpop.com/doc/0/666/666783_all.shtml),这篇文章简直就是超级精华,看来小编是费了不少心思,在此我也表示感谢!

[caption id="" align="alignnone" width="650"][![点击查看原图](http://img5.pcpop.com/ArticleImages/0X0/1/1973/001973171.jpg)](http://img5.pcpop.com/ArticleImages/0X0/1/1973/001973171.jpg) 显卡支持情况一览表[/caption]

也附上方便大家直接查阅.

那么关于集成显卡究竟能不能支持呢?先来说说Intel处理器的i3,i5这两款CPU自带的核心显卡是支持硬解码的.如果不信可以参考<<[i3/i5完美HTPC 影院电脑客厅为王](http://hb.qq.com/a/20100706/001954.htm)>>.而另一方面关于APU硬解码的文章真是太少了.我只能负责任的告诉大家除了上图说明了这些AMD独立显卡支持次世代音频,所有的HD5000以上的AMD独立显卡都是支持的,可能部分HD 4000的显卡也支持(可不是Intel 的HD 4000!这里不要混淆了),如果不信可以参考此文<<[AMD显卡宽域技术与7.1声道输出技术解析](http://diy.pconline.com.cn/graphics/reviews/1009/2210661_1.html)>>,以及[http://whirlpool.net.au/wiki/rmp_sg_whirlpoolpcs_htpc](http://whirlpool.net.au/wiki/rmp_sg_whirlpoolpcs_htpc) 找到底部**HTPC Considerations**内


<blockquote>

> 
> ### Blu-ray
> 
> 

> 
> 
	
>   * All listed HTPC builds are capable of smooth blu-ray& HDTV playback, hence you can upgrade or downgrade optical drive in any build depending on your blu-ray requirements.
> 
	
>   * Boards with 780g, 785g and 790g chipsets support stereo LPCM audio and bitstream Dolby Digital/DTS 5.1 over HDMI. If you need 8-channel LPCM support (true HD via an amp), chose a build based on Nvidia or Intel integrated GPU, a discrete GPU, or install a sound card that supports bitstreaming over HDMI.
> 
	
>   * Software that comes with blu-ray players usually only supports stereo sound. You need to purchase software like PowerDVD 9 or Arcsoft Total Media Theatre to get TrueHD.
> 
	
>   * There is no support for real-time blu-ray playback under linux, however blu-ray rips can be played.
> 

</blockquote>


标红部分写的很清楚了~

至此我依然没有找到A8 3850 的HD 6550D显卡能不能输出8通道音频.虽然从上面那句话得出结论应该是支持的,另外国外还有一个老外的帖子,不知道是不是意味着的确是支持的.详细请看[http://forum.xbmc.org/showthread.php?tid=124592&page=5](http://forum.xbmc.org/showthread.php?tid=124592&page=5)

来自网友HeGetsIt:


<blockquote>I would love to get this to work; but, so far I'm having no such luck.

I have an AMD A8-3850 APU which includes a Radeon HD 6550D attached via HDMI to a Sony STR-DH810 AVR. I'm running 64Windows7SP1 and version 12.2 of Catalyst CC. I followed bluray's link in his blu-ray in 1080p with dts-hd and truehd thread, and, installed the Realtek Driver and ATI HDMI Device file and I've tried both DD and bluray's version of XBMC+HD Audio.

I have both DTS-HD and Dolby TrueHD listed as supported formats and my sound properties are identical to bluray's screenshot in post #3 of this thread. Within xbmc, my video and audio settings are set according to bluray's instructions.

Having said all that, when trying to play blu-ray rips to MKVs and M2TS files with DTS-HD, xbmc reports the audio failed to initialize and there is no sound; when trying to play blu-ray rips to MP4 and M2TS files with TrueHD AC-3, the AVR reports LPCM and the sound pops and crackles.</blockquote>


当然紧跟他楼下的便是回复,貌似这样来说A8 3850的CPU应该是支持的.

好了,这几天研究装机,研究HTPC,研究HDMI等问题累死了...装机下篇等有时间再写罢,最后附上几篇文章,方便用户对APU的相关资料有一定了解.

[全民融聚AMD A8-3850处理器全球首测](http://cd.beareyes.com.cn/2/lib/201106/30/20110630190_0.htm)

[AMD A8-3850 With Radeon HD 6550D Running On Linux](http://www.phoronix.com/scan.php?page=article&item=amd_a83850_graphics&num=1%20%20%20)

以及我在网上找到的一个讨论帖,也是我在找的问题,不过貌似没有详细准确的回复,

[请问大侠什么显卡有次世代音频输出啊？不追求性能。](http://we.pcinlife.com/thread-1818649-1-1.html)

还有我在ZOL上发的帖子

[组HTPC的话AMD平台选U怎么选?用A8还是641?](http://diybbs.zol.com.cn/11/11_104124.html)

好了不早了,睡觉...看来我又要成为HTPC高手高手高高手了!偷笑...
