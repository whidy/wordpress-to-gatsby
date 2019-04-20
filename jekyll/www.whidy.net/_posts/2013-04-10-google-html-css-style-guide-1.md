---
author: whidy
comments: true
date: 2013-04-10 07:32:12+00:00
template: post
link: http://www.whidy.net/google-html-css-style-guide-1.html
slug: /google-html-css-style-guide-1
title: 谷歌HTML/CSS书写规范总结一(Google HTML/CSS Style Guide)
wordpress_id: 1646
category: '音乐'
tags:
- 技术
- 网站
---

英文水平尚可或者没心情看我写的的朋友请查看谷歌原文档:**[Google HTML/CSS Style Guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)**

那么以下是我简要的总结(因为有点长分几篇发):



	
  1. 可以省略掉所有的关于附加的文档,图片等文件,甚至是CSS里面的的链接地址中存在的的**http:**或**https:**

	
  2. 关于代码缩进问题,都不要使用tab进行缩进,全部使用**2个空格**键进行缩进

	
  3. 所有的HTML元素名称,属性,属性值(除了text/CDATA),CSS选择器,属性,属性值**全部都用小写**,简单的说就是基本上不用大写就行了

	
  4. **不要留多余的空格**,在代码末尾,就算是自动生成的

	
  5. 强烈建议使用**UTF-8**编码进行页面制作.通过在模板内添加<meta charset="utf-8">,想了解更多请查看[Handling character encodings in HTML and CSS](http://www.w3.org/International/tutorials/tutorial-char-enc/)

	
  6. 养成写注释的好习惯,当然每种计算机语言都是这样的<!-- more -->

	
  7. **todos**是什么我暂时不知道,没找到相关资料,因此直接摘抄原文


_Mark todos and action items with `TODO`._









_Highlight todos by using the keyword `TODO` only, not other common formats like `@@`._
_ Append a contact (username or mailing list) in parentheses as with the format `TODO(contact)`.
Append action items after a colon as in `TODO: action item`._


    
    ```html
    {# TODO(john.doe): revisit centering #}
    <center>Test</center>
    ```





    
    ```html
    <!-- TODO: remove optional tags -->
    <ul>
      <li>Apples</li>
      <li>Oranges</li>
    </ul>
    ```









	
  8. 强烈建议使用HTML5作为网页html编码并且**不要使用xhtml**,例如application/xhtml+xml,不要闭合void 元素(不知道如何翻译),例如写成<br>,而不是<br />,笔者注:当然dw默认自动成后者了- -..

	
  9. 最好是做**W3C HTML 验证**来确保一切都很标准


未完待续...
