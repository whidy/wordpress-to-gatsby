---
author: whidy
comments: true
date: 2014-05-15 15:18:37+00:00
layout: post
link: http://www.whidy.net/sublime-text-3-user-setting-intro.html
slug: sublime-text-3-user-setting-intro
title: Sublime Text 3常用用户自定义配置推荐
wordpress_id: 2071
categories:
- IT技术
- 技术分享
tags:
- sublime text
- 技术
- 教程
---

现在可算是对sublime text编辑器有点入门了,除了基本操作快捷键之外,对于sublime text的用户配置设置我今天也细细研究了一番,对于英语勉强说得过去的我,看这个默认的配置(**Preferences.sublime-settings---Default**)说明是没有太大压力的,对于英语差的,先硬着头皮看看,实在不行,我总结了以下一些我感觉还算比较方便的配置选项,当然,自定义的就是覆盖了默认设置的,有兴趣的可以看看,根据个人需要修改...首先当然是开启**Preferences.sublime-settings---User**了,见图,我在配置中加了说明方便查阅:

[caption id="attachment_2072" align="aligncenter" width="400"][![Sublime text 3用户自定义设置配置](http://www.whidy.net/wp-content/uploads/2014/05/sublime_user_settings-400x270.png)](http://www.whidy.net/wp-content/uploads/2014/05/sublime_user_settings.png) Sublime text 3用户自定义设置配置[/caption]

(图中可以看到修改过的文件名称是黄色,选中的那一行也高亮了等等,大家自行观察咯~)

接下来大家根据需要拷贝过去进行修改吧...

    ```javascripton
    {
    "auto_complete_selector": "source,text", //用到snippet的话加此行,否则请无视我
    "font_size": 16, //不用多说,字体大小,同样可以按住CTRL+'+'或者'-'或者'鼠标滚轮'调整
    "ignored_packages":
    [
    "Vintage"
    ], //忽视此包...
    "word_separators": "./\\()\"':,.;<>~!@#$%^&*|+=[]{}`~?", //这些字符会在鼠标双击时隔断,可自行删除不必要的,例如这个被我修改过删除了'-'符号,详情可参考我之前写的<<sublime text快速选择带有横线(连接符)的类名或ID名等>>,上一篇就是了
    "word_wrap": true, //一行内容太长了,自动换行(如果你够'自信'的话,又喜欢拖动X轴滚动条请无视我)
    "highlight_line": true, //高亮显示当前编辑的行,有时自动折行看不清,这个就把一整块显示出来,清晰一些
    "show_encoding": true, //编辑器底部显示编码信息,用GBK编码的偶尔出现乱码,看看这个能查一下,虽然作用不大,放在下面也不占地方,无所谓了
    "save_on_focus_lost": true, //当焦点从当前编辑文档中丢失,会自动保存,看个人喜好咯
    "highlight_modified_tabs": true, //高亮TAB显示被修改过的文档,如果上一条为关闭,修改过的文件看起来更清晰
    "draw_minimap_border": true, //在编辑器右侧小代码地图上为当前区加个边框,视力不好可以加上,比如我
    "always_show_minimap_viewport": true, //总是显示这个迷你地图窗口,还是视力不好
    "show_tab_close_buttons": false //不显示TAB标签上的关闭图标(个人认为没用,文件多了不小心切换的时候关了更麻烦,真的需要关闭某个标签的时候,可以在左侧栏已打开的文件中点叉叉,当然个人更加推荐使用快捷键CTRL+W)
    //注释 BY WHIDY 2014年5月15日...
    }
    ```

PS: 经过几日测试,我发现焦点失去自动保存功能并不好用,大家看情况来使用吧,原因:从外部快速切换到sublime text时,代码块会滚动一下,影响查找刚才编辑的位置,另外,如果是GBK编码格式,有时不小心乱码了,比较麻烦(2014年5月21日)
