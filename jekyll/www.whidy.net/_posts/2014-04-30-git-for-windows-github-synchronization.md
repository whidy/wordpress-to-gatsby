---
author: whidy
comments: true
date: 2014-04-30 14:51:42+00:00
template: post
link: http://www.whidy.net/git-for-windows-github-synchronization.html
slug: /git-for-windows-github-synchronization
title: 如何使用git for windows与github同步数据
wordpress_id: 2017
category: '开发'
tags:
- 技术
- 网站
---

其实,github这个东东很多经常做开发的人都应该知道,可以将自己做的demo上传维护并管理,也可以把其他人的优秀作品抓来研究学习,可谓一个很棒的网站.今天主要介绍一下**git for windows**(msysgit)与**github**同步的方法.

前几天在同事hoosin的简单介绍下,我又决定尝试好好学习利用一下github这个利器了.正巧有个朋友曾经试过失败了,希望我写个简单的操作过程,那么我接下来就简单介绍一下本地git与github数据同步的一些方法及过程.<!-- more -->



	
  1. 


## 注册一个github账号


打开[github首页](https://github.com/)就可以直接注册,依次输入**用户名**/**电子邮箱**/**密码**,点击**Sign up for GitHub**即可.

	
  2. 


### 下载[**git for windows**](http://msysgit.github.io/)(msysgit),按照正常的安装流程安装程序




	
  3. 


### 在GuiHub上**Create a new repository**


![create a new repository](http://www.whidy.net/wp-content/uploads/2014/04/create_new_repository.png)

名字随便起个,创建完成后,会出现这样一个页面(不要关闭)

![my github repositry](http://www.whidy.net/wp-content/uploads/2014/04/my_github-400x314.png)

	
  4. 


### 创建本地git管理目录


在本地硬盘上新建一个git管理目录,然后进入该目录,<del>鼠标右键**Git Init Here**,会自动生成一个隐藏目录,不用管它.再(_因为我下面将使用命令行,所以此处无需初始化该目录_)</del>右键**Git Gui**,弹出一个可视化界面,点击帮助下拉菜单,生成一个**SSH KEY**,将KEY的内容复制下来

	
  5. 


### 添加SSH KEY


在你的GitHub**用户设置**页面找到**SSH KEYS**如图,**Add SSH Key**,我这里已经添加好了就不用加了.

![add a ssh key](http://www.whidy.net/wp-content/uploads/2014/04/ssh_keys-400x251.png)

	
  6. 


### Git Bash操作介绍


根据个人习惯,当然我可能对命令行一直有好感,所以这里介绍命令行的操作方式,第3步说了页面不要关闭,此刻可以试试了.在这个目录内,右键Git Bash弹出命令行,执行第3步内容:

![git bash](http://www.whidy.net/wp-content/uploads/2014/04/git_bash-400x422.png)

	
  7. 


### 完成说明


这样就算大功告成了.(其实我这说的是基本操作...更多复杂的比如本地创建的文件上传上去,需要哪些命令,大家可以自己研究下,,,或者使用GUI界面操作,很简单的.)


等我在研究一段时间,发点高级的玩意...暂且先写这么多吧
