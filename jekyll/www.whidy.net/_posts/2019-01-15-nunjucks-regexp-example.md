---
author: whidy
comments: true
date: 2019-01-15 07:49:25+00:00
excerpt: 我在使用egg.js时，他用的模板引擎是Nunjucks，其中有个地方需要用到正则，可是官方文档基本上写了跟没写一样，官方的[正则表达式](https://mozilla.github.io/nunjucks/templating.html#regular-expressions)，于是我便去找例子了。
template: post
link: http://www.whidy.net/nunjucks-regexp-example.html
slug: /nunjucks-regexp-example
title: Nunjucks使用正则表达式示例
wordpress_id: 3209
category: '开发'
tags:
- 技术
---

<blockquote>
  
> 
> 我在使用egg.js时，他用的模板引擎是Nunjucks，其中有个地方需要用到正则，可是官方文档基本上写了跟没写一样，官方的[正则表达式](https://mozilla.github.io/nunjucks/templating.html#regular-expressions)，于是我便去找例子了。
> 
> 
</blockquote>





## 正则表达式





在Nunjucks中使用正则表达式的示例：




    
    ```html
    {% set regExp = r/^foo.*/g %}
    {% if regExp.test('foo') %}
      Foo in the house!
    {% endif %}
    ```





那么这个就会被正常显示。其他的表达式也是可以的。例如：




    
    ```html
    <!-- 有个后台存储的未验证的手机号码(mobile)在前端显示，如果格式正确则显示，不正确则显示“暂无” -->
    {% set regExp = r/^\d{11}$/g %}
    <span>号码：{{mobile if regExp.test(mobile) else '暂无'}}</span>
    ```





这两个例子应该看得懂吧。正则这块我并没有看源码，因为搜索出来了，我这里参考的[regex exmaple?](https://github.com/mozilla/nunjucks/issues/891)





后来发现其实很多方法文档并没有写出来，这时候可能真的需要看看源码了，有兴趣的话可以阅读下filter的源码[https://github.com/mozilla/nunjucks/blob/master/nunjucks/src/filters.js](https://github.com/mozilla/nunjucks/blob/master/nunjucks/src/filters.js)



