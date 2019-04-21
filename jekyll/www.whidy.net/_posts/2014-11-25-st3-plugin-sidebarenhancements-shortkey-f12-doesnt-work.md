---
author: whidy
comments: true
date: 2014-11-25 14:17:15+00:00
description: 最近我的sublime text 3突然无法用F12预览正在制作的页面了.相反,倒是成了提示" unable to find xxx",还真是奇怪,当然本身这是用的一个侧边栏插件Side​Bar​Enhancements,但是好好的插件,为什么无缘无故的快捷键就坏了呢.
template: post
draft: false
link: http://www.whidy.net/st3-plugin-sidebarenhancements-shortkey-f12-doesnt-work.html
slug: /st3-plugin-sidebarenhancements-shortkey-f12-doesnt-work
title: SublimeText3突然无法通过快捷键F12预览页面
wordpress_id: 2634
category: '开发'
tags:
- sublime text
- 教程
---

最近我的sublime text 3突然无法用F12预览正在制作的页面了.相反,倒是成了提示" unable to find xxx",还真是奇怪,当然本身这是用的一个侧边栏插件**Side​Bar​Enhancements**,但是好好的插件,为什么无缘无故的快捷键就坏了呢.不过最近似乎每次启动sublime text的时候,都有更新什么插件,于是就想到本来已装的插件SideBarEnhancements的设置,可是初看又看不出来什么名堂.于是只好去看看是不是插件更新了什么.

找到插件主页,看到了大大的**F12 key**的说明片段:


<blockquote>(Please note that from version 2.122104 this package no longers provides the key , you need to manually add it to your sublime-keymap file (see next section))</blockquote>


这句话说的很清楚了.但是我就想作为全局使用的快捷键,毕竟养成的习惯不易更改嘛...继续向下看,找到**F12 key conflict**, 官方也有说明啦:


<blockquote>On Sublime Text 3 `F12` key is bound to `"goto_definition"` command by default. This package was conflicting with that key, this no longers happens. You need to manually add the keys now: Go to `Preferences -> Package Settings -> Side Bar -> Key Bindings - User` and add any of the following:</blockquote>



    
    ```json
    [
        { "keys": ["f12"],
        "command": "side_bar_open_in_browser" ,
        "args":{"paths":[], "type":"testing", "browser":""}
        },
        { "keys": ["alt+f12"],
        "command": "side_bar_open_in_browser",
        "args":{"paths":[], "type":"production", "browser":""}
        },
        {
        "keys": ["ctrl+t"],
        "command": "side_bar_new_file2"
        },
        {
        "keys": ["f2"],
        "command": "side_bar_rename"
        },
    ]
    ```


其实很简单,将上面内容复制到

![SideBarEnhancements_keybindings_user](https://www.whidy.net/wp-content/uploads/2014/11/SideBarEnhancements_key-400x278.jpg)

保存就行了,如果想要鱼和熊掌兼得的朋友,就请自行设置成其他快捷键咯.

另外奉献两个参考地址:


# [Side​Bar​Enhancements](https://sublime.wbond.net/packages/SideBarEnhancements)




# [Sublime 3 - Set Key map for function Goto Definition](http://stackoverflow.com/questions/16235706/sublime-3-set-key-map-for-function-goto-definition)


PS: 注意官方提供的修改方案,设置了F2的快捷键,覆盖了之前的定位功能,如果不需要这个重命名文件功能请自行删除(2014年11月28日)
