---
author: whidy
comments: true
date: 2016-03-07 03:37:26+00:00
description: 关于sublime text 3(3103)版本Ctrl+Alt+P无法正常使用,自定义快捷键的设置command实际上就是prompt_select_workspace,解决了此问题
template: post
draft: false
link: http://www.whidy.net/sublime-text-3-3103-ctrl-alt-p-cannot-use.html
slug: /sublime-text-3-3103-ctrl-alt-p-cannot-use
title: 关于sublime text 3(3103)版本Ctrl+Alt+P无法正常使用解决办法
wordpress_id: 2852
category: '开发'
tags:
- sublime text
- 技术
---

过完年回来上班的第一天,打开sublime text 3,提示有更新([Sublime Text 3 Build 3103](https://www.sublimetext.com/blog/articles/sublime-text-3-build-3103)),没有多想就点下载更新了...更新完后,发现问题严重了,一方面是之前朋友买的key失效了,看到非注册的几个单词在窗口顶部就不自在了.当然这个不是本文重点,至于怎么解决这个问题,我相信不会难倒机智的大家.

而另一方面是很多之前的设置也没了.比如自定义快捷键.我有安装SideBarEnhancements这个插件,设置的F12快速预览也没了,只好找回旧版存档重新设置,其实这个问题也不大.
最糟糕的是,之前习惯用的**快速切换项目**的Ctrl+Alt+P不能用了,这个是旧版默认设置好的.然后到处找快捷键怎么设置的,我很傻,其实后来发现这个问题很好解决.我却绕了个大弯.

首先,百度肯定是搜不到的.然后去用谷歌找.谷歌是万能的,找到如下内容:

    
    ```json
    { "keys": ["ctrl+alt+p"], "command": "prompt_select_workspace" }
    ```


这下添加到自定义keymap,问题解决.参考:[Quick Switch Project shortcut doesn’t work anymore](https://forum.sublimetext.com/t/quick-switch-project-shortcut-doesnt-work-anymore/17261)(当然,他好像说3098版本就去掉了,我并未注意到可能我一直在使用更旧的版本.而changelog里面似乎也没看到3098)

当然这里还要提一点的是,如果一切设置好了发现还是不能用,那多半是快捷键冲突所致,比如输入法的全局快捷键等等,这里推荐一个虽然有点老,但是还不错的工具Windows Hotkey Explorer,大家自行安装后,可以查看系统全局被占用的快捷键,然后对应的关闭调整一下就好了.

![windowsHotkeyExplorer软件界面](https://www.whidy.net/wp-content/uploads/2016/03/windowsHotkeyExplorer-400x383.png)

总结下来我的自定义快捷键是这样的.

    
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
            "keys": ["ctrl+alt+p"],
            "command": "prompt_select_workspace"
        }
    ]
    ```


最后来说说为啥我笨死了.其实关于这个command,我找不到的话,我直接找旧版本的sublime text的default keymap查一下就好了嘛...笨笨笨...........还费了老大功夫.其他朋友有遇到类似问题也可举一反三,自行配置一个好用的sublime text咯~~~~

**工具虽好,务必不要再WIN10下使用该软件,会发生十分可怕的事情!(2017年8月25日 更新)**
