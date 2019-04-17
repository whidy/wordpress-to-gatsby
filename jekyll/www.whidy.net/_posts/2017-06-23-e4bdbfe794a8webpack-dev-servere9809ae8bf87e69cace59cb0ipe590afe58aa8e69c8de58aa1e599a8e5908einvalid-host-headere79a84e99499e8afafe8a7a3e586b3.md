---
author: whidy
comments: true
date: 2017-06-23 08:44:10+00:00
layout: post
link: http://www.whidy.net/%e4%bd%bf%e7%94%a8webpack-dev-server%e9%80%9a%e8%bf%87%e6%9c%ac%e5%9c%b0ip%e5%90%af%e5%8a%a8%e6%9c%8d%e5%8a%a1%e5%99%a8%e5%90%8einvalid-host-header%e7%9a%84%e9%94%99%e8%af%af%e8%a7%a3%e5%86%b3.html
slug: '%e4%bd%bf%e7%94%a8webpack-dev-server%e9%80%9a%e8%bf%87%e6%9c%ac%e5%9c%b0ip%e5%90%af%e5%8a%a8%e6%9c%8d%e5%8a%a1%e5%99%a8%e5%90%8einvalid-host-header%e7%9a%84%e9%94%99%e8%af%af%e8%a7%a3%e5%86%b3'
title: 使用webpack dev server通过本地IP启动服务器后invalid host header的错误解决办法
wordpress_id: 2931
categories:
- IT技术
- 技术分享
tags:
- webpack
- 技术
---

最近在研究webpack,本来前阵子webpack dev server还配置的挺正常的...今天突然重新搭环境的时候跑不起来了...不知道是不是版本原因导致的,反正现象是

webpackDevServer服务器启动正常,进行localhost:9000访问正常,但是用本地的ip例如我IP是192.168.1.100,于是在浏览器中访问192.168.1.100:9000则出现了invalid host header.

那么解决这个问题也是差了不少资料.如果你存在此问题可以尝试一下方法:

首先说明环境 webpack 2.6.1 + webpackDevServer 2.5.0

我本来的webpack.config.js文件内的webpackDevServer配置如下

    
    ```javascript
    devServer: {
        contentBase: __dirname,
        compress: true,
        port: 9000,
        inline: true,
        host: '0.0.0.0'
    }
    ```


有人说要加一个

disableHostCheck: true

不过不知道这里是没有效果的

又查到说加了一个public参数,试了下就好了.所以就分享下.完整的效果是

    
    ```javascript
    devServer: {
        contentBase: __dirname,
        compress: true,
        port: 9000,
        inline: true,
        host: '0.0.0.0',
        disableHostCheck: true,
        public: '192.168.1.107'
    }
    ```


PS:后来发现用disableHostCheck: true其实也行了,大概是缓存原因没有及时看到效果,不论怎么样...出现这种问题的朋友都可以试试咯~

参考

[--host 0.0.0.0 Not working](https://github.com/webpack/webpack-dev-server/issues/882)
[I am getting an “Invalid Host header” message, when running my React app in a Webpack dev server on Cloud9.io](https://stackoverflow.com/questions/43619644/i-am-getting-an-invalid-host-header-message-when-running-my-react-app-in-a-we)
[webpack-dev-server2.4.3版本的官方说明](https://github.com/webpack/webpack-dev-server/releases/tag/v2.4.3)
[webpack-dev-server disableHostCheck导致 invalid host header](https://segmentfault.com/a/1190000009425403)
