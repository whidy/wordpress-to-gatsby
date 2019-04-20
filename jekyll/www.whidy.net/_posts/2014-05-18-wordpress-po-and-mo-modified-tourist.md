---
author: whidy
comments: true
date: 2014-05-18 09:46:33+00:00
template: post
link: http://www.whidy.net/wordpress-po-and-mo-modified-tourist.html
slug: /wordpress-po-and-mo-modified-tourist
title: WORDPRESS自定义模板后的PO文本翻译修改以及MO修改教程
wordpress_id: 2186
category: '开发'
tags:
- wordpress
- 技术
- 教程
- 网站
---

wordpress这个程序虽然强大,但是有时候根据自己需求不同,需要进行一些模板的修改,这次就我自定义模板后出现的一些问题和大家分享下,内容涉及到**主题的修改**以及**PO文本翻译修改**,还有**MO文件的修改**等内容.

先简单说一下我的需求,我希望**图片附件模板**(image.php)里增加一条**作者信息(实际上还是为了google的seo优化处理的)**,而默认是没有的,怎么处理,可参考该页面[OCZ Vertex4包装正面图一](http://www.whidy.net/ssd-ocz-vertex4-reviews-pictures.html/ocz-vertex4-front-1)(当然目前是已添加好的),如图:

![修改图片内容模板信息](https://www.whidy.net/wp-content/uploads/2014/05/modified-content-info-400x259.png)

现在应该很容易理解我要做的事情了吧,这个东西看起来似乎也是很简单的,不过当你看完这篇文章,也许你不会轻易这样想了.至少我完美解决这样的小问题花了3个小时,不过我的确不熟悉wordpress和php,也没有人能帮助我,好吧,闲话少说,步入正题.<!-- more -->


## 修改image.php图片内容模板


找到这一段,也就是上面一张图的框内输出部分


    
    ```php
    <?php
      $metadata = wp_get_attachment_metadata();
      printf( __( '<span class="meta-prep meta-prep-entry-date">Published </span> <span class="entry-date"><time class="entry-date" datetime="%1$s">%2$s</time></span> at <a href="%3$s" title="Link to full-size image">%4$s &times; %5$s</a> in <a href="%6$s" title="Return to %7$s" rel="gallery">%8$s</a>.', 'twentytwelve' ),
        esc_attr( get_the_date( 'c' ) ),
        esc_html( get_the_date() ),
        esc_url( wp_get_attachment_url() ),
        $metadata['width'],
        $metadata['height'],
        esc_url( get_permalink( $post->post_parent ) ),
        esc_attr( strip_tags( get_the_title( $post->post_parent ) ) ),
        get_the_title( $post->post_parent )
      );
    ?>
    ```



具体什么意思我就不说明了.上面有8个**%*$s**,其中*****代表**数字**,分别对应下面的8条(有点像C语言的printf,难道PHP也是这样的!?),我不知道如何用专有名字,姑且就这样描述了.然后我们将作者部分直接弄过来,我是直接调用主题的[functions.php](http://www.whidy.net/google-web-tool-structured-data-errors.html)的这一部分:


    
    ```php
    $author = sprintf( '<span class="author vcard"><a class="url fn n" href="%1$s" title="%2$s" rel="author">%3$s</a></span>',
      esc_url( get_author_posts_url( get_the_author_meta( 'ID' ) ) ),
      esc_attr( sprintf( __( 'View all posts by %s', 'twentytwelve' ), get_the_author() ) ),
      get_the_author()
    );
    ```



将他们合并起来就成了:


    
    ```php
    <?php
      $metadata = wp_get_attachment_metadata();
      printf( __( '<span class="author vcard">Author <a class="url fn n" href="%9$s" title="%10$s" rel="author">%11$s</a></span> <span class="meta-prep meta-prep-entry-date">Published </span> <span class="entry-date"><time class="entry-date updated" datetime="%1$s">%2$s</time></span> at <a href="%3$s" title="Link to full-size image">%4$s &times; %5$s</a> in <a href="%6$s" title="Return to %7$s" rel="gallery">%8$s</a>.', 'twentytwelve' ),
        esc_attr( get_the_date( 'c' ) ),
        esc_html( get_the_date() ),
        esc_url( wp_get_attachment_url() ),
        $metadata['width'],
        $metadata['height'],
        esc_url( get_permalink( $post->post_parent ) ),
        esc_attr( strip_tags( get_the_title( $post->post_parent ) ) ),
        get_the_title( $post->post_parent ),
        esc_url( get_author_posts_url( get_the_author_meta( 'ID' ) ) ),
        esc_attr( sprintf( __( 'View all posts by %s', 'twentytwelve' ), get_the_author() ) ),
        get_the_author()
      );
    ?>
    ```



说明一下,合并的时候,我稍加修改,**加了个Author**进去,请注意!

接下来保存image.php模板,发现输出了作者,但是有个问题,为什么是原本的"发表于","尺寸"等汉字都变成英文的呢?其实这个CN版本的wordpress有一个功能自动将语言转换成中文,那么,一定是转换部分出了问题!


## 修改twentytwelve-zh_CN.po以及对应的mo文件


接下来用这个笨却很实用的方法,搜索整个wordpress目录内"发布于"关键字,可以找到,原来这个转换部分存在这个文件内:**..\wp-content\languages\themes\twentytwelve-zh_CN.po**,找到约280行,我们可以看到如下信息:


    
    ```html
    #: image.php:26
    msgid ""
    "<span class=\"meta-prep meta-prep-entry-date\">Published </span> <span class="
    "\"entry-date\"><time class=\"entry-date\" datetime=\"%1$s\">%2$s</time></"
    "span> at <a href=\"%3$s\" title=\"Link to full-size image\">%4$s &times; "
    "%5$s</a> in <a href=\"%6$s\" title=\"Return to %7$s\" rel=\"gallery\">%8$s</"
    "a>."
    msgstr ""
    "<span class=\"meta-prep meta-prep-entry-date\">发表于</span> <span class="
    "\"entry-date\"><time class=\"entry-date\" datetime=\"%1$s\">%2$s</time></"
    "span>，尺寸为<a href=\"%3$s\" title=\"到全尺寸图像的链接\">%4$s &times; "
    "%5$s</a>，属于<a href=\"%6$s\" title=\"回到%7$s\" rel=\"gallery\">%8$s</a>。"
    ```



看到这里似乎明白了些什么,msgid和msgstr应该是对应关系,那么就开始动手修改这处,这里注意**转义字符**就可以了,如下:


    
    ```html
    #: image.php:26
    msgid ""
    "<span class=\"author vcard\">Author <a class=\"url fn n\" href=\"%9$s\" "
    "title=\"%10$s\" rel=\"author\">%11$s</a></span> <span class=\"meta-prep meta-"
    "prep-entry-date\">Published </span> <span class=\"entry-date\"><time class="
    "\"entry-date updated\" datetime=\"%1$s\">%2$s</time></span> at <a href=\"%3$s"
    "\" title=\"Link to full-size image\">%4$s &times; %5$s</a> in <a href=\"%6$s"
    "\" title=\"Return to %7$s\" rel=\"gallery\">%8$s</a>."
    msgstr ""
    "<span class=\"author vcard\">作者 <a class=\"url fn n\" href=\"%9$s\" title="
    "\"%10$s\" rel=\"author\">%11$s</a></span> <span class=\"meta-prep meta-prep-"
    "entry-date updated\">发表于</span> <span class=\"entry-date updated\"><time "
    "class=\"entry-date\" datetime=\"%1$s\">%2$s</time></span>，尺寸为<a href="
    "\"%3$s\" title=\"到全尺寸图像的链接\">%4$s &times; %5$s</a>，属于<a href="
    "\"%6$s\" title=\"回到%7$s\" rel=\"gallery\">%8$s</a>。"
    ```



好了,保存文件测试一下效果吧!**注意,我除了加了作者,还给日期部分加了个updated的class!**

到前台刷新页面发现还是英文的,事情原来远远没有这么简单,我花了大量时间来测试,为什么无法转换成中文,我检查我的转义后的语句是否有错误,我找了对应的代码部分是否相同,结果都毫无作用,我索性打开**twentytwelve-zh_CN.po**这个目录,发现还有个对应的**twentytwelve-zh_CN.mo**的文件,这个文件是做什么的呢,打开一看,有点像16进制文件,不可阅读的一大堆编码,这可怎么办,好在网上找得到原来PO文件有专门的编辑器可以保存出对应的MO文件,也就是说,上面仅仅更改了PO文件是没有用的,还要有对应生成的MO才可以!这个编辑器就是**[Poedit](http://poedit.net/dl/Poedit-1.6.5-setup.exe)**,那么安装后,打开这个twentytwelve-zh_CN.po文件,找到对应的地方重新检查是否有错误,如果没有,直接保存,就会自动生成新的twentytwelve-zh_CN.mo文件.

![poedit修改界面](https://www.whidy.net/wp-content/uploads/2014/05/poedit-400x248.png)

将以上修改好的所有文件上传到服务器上,刷新页面测试.发现一切正常了.需要的内容全部出来了.至此,这个不算太复杂却也耗费了一上午来处理的需求就完成了.


<blockquote>**最后来说说思路,首先我们需要什么?然后如何按步骤去做好?**

我们需要解决谷歌结构化数据内,图片内容模板没有作者和更新日期的标志.

那么找到wordpress的调用作者信息的方法,即上面修改image.php

其实在修改image.php的时候就应该注意到了,代码内容全是英文,而前台显示的是中文,这必定有个内容部转换过程,于是,就有了下一步,修改转换代码,即twentytwelve-zh_CN.po

修改后检查了image.php与twentytwelve-zh_CN.po对应的代码块发现没有任何问题,却依然无法正常输出中文,那么这里就容易卡住,如果想不出来借助搜索引擎的帮助,发现居然有Poedit这东西,简单的处理一下这一块,生成新的twentytwelve-zh_CN.mo文件后,问题迎刃而解,效果达到了!</blockquote>


PS: 本文是我在已经修改完成后经过回忆修改过程而写的,如果部分内容有差错,请及时通知我,感谢你的支持和帮助!
