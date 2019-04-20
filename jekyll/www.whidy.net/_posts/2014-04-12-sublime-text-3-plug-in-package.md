---
author: whidy
comments: true
date: 2014-04-12 06:25:06+00:00
template: post
link: http://www.whidy.net/sublime-text-3-plug-in-package.html
slug: /sublime-text-3-plug-in-package
title: Sublime Text 3近期使用总结(常用插件篇)
wordpress_id: 1895
category: '开发'
tags:
- sublime text
- 技术
- 网站
---

虽然很早就有了解,不过实际上还是近期因工作需要才开始正式以sublimeText3做主要开发工具.为此费了不少精力学习这个编辑器,现总结如下.

因为网上大部分都是介绍sublime text 2的相关内容,很多插件实际上在3已经不好用了,<del>并且sublime text 3安装插件也不需要调用控制台了(貌似便携版还是需要手动添加,通过快捷键 ctrl+` 或者 View > Show Console 菜单打开控制台</del>


<blockquote>import urllib.request,os;pf='Package Control.sublime-package';ipp=sublime.installed_packages_path();urllib.request.install_opener(urllib.request.build_opener(urllib.request.ProxyHandler()));open(os.path.join(ipp,pf),'wb').write(urllib.request.urlopen('http://sublime.wbond.net/'+pf.replace(' ','%20')).read())</blockquote>


如果以上报错(**上面可能只适用于安装版,如果便携版报错**)请试试下面这条


<blockquote>import urllib.request,os,hashlib; h = '7183a2d3e96f11eeadd761d777e62404' + 'e330c659d4bb41d3bdf022e94cab3cd0'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)</blockquote>


如果还是不行,请参考: [**https://sublime.wbond.net/installation**](https://sublime.wbond.net/installation) (更新日期2014年9月4日)

<del>更新日期:2014年5月5日)</del>,直接在Preferences里面就可以看到Package Control,进行插件安装.我专也门查了很多资料,根据个人习惯以及工作需要对于sublime text 3的常用插件做了一些整理,有需要的可以参考一下:


## **bracketHighLighter (Bracket and tag highlighter for Sublime Text)**


_Bracket Highlighter matches a variety of brackets such as: `[]`, `()`, `{}`, `""`, `''`, `<tag></tag>`, and even custom brackets._
自动在成对标签内的首尾下面添加一个下划线,方便查看是否有遗漏的tag或者js里面少写了一些闭合符号.

<!-- more -->


## **Tag (Collection of packages about HTML/XML tags.)**


不记得这个插件式默认自带的还是我装的了.总是写HTML必须要有,自动元素标签用的,如果默认就有无视我吧...


## **Emmet (Emmet (ex-Zen Coding) for Sublime Text)**


这个就是所谓的神器了.其实之前介绍过的,我就不多说了,见文章底部扩展阅读[Vimeo的关于Sublime Text 2插件Zencoding用法演示视频下载](http://www.whidy.net/wp-admin/post.php?post=999&action=edit)


## **Convert​To​UTF8 (A Sublime Text 2 & 3 plugin for editing and saving files encoded in GBK, BIG5, EUC-KR, EUC-JP, Shift_JIS, etc.)**


为什么要装这个,虽然现在都是主流的UTF-8,但是有些老网站不便更新,所以,基本上就是因为工作需要安装了,好处在于支持GBK的编码格式文件,当然也有缺点的,偶尔保存会乱码,撤销上一步重新保存就好了如果还是不行,那就复制一遍正确的,关闭后重新打开了...我目前就是这样解决的.


## **SideBarEnhancements (Enhancements to Sublime Text sidebar. Files and folders.)**


侧边栏增强插件,同样的可以设置快速预览HTML(或者安装ViewInBrowser),至于有没有需要安装看自己了.


## **TrailingSpaces (Highlight trailing spaces and delete them in a flash.)**


对于我这样轻度洁癖的人来说是有必要的,在不该存在空格和TAB的地方就不能有,全部删掉,全部删掉,全部删掉!!!


## **j​Query(Sublime Text package bundle for jQuery.)**


可以自动补全jQuery代码,的确很不错.这样以后不用因为格式问题频繁查看jQuery的API文档了~

其实还有一些什么自动对齐(**alignment**),主题插件之类的,我都没装感觉不是很常用,有兴趣自己去查一下咯~

最后如果大家想尝试一下Sublime Text的其他各种插件,可以去[**Package Control - the Sublime Text package manager**](https://sublime.wbond.net/)这个网站寻找尝试~

扩展阅读:
[Sublime Text 2下使用ZenCoding简介](http://www.whidy.net/wp-admin/post.php?post=990&action=edit)
[Vimeo的关于Sublime Text 2插件Zencoding用法演示视频下载](http://www.whidy.net/wp-admin/post.php?post=999&action=edit)
[Sublime Text 3 中文优化版更新下载了](http://www.whidy.net/wp-admin/post.php?post=1705&action=edit)

更新增加jQuery插件(2014年9月29日)
