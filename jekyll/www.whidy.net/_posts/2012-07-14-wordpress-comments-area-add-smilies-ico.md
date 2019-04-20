---
author: whidy
comments: true
date: 2012-07-14 11:11:45+00:00
template: post
link: http://www.whidy.net/wordpress-comments-area-add-smilies-ico.html
slug: /wordpress-comments-area-add-smilies-ico
title: wordpress评论区域下方添加表情图标方法
wordpress_id: 888
category: '开发'
tags:
- wordpress
- 技术
- 网站
- 表单
---

最近研究淘宝网店,顺便自己开了个做测试,没想到拉了个小客户,虽然交易价很便宜只有一元钱,并且花了一会就解决了他的问题.

随后他又遇到了一些问题想我询问,不过我以学习研究的态度帮助了他,这也就是今天要说的内容,何如给wordpress模板的评论区域快添加一排表情.先来看看效果图...

![表情图片位于评论区内的效果](https://www.whidy.net/wp-content/uploads/2012/07/smilies-346x400.jpg)

看后大家觉得这个很简单的,其实说简单也简单说有点麻烦也的确有点麻烦.首先我要说的是,调用系统默认的表情是需要在适当的位置添加下面一行代码:


    
    ```php
    <?php if ( function_exists(cs_print_smilies) ) {cs_print_smilies();} ?>
    ```



然而究竟是在哪里添加这段代码呢,我们继续分析研究...

可能回事修改主题的comments.php模板文件,但是当你找到评论区表单部分的时候,你发现居然只有短短的一句话:


    
    ```php
    <?php comment_form(); ?>
    ```



于是这个要么就出现在了整个评论表单区域的前面要么出现在了最底部,这并不美观,更不是我们想要的.所以修改comments.php是做不到的...那么就需要研究一下comment_form();这个函数了,可能是我比较笨,我首先想到的依然是主题目录下的functions.php文件里面修改,恰巧我也找到了,不过略不相同,抱着试试的态度,搜索到了comment_form_default_fields,具体完整代码如下:


    
    ```php
    add_filter('comment_form_default_fields','MxS_fields');
    /** -----------------------------------------------
    	 * custom comments
    */ 
    if ( ! function_exists('MxS_custom_comments')) {
    function MxS_custom_comments($comment, $args, $depth) {
    $GLOBALS['comment'] = $comment;
    ?>
    <li <?php comment_class(); ?> id="li-comment-<?php comment_ID() ?>">
    <div id="comment-<?php comment_ID(); ?>">
    <div class="message_head">
    <span class="avatarx"><?php echo get_avatar($comment,$size='40',$default='' ); ?></span>
    <span class="name"><?php comment_author_link() ?></span> <?php edit_comment_link( __( '(Edit)', 'mxs_theme' ), ' ' ); ?>
    <span class="reply"><?php comment_reply_link( array_merge( $args, array( 'depth' => $depth, 'max_depth' => get_option('thread_comments_depth') ) ) ); ?></span>
    </div>
    <span class="date"><?php comment_date('y/m/d') ?></span>
    <div class="clear"></div>
    <div class="cmt_text"><?php comment_text(); ?></div>
    </div><!-- #comment-##  -->	
    <?php }}
    ```



当然这个函数之前的语句是与这个函数没有什么关系的.看这个函数,写的是已评论的表单结构.貌似也不对,其中有一句**$GLOBALS['comment'] = $comment;**目测好像是调用系统全局评论变量,具体是啥意思,我这PHP外行也不大明白...改来改去还是没该成功,于是想到会不会是跟系统函数模块有关.于是继续查找...找到了wp-includes/comment_template.php打开一看,仍然搜索comment_form,在1510行,找到了好长一段...耐心读下去..一直看到<?php if ( comments_open() ) : ?>字面上意思是,如果评论功能开启,则执行以下语句,接着看,就发现跟表单相关了.找到


    
    ```php
    <?php echo $args['comment_notes_after']; ?>
    <p class="form-submit">
      <input name="submit" type="submit" id="<?php echo esc_attr( $args['id_submit'] ); ?>" value="<?php echo esc_attr( $args['label_submit'] ); ?>" />
      <?php comment_id_fields( $post_id ); ?>
    </p>
    ```



其实也就看出来了,我不正是要在submit之前添加表情么?果断在form-submit前面加一行之前提到的表情调用代码,修改如下:


    
    ```php
    <?php echo $args['comment_notes_after']; ?>
    <?php if ( function_exists(cs_print_smilies) ) {cs_print_smilies();} ?>
    <p class="form-submit">
      <input name="submit" type="submit" id="<?php echo esc_attr( $args['id_submit'] ); ?>" value="<?php echo esc_attr( $args['label_submit'] ); ?>" />
      <?php comment_id_fields( $post_id ); ?>
    </p>
    ```



保存,接着刷新一下文章内容页看到评论区域就有了表情了.至此关于wp评论区域调用系统自带的表情图标功能就实现了.是不是很简单啊 :D

PS: 似乎这个方法在现在的3.8.2修改无效了.如果不行就直接装个Custom Smilies插件吧~(2014年4月9日)
