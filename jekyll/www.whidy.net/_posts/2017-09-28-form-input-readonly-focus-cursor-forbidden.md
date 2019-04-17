---
author: whidy
comments: true
date: 2017-09-28 02:38:41+00:00
excerpt: 在做移动端页面，表单内的部分元素如果设置了readonly="readonly"，CHROME模拟移动端是看不出问题的。而手机上虽然表单元素不能编辑内容，但是会出现闪动的光标以及页面底部有一条系统自带的控制bar。这样的体验很差，于是我总结了几个方案。
layout: post
link: http://www.whidy.net/form-input-readonly-focus-cursor-forbidden.html
slug: form-input-readonly-focus-cursor-forbidden
title: 表单中readonly的input等标签，禁止光标进入（focus）的几种方式
wordpress_id: 2994
categories:
- CSS
- IT技术
- 技术分享
tags:
- 技术
- 教程
- 表单
---

在做移动端页面，需要在订单页面中显示表单数据，由于UI统一，所以就依旧采用form的结构来写结构，只读数据的标签自然要加readonly="readonly"，以为这样就行了，CHROME模拟移动端是看不出问题的。手机上一看，虽然表单元素不能编辑内容，但是会出现闪动的光标以及页面底部有一条系统自带的控制bar。

![表单readonly元素依然有光标](http://www.whidy.net/wp-content/uploads/2017/09/form-400x711.png)

这种情况对我来说并不好。于是网上找了一些解决方案，现在总结一下：

方案一（JS）：

    
    ```html
    <input type="text" value="test" onfocus="this.blur()" readonly="readonly">
    ```


这个很好理解就是进入的时候自动跳出。但是缺点是一方面js处理没有css好，二是如果需要在该元素上绑定其他事件，其他人开发不留意可能会造成事件覆盖。

方案二（CSS）：

    
    ```css
    [readonly="readonly"] {
      user-select: none;
    }
    ```


这是个新的实验性属性，具体说明及兼容性可参考[user-select MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/user-select)
用起来感觉很好，但是同样有两个问题：一，非标准属性（**请尽量不要在生产环境中使用它！**）；二，如果用户想要复制该表单内容就不行了，这个问题个人感觉很严重！

方案三（CSS）：

    
    ```css
    [readonly="readonly"] {
      pointer-events: none;
    }
    ```


这个是我感觉比较适合我的，因此最后我采纳了该方案，当然也是有弊端的，绑定在只读表单元素的所有事件将无法生效。除此之外都表现完美，就我目前需求来看，也不需要什么事件。因此采用了~

当然，如果你也遇到相似的问题，可以根据情况选择对应的方案，当然，如果你也有更好的方法也欢迎留言~
