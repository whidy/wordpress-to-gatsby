---
author: whidy
comments: true
date: 2018-04-21 16:10:20+00:00
excerpt: '看到一篇Implementing an Infinite Scroll with Vue.js, 觉得挺实用的就看了下, 顺便简单翻译了一下给需要的人参考.

  从这个项目中可以加深对Vue的生命周期的理解, 何时开始axios请求, 如何结合Vue使用原生js来写scroll事件等等, 我这里主要是对原文的重点提取和补充'
layout: post
link: http://www.whidy.net/infinite-scroll-vuejs-demo.html
slug: infinite-scroll-vuejs-demo
title: Vue下滚动到页面底部无限加载数据Demo
wordpress_id: 3143
categories:
- IT技术
- Javascript
- 原创翻译
- 技术分享
- 精彩分享
tags:
- VSCode
- 技术
- 教程
- 网站
---

# Vue下滚动到页面底部无限加载数据Demo




<blockquote>看到一篇[Implementing an Infinite Scroll with Vue.js](https://alligator.io/vuejs/implementing-infinite-scroll/), 觉得挺实用的就看了下, 顺便简单翻译了一下给需要的人参考.

**从这个项目中可以加深对Vue的生命周期的理解, 何时开始axios请求, 如何结合Vue使用原生js来写scroll事件等等**, 我这里主要是对原文的重点提取和补充</blockquote>




## [](https://github.com/whidy/infinite-scroll-vuejs#%E6%9C%AC%E6%96%87%E6%8A%80%E6%9C%AF%E8%A6%81%E7%82%B9)本文技术要点





 	
  * `Vue`生命周期

 	
  * `axios`简单用法

 	
  * `moment.js`格式化日期

 	
  * 图片懒加载

 	
  * 结合原生js来写`scroll`事件

 	
  * 请求节流




## [](https://github.com/whidy/infinite-scroll-vuejs#%E5%88%9B%E5%BB%BA%E9%A1%B9%E7%9B%AE)创建项目


首先创建一个简单的vue项目




    
    <span class="pl-c"># vue init webpack-simple infinite-scroll-vuejs</span>





然后安装项目所需要用的一些插件




    
    <span class="pl-c"># npm install axios moment</span>







## [](https://github.com/whidy/infinite-scroll-vuejs#%E5%88%9D%E5%A7%8B%E5%8C%96%E7%94%A8%E6%88%B7%E6%95%B0%E6%8D%AE)初始化用户数据


项目搭建完后, 跑起来看看




    
    <span class="pl-c"># npm run dev</span>





打开`http://localhost:8080`无误后, 我们开始修改代码, 先看看获取用户数据这块,




    
    <<span class="pl-ent">script</span>>
    <span class="pl-s1"><span class="pl-k">import</span> <span class="pl-smi">axios</span> <span class="pl-k">from</span> <span class="pl-s"><span class="pl-pds">'</span>axios<span class="pl-pds">'</span></span></span>
    <span class="pl-s1"><span class="pl-k">import</span> <span class="pl-smi">moment</span> <span class="pl-k">from</span> <span class="pl-s"><span class="pl-pds">'</span>moment<span class="pl-pds">'</span></span></span>
    <span class="pl-s1"><span class="pl-k">export</span> <span class="pl-c1">default</span> {</span>
    <span class="pl-s1">  name<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>app<span class="pl-pds">'</span></span>,</span>
    <span class="pl-s1">  <span class="pl-c">// 创建一个存放用户数据的数组</span></span>
    <span class="pl-s1">  <span class="pl-en">data</span>() {</span>
    <span class="pl-s1">    <span class="pl-k">return</span> {</span>
    <span class="pl-s1">      persons<span class="pl-k">:</span> []</span>
    <span class="pl-s1">    }</span>
    <span class="pl-s1">  },</span>
    <span class="pl-s1">  methods<span class="pl-k">:</span> {</span>
    <span class="pl-s1">    <span class="pl-c">// axios请求接口获取数据</span></span>
    <span class="pl-s1">    <span class="pl-en">getInitialUsers</span>() {</span>
    <span class="pl-s1">      <span class="pl-k">for</span> (<span class="pl-k">var</span> i <span class="pl-k">=</span> <span class="pl-c1">0</span>; i <span class="pl-k"><</span> <span class="pl-c1">5</span>; i<span class="pl-k">++</span>) {</span>
    <span class="pl-s1">        <span class="pl-smi">axios</span>.<span class="pl-c1">get</span>(<span class="pl-s"><span class="pl-pds">`</span>https://randomuser.me/api/<span class="pl-pds">`</span></span>).<span class="pl-en">then</span>(<span class="pl-smi">response</span> <span class="pl-k">=></span> {</span>
    <span class="pl-s1">          <span class="pl-c1">this</span>.<span class="pl-smi">persons</span>.<span class="pl-c1">push</span>(<span class="pl-smi">response</span>.<span class="pl-c1">data</span>.<span class="pl-smi">results</span>[<span class="pl-c1">0</span>])</span>
    <span class="pl-s1">        })</span>
    <span class="pl-s1">      }</span>
    <span class="pl-s1">    },</span>
    <span class="pl-s1">    <span class="pl-en">formatDate</span>(<span class="pl-smi">date</span>) {</span>
    <span class="pl-s1">      <span class="pl-k">if</span> (date) {</span>
    <span class="pl-s1">        <span class="pl-k">return</span> <span class="pl-en">moment</span>(<span class="pl-c1">String</span>(date)).<span class="pl-en">format</span>(<span class="pl-s"><span class="pl-pds">'</span>MM/DD/YYYY<span class="pl-pds">'</span></span>)</span>
    <span class="pl-s1">      }</span>
    <span class="pl-s1">    },</span>
    <span class="pl-s1">  <span class="pl-en">beforeMount</span>() {</span>
    <span class="pl-s1">    <span class="pl-c">// 在页面挂载前就发起请求</span></span>
    <span class="pl-s1">    <span class="pl-c1">this</span>.<span class="pl-en">getInitialUsers</span>()</span>
    <span class="pl-s1">  }</span>
    <span class="pl-s1">}</span>
    <span class="pl-s1"><span class="pl-k"><</span><span class="pl-k">/</span>script<span class="pl-k">></span></span>







<blockquote>这里原作者也专门提醒, **完全没有必要也不建议在加载页面的时候请求5次, 只是这个接口一次只能返回1条数据, 仅用于测试才这样做的.** 当然我这里也可以通过Mock来模拟数据, 就不详细说了~</blockquote>


接下来来写模板结构和样式, 如下:




    
    <<span class="pl-ent">template</span>>
      <<span class="pl-ent">div</span> <span class="pl-e">id</span>=<span class="pl-s"><span class="pl-pds">"</span>app<span class="pl-pds">"</span></span>>
        <<span class="pl-ent">h1</span>>Random User</<span class="pl-ent">h1</span>>
        <<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>person<span class="pl-pds">"</span></span> <span class="pl-e">v-for</span>=<span class="pl-s"><span class="pl-pds">"</span>(person, index) in persons<span class="pl-pds">"</span></span> :<span class="pl-e">key</span>=<span class="pl-s"><span class="pl-pds">"</span>index<span class="pl-pds">"</span></span>>
          <<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>left<span class="pl-pds">"</span></span>>
            <<span class="pl-ent">img</span> :<span class="pl-e">src</span>=<span class="pl-s"><span class="pl-pds">"</span>person.picture.large<span class="pl-pds">"</span></span> <span class="pl-e">alt</span>=<span class="pl-s"><span class="pl-pds">"</span><span class="pl-pds">"</span></span>>
          </<span class="pl-ent">div</span>>
          <<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>right<span class="pl-pds">"</span></span>>
            <<span class="pl-ent">p</span>>{{ person.name.first}} {{ person.name.last }}</<span class="pl-ent">p</span>>
            <<span class="pl-ent">ul</span>>
              <<span class="pl-ent">li</span>>
                <<span class="pl-ent">strong</span>>Birthday:</<span class="pl-ent">strong</span>> {{ formatDate(person.dob)}}
              </<span class="pl-ent">li</span>>
              <<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>text-capitalize<span class="pl-pds">"</span></span>>
                <<span class="pl-ent">strong</span>>Location:</<span class="pl-ent">strong</span>> {{ person.location.city}}, {{ person.location.state }}
              </<span class="pl-ent">div</span>>
            </<span class="pl-ent">ul</span>>
          </<span class="pl-ent">div</span>>
        </<span class="pl-ent">div</span>>
      </<span class="pl-ent">div</span>>
    </<span class="pl-ent">template</span>>
    
    <<span class="pl-ent">style</span> <span class="pl-e">lang</span>=<span class="pl-s"><span class="pl-pds">"</span>scss<span class="pl-pds">"</span></span>>
    <span class="pl-s1"><span class="pl-e">.person</span> {</span>
    <span class="pl-s1">  <span class="pl-c1">background</span>: <span class="pl-c1">#ccc</span>;</span>
    <span class="pl-s1">  <span class="pl-c1">border-radius</span>: <span class="pl-c1">2<span class="pl-k">px</span></span>;</span>
    <span class="pl-s1">  <span class="pl-c1">width</span>: <span class="pl-c1">20<span class="pl-k">%</span></span>;</span>
    <span class="pl-s1">  <span class="pl-c1">margin</span>: <span class="pl-c1">0</span> <span class="pl-c1">auto</span> <span class="pl-c1">15<span class="pl-k">px</span></span> <span class="pl-c1">auto</span>;</span>
    <span class="pl-s1">  <span class="pl-c1">padding</span>: <span class="pl-c1">15<span class="pl-k">px</span></span>;</span>
    
    <span class="pl-s1">  <span class="pl-c1">img</span> {</span>
    <span class="pl-s1">    <span class="pl-c1">width</span>: <span class="pl-c1">100<span class="pl-k">%</span></span>;</span>
    <span class="pl-s1">    <span class="pl-c1">height</span>: <span class="pl-c1">auto</span>;</span>
    <span class="pl-s1">    <span class="pl-c1">border-radius</span>: <span class="pl-c1">2<span class="pl-k">px</span></span>;</span>
    <span class="pl-s1">  }</span>
    
    <span class="pl-s1">  <span class="pl-ent">p</span><span class="pl-e">:first-child</span> {</span>
    <span class="pl-s1">    <span class="pl-c1">text-transform</span>: <span class="pl-c1">capitalize</span>;</span>
    <span class="pl-s1">    <span class="pl-c1">font-size</span>: <span class="pl-c1">2<span class="pl-k">rem</span></span>;</span>
    <span class="pl-s1">    <span class="pl-c1">font-weight</span>: <span class="pl-c1">900</span>;</span>
    <span class="pl-s1">  }</span>
    
    <span class="pl-s1">  <span class="pl-e">.text-capitalize</span> {</span>
    <span class="pl-s1">    <span class="pl-c1">text-transform</span>: <span class="pl-c1">capitalize</span>;</span>
    <span class="pl-s1">  }</span>
    <span class="pl-s1">}</span>
    <span class="pl-s1"><</span>/<span class="pl-ent">style</span>>





这样页面就能显示5个人的个人信息了.


## [](https://github.com/whidy/infinite-scroll-vuejs#%E5%A4%84%E7%90%86%E6%97%A0%E9%99%90%E6%BB%9A%E5%8A%A8%E5%8A%A0%E8%BD%BD%E9%80%BB%E8%BE%91)处理无限滚动加载逻辑


我们接下来需要在`methods`里面添加`scroll()`来监听滚动, 并且这个事件是应该在`mounted()`这个生命周期内的. 代码如下:




    
    <<span class="pl-ent">script</span>>
    <span class="pl-s1">  <span class="pl-c">// ...</span></span>
    <span class="pl-s1">  methods<span class="pl-k">:</span> {</span>
    <span class="pl-s1">    <span class="pl-c">// ...</span></span>
    <span class="pl-s1">    <span class="pl-en">scroll</span>(<span class="pl-smi">person</span>) {</span>
    <span class="pl-s1">      <span class="pl-k">let</span> isLoading <span class="pl-k">=</span> <span class="pl-c1">false</span></span>
    <span class="pl-s1">      <span class="pl-c1">window</span>.<span class="pl-en">onscroll</span> <span class="pl-k">=</span> () <span class="pl-k">=></span> {</span>
    <span class="pl-s1">        <span class="pl-c">// 距离底部200px时加载一次</span></span>
    <span class="pl-s1">        <span class="pl-k">let</span> bottomOfWindow <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">documentElement</span>.<span class="pl-smi">offsetHeight</span> <span class="pl-k">-</span> <span class="pl-c1">document</span>.<span class="pl-c1">documentElement</span>.<span class="pl-smi">scrollTop</span> <span class="pl-k">-</span> <span class="pl-c1">window</span>.<span class="pl-c1">innerHeight</span> <span class="pl-k"><=</span> <span class="pl-c1">200</span></span>
    <span class="pl-s1">        <span class="pl-k">if</span> (bottomOfWindow <span class="pl-k">&&</span> isLoading <span class="pl-k">==</span> <span class="pl-c1">false</span>) {</span>
    <span class="pl-s1">          isLoading <span class="pl-k">=</span> <span class="pl-c1">true</span></span>
    <span class="pl-s1">          <span class="pl-smi">axios</span>.<span class="pl-c1">get</span>(<span class="pl-s"><span class="pl-pds">`</span>https://randomuser.me/api/<span class="pl-pds">`</span></span>).<span class="pl-en">then</span>(<span class="pl-smi">response</span> <span class="pl-k">=></span> {</span>
    <span class="pl-s1">            <span class="pl-smi">person</span>.<span class="pl-c1">push</span>(<span class="pl-smi">response</span>.<span class="pl-c1">data</span>.<span class="pl-smi">results</span>[<span class="pl-c1">0</span>])</span>
    <span class="pl-s1">            isLoading <span class="pl-k">=</span> <span class="pl-c1">false</span></span>
    <span class="pl-s1">          })</span>
    <span class="pl-s1">        }</span>
    <span class="pl-s1">      }</span>
    <span class="pl-s1">    }</span>
    <span class="pl-s1">  },</span>
    <span class="pl-s1">  <span class="pl-en">mounted</span>() {</span>
    <span class="pl-s1">    <span class="pl-c1">this</span>.<span class="pl-c1">scroll</span>(<span class="pl-c1">this</span>.<span class="pl-smi">persons</span>)</span>
    <span class="pl-s1">  }</span>
    <span class="pl-s1">}</span>
    <span class="pl-s1"><</span>/<span class="pl-ent">script</span>>







<blockquote>这段代码原文是有一点拼写错误的. 我这里修正了, 另外增加了距离底部即开始加载数据, 并进行截流.</blockquote>


保存好, 回到浏览器, 查看效果, 已经没有问题了~


## [](https://github.com/whidy/infinite-scroll-vuejs#%E6%80%BB%E7%BB%93)总结


滚动到页面底部无限加载的功能在Vue上实现其实和普通的页面开发差不多, 每次滚动加载未完成的情况下不会触发请求下一次, 每次请求`push`到数组内, 通过`<img :src="">`的数据绑定实现了懒加载(其实0 0我不太认可...), 看完是不是感觉挺简单的.





最后, 我把这个也弄了一份在GitHub上面, 有需要的可以看看[infinite-scroll-vuejs-demo](https://github.com/whidy/infinite-scroll-vuejs)~



