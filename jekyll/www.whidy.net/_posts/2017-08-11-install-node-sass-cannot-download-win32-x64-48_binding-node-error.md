---
author: whidy
comments: true
date: 2017-08-11 14:32:23+00:00
description: 搭建项目环境需要安装node-sass,经常会出现错误,提示https://github.com/sass/node-sass/releases/download/v4.5.3/win32-x64-48_binding.node无法下载,原因就是国外的东西很慢,解决办法也很简单...
template: post
draft: false
link: http://www.whidy.net/install-node-sass-cannot-download-win32-x64-48_binding-node-error.html
slug: /install-node-sass-cannot-download-win32-x64-48_binding-node-error
title: '安装node-sass的时候报错 Cannot download "https://github.com/sass/node-sass/releases/download/v4.5.3/win32-x64-48_binding.node":'
wordpress_id: 2963
category: '开发'
tags:
- nodejs
---

最近重装了系统在配置项目环境时需要用到node-sass,经常出现安装失败的情况.

以前也是又是装python又是配环境,也不知道到底是怎么瞎折腾出来的的.好不容易弄好了就没管了.

这次搞虚拟机测试了一下,有个很好的解决方案.是在github上node-sass的issues看到的,屡试不爽,当然如果你也是我这种情况可以试试.我想大部分情况都能解决吧.

先看看我的出错信息

![安装node-sass错误信息](https://www.whidy.net/wp-content/uploads/2017/08/node-sass-400x154.png)

如果你也是这样的不妨将提示中的这个[https://github.com/sass/node-sass/releases/download/v4.5.3/win32-x64-48_binding.node](https://github.com/sass/node-sass/releases/download/v4.5.3/win32-x64-48_binding.node)下载下来,存放在**C:\Users\Whidy(你的用户)\AppData\Roaming\npm-cache\node-sass\4.5.3**目录内,再尝试重新执行npm install node-sass我想应该就可以成功了吧.

当然版本不同的话会略有差异.请自行对应替换,如果你发现还是下载的很慢,我这里分享一下我上传到百度云的这个4.5.3版本的[win32-x64-48_binding.node](https://pan.baidu.com/s/1cevVaQ),然后拷贝到刚才说的目录就好了.

参考: [Install node-sass 4.5.0 failed on window 7, "Binary has a problem: Error: %1 is not a valid Win32 application.".](https://github.com/sass/node-sass/issues/1888)
