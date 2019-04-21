---
author: whidy
comments: true
date: 2018-01-14 09:44:38+00:00
description: Linux(CentOS6)下安装Nodejs,删除Nodejs,升级Nodejs遇到的一些问题,以及相关解决方案的介绍
template: post
draft: false
link: http://www.whidy.net/how-to-install-upgrade-remove-nodejs-on-linux.html
slug: /how-to-install-upgrade-remove-nodejs-on-linux
title: Linux下无法正常安装（升级）和删除Nodejs的解决方法
wordpress_id: 3061
category: '开发'
tags:
- 技术
- 网站
---

接着上次说，自从买了VPS后就没闲着，总想要充分利用起来倒腾点东西。于是决定安装nodejs搭建web服务器等，如今nodejs稳定版本已经更新到8.x了，因此我就试着装一下8.x吧，没想到又遇到了坑，一搞搞了好几天。

我的操作系统是CentOS 6 64 Bit的，我查阅了[Nodejs官方升级文档](https://nodejs.org/en/download/package-manager/)（包含各种可支持的系统），针对我的系统需要分别执行以下几条命令：

    
    ```bash
    curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash -
    ```



    
    ```bash
    sudo yum -y install nodejs
    ```


当然你也许需要通过以下命令额外安装构建工具：

    
    ```bash
    sudo yum install gcc-c++ make
    # or: sudo yum groupinstall 'Development Tools'
    ```


如果其他系统则可以参考文档中其他内容。

在这里我就遇到坑了（可能存在该情况较少，所以稍后具体解决放在文章最后来说）。上面第一条应该是静默指定使用8.x的资源，便于安装时采用这个而不是yum自己原来的远程仓，不知道这个解释对不对。

我反复试过了，命令明明提示请执行 **sudo yum -y install nodejs** 来安装nodejs8.x，却一直安装的是6.x，难道是依赖问题？找不出原因的我，没有办法只能找其他安装途径，于是发现了第二种安装办法，手动获取最新的安装包，并进行解压缩安装，可能依赖Python2.7以上版本，我一步步来说。

如果是仅手动安装Nodejs8.x，执行以下命令：

    
    ```bash
    yum install gcc-c++ openssl-devel
    cd /usr/local/src
    wget http://nodejs.org/dist/v8.9.4/node-v8.9.4.tar.gz
    tar zxvf node-v8.9.4.tar.gz
    (cd into extracted folder: ex "cd node-v8.9.4.tar.gz")
    ./configure
    make
    make install
    ```


顺利的话应该不会有什么问题，大概会过一段时间，稍微有点长，就提示安装好了，可以执行

    
    ```bash
    node -v
    ```


来查看是否是8.x，如果好了，基本上关于安装部分就大功告成了。如果没好，太惨了，跟Python有关系的话，请查看Linux下[Python安装升级心得](http://www.whidy.net/linux-install-upgrade-python-2-7.html)。

接着我们来看看删除，因为你已经安装了一个低版本，需要升级，那就是要先删除旧版本了，<del>nodejs应该是向下兼容的，所以我就没有去研究可能闲着蛋疼才会去研究如果保存多个版本nodejs，</del>当然在新版中可能会存在部分旧的功能废除而造成异常，虽然一般来说升级利大于弊，不过还是要考虑老项目环境是否要升级！如果你是闲着蛋疼的人，必有理由说服我，请在下方留言。差点跑题，删除命令简直是太简单了。

    
    ```bash
    sudo yum remove nodejs
    ```


然后按提示输入y，回车后很快就删了。一切删除操作都是令人兴奋的。。。

其实，我在安装过程中远没有那么轻松，否则也不会折腾几天了，一个是版本错误，一个是Python升级。版本问题，后来差了很多资料才发现，原来是yum缓存问题导致。如果遇到和我类似的问题，请尝试以下命令：

    
    ```bash
    rm -f /etc/yum.repos.d/nodesource-el.repo
    yum clean all
    yum -y remove nodejs
    yum -y install nodejs
    ```


汇总下本文参阅的相关文章：



 	
  1. [Nodejs官方文档，通过包管理安装Nodejs](https://nodejs.org/en/download/package-manager/)

 	
  2. [Centos下手动安装Nodejs的方法](https://serverfault.com/questions/299288/how-do-you-install-node-js-on-centos)

 	
  3. [无法在Yum仓下安装正确的Nodejs版本](https://github.com/nodesource/distributions/issues/340)（和刚才示例的代码类似，都是清除缓存，不过对我无效）

 	
  4. [CentOS下使用nodejs7.x的包进行安装却安装成了6.9.5](https://github.com/nodesource/distributions/issues/421)（针对我的有效方案）

 	
  5. [如何通过Linux命令删除Nodejs](https://stackoverflow.com/questions/5650169/uninstall-node-js-using-linux-command-line)


所以我呢，其实就是应该遇到版本不对的情况就尝试清除缓存，再用官方命令进行安装就好了~

我想既然是Yum仓库缓存的问题，除了Nodejs，别的包也许也会有类似情况吧，如果也发现了选择了需要的版本后依然装的是旧版的，又和依赖没什么关系，就试试清除缓存吧 :)
