---
author: whidy
comments: true
date: 2017-06-26 14:57:10+00:00
excerpt: 今天要说的就是这个插件Settings Sync,一个可以在github上面通过gist仓来同步用户的vscode的配置包括插件,settings等信息的好插件
template: post
link: http://www.whidy.net/visual-studio-code-settings-sync-introduction.html
slug: /visual-studio-code-settings-sync-introduction
title: Visual Studio Code 设置同步到github的插件介绍及使用方法(Settings Sync)
wordpress_id: 2929
category: '开发'
tags:
- VSCode
- 技术
- 教程
---

最近基本上习惯了用VSCODE进行开发了.最主要的感觉就是查找JS里面函数定义和引用很方便.还有可能是装逼心理... :roll:

一开始不知道怎么备份VSCODE的配置,傻乎乎的把要用的插件抄下来,还有用户settings拷贝出来.每次换了电脑或者重装系统什么的都要重新备份.虽然来回调整的概率很低,但是突然哪天需要同步设置什么的就很麻烦了~至少我是在初期经常鼓捣这个编辑器,而且办公在家和公司是不同的设备~所以觉得还是很有必要的~

于是我今天要说的就是这个插件**Settings Sync**

官方都是英文的,不过还算简单,我把步骤简化一下.

1.安装插件并重启VSCODE就不用说了

![安装Settings Sync](https://www.whidy.net/wp-content/uploads/2017/06/00-400x264.png)

2.重启后按快捷键 **alt+shift+u** (这里假设你第一次用)

它会弹出一个窗口对应的是github上面的创建个人gist的页面,如果未登录请先登录github.

![github创建gist来存储设置](https://www.whidy.net/wp-content/uploads/2017/06/01-400x445.png)

保存后会生成一个key

![请牢记token id,后面将会用到](https://www.whidy.net/wp-content/uploads/2017/06/02-400x189.png)

3.切回到vscode,他会有个输入区,就是存放刚才生成的key

![输入刚才生成的key](https://www.whidy.net/wp-content/uploads/2017/06/03-400x75.png)

然后理论上他就开始对你本机的配置进行一个扫描上传了.至此上传工作完成.

接下来我们到另一台电脑上了下载配置.同样的先安装**Settings Sync**插件,并重新加载.

然后按快捷键alt+shift+d,就应该会弹出一个输入框,请在这里输入之前保存下来的key(GIST ID),回车后将会自动下载之前上传的配置.

那么下载完成后,你这台电脑修改了相关配置再次上传就好了.是不是感觉方便多了~

其他的说明,如果在输入gist id写错了,读取不到的情况下,大概需要重置设置,按F1,输入sync,这里有重置选项.试试看~

![重置sync的gist配置信息等](https://www.whidy.net/wp-content/uploads/2017/06/04.png)

还有些其他的功能例如自动上传下载等等,不是很常用,大家可以自行看看官方文档,基本的使用方法就是这样了,我写的如果有问题或者哪里不明白的可以留言- -.

下面是官方说明

[http://shanalikhan.github.io/2015/12/15/Visual-Studio-Code-Sync-Settings.html](http://shanalikhan.github.io/2015/12/15/Visual-Studio-Code-Sync-Settings.html)

插件地址

[https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync)



* * *



2018年1月15日补充
有朋友留言说Settings Sync不能同步插件,我刚测试过是可以同步插件的哦~按Alt+Shift+D后左下角可以看到同步的进度,例如下图:

![Settings Sync插件同步](https://www.whidy.net/wp-content/uploads/2018/01/SyncExt.png)
