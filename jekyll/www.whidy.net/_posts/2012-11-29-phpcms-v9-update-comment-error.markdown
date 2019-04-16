---
author: whidy
comments: true
date: 2012-11-29 08:57:55+00:00
layout: post
link: http://www.whidy.net/phpcms-v9-update-comment-error.html
slug: phpcms-v9-update-comment-error
title: phpcms V9更新到最新后评论审核出错解决方法
wordpress_id: 1148
categories:
- IT技术
- Phpcms
tags:
- 网站
---

开门见山,这前几天更新了PHPCMS V9的最新后台程序(PHPCMS程序版本：Phpcms V9.2.4 Release 20121109),却不料发现评论审核无法通过.具体报错情况如图:

[caption id="attachment_1149" align="aligncenter" width="360"][![phpcms升级,评论审核出问题](/wp-content/uploads/2012/11/commentError.jpg)](/wp-content/uploads/2012/11/commentError.jpg) phpcms升级,评论审核出问题[/caption]

起了个乖,最早还不晓得什么回事.后来到处找也没找到原因,无奈上了官方论坛,找到了解决方案.具体修改方法如下:



	
  1. 找到后台系统phpcms\modules\comment\templates\comment_check.tpl.php文件

	
  2. 找到第33行


    
    <code class="php">	$.get('?m=comment&c=check&a=ajax_checks&id='+id+'&type='+type+'&commentid='+commentid+'&'+Math.random(), function(data){if(data!=1){if(data==0){alert('<?php echo L('illegal_parameters')?>')}else{alert(data)}}else{$('#tbody_'+id).remove();
    
    	$.getJSON('?m=comment&c=check&a=public_get_one&'+Math.random(), function(data){
    </code>



修改成


    
    <code class="php">	$.get('?m=comment&c=check&a=ajax_checks&id='+id+'&type='+type+'&commentid='+commentid+'&pc_hash='+pc_hash+'&'+Math.random(), function(data){if(data!=1){if(data==0){alert('<?php echo L('illegal_parameters')?>')}else{alert(data)}}else{$('#tbody_'+id).remove();
    
    	$.getJSON('?m=comment&c=check&a=public_get_one&'+'&pc_hash='+pc_hash+Math.random(), function(data){
    </code>



保存,然后进入后台进行测试,评论审核问题基本完美解决!(其实还有个BUG,就是除了管理员账户,其他权限账户还是报错- -...好吧那么就只有等待官方解决了.)


参考资料: [打了9.2.4补丁后，评论审核出错](http://bbs.phpcms.cn/thread-724404-1-1.html)
