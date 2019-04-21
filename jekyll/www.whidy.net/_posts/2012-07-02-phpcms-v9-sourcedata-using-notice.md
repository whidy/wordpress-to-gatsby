---
author: whidy
comments: true
date: 2012-07-02 03:26:21+00:00
template: post
draft: false
link: http://www.whidy.net/phpcms-v9-sourcedata-using-notice.html
slug: /phpcms-v9-sourcedata-using-notice
title: PHPCMS数据源功能使用注意事项
wordpress_id: 851
category: '开发'
tags:
- 技术
---

上次很抱歉的,上次写了一篇关于PHPCMS V9通过数据源生成代码调用至DISCUZ论坛上的方法[<<PHPCMS利用数据源对网站数据调用至其他网站方法>>](/phpcms-data-website-to-website.html),但是后来发现有个问题,就是论坛上出现了一个链接地址的问题,经过大量搜索,无果,决定自己想办法解决.

首先说一下问题状况吧.

列表中的地址并非直接引用的外链数据源地址,而是

    
    ```html
    http://b.net/"http://h.net/6-8540-1.html/"
    ```


这又不像其他网站外链提示是否安全再进行正常访问,而这个地址是完全无法用的.我最早考虑的解决方案是因为论坛域名固定,那么长度固定,所以截取前面http://b.net/"这段,但是貌似后面有个双引号也是无法正常访问的.

这样我想到另一个方法,自动找到h.net,并且通过正则表达式判断html为结束段,PHP string方法很强大,都是可以用的,但是觉得这个方法太笨重了.写起来不容易.最终决定在网上找到好的办法,搜索了discuz外链不正确,discuz外链地址等关键字无果.唯一找到一个沾边的内容,说是修改include/discuzcode.func.php文件内`function parseurl($url, $text)`这个函数

但是,我试过了,完全是两码事,于是放弃了,我尝试发帖的时候外链试试,发现会自动添加[url][/url],是这在模版上加了个,但是HTML和BBS语言在不同的位置上也是不能用的,思考了很久,最后决定试试修改数据源的代码,很巧的事情发生了,我将数据源内的代码改成了

    
    ```html
    <h3>行业最新产品</h3>
    {loop $data $k $v}
        <li>· <a href={$v[url]}>{$v[title]}</a></li>
    {/loop}
    ```


注意,跟之前的不同,a标签内的双引号我去掉了,就成功了,论坛首页刷新一看,完全正常.至此这个问题就解决了.

PS:我也试过在数据源的这段代码内添加[url]当然这个是完全不成立的还是那句话,HTML是HTML,BBS CODES是BBS CODES...
