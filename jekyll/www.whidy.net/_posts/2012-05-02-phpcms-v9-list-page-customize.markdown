---
author: whidy
comments: true
date: 2012-05-02 08:54:37+00:00
layout: post
link: http://www.whidy.net/phpcms-v9-list-page-customize.html
slug: phpcms-v9-list-page-customize
title: PHPCMS V9 自定义列表分页功能实现方法
wordpress_id: 733
categories:
- IT技术
- Phpcms
tags:
- 技术
- 网站
---

在用PHPCMS V9的过程中,可能一般人都不会在意分页功能,因为调用他实在是很简单,需要修改的估计也就是分页功能的样式了,拿系统自带的模板来看

    ```php
    <div id="pages" class="text-c">{$pages}</div>
    ```



我们可以修改class来自定义样式,当然有人会说,这个只能修改DIV的样式,无法修改里面的内容的样式,其实之需要看一下这段代码解析出来的实际代码就知道了,而这里的样式可以直接通过head部分内读取的CSS来代替,我就可以在CSS里面添加这样一段,为了方便测试,我直接写在head标签内:

    ```css
    .text-c {margin:10px 0;}
    .text-c a {padding:5px;margin:0 8px;border:1px solid #ccc;background-color:#eee;}
    ```



经过测试是有效的.这里不在说这个了,重点是**{$pages}**输出的分页效果是固定的,如何让他能够满足自己的需求,比如最简单的系统默认是显示多少**条**,用**上一页**,**下一页**来表示,如果我想改成**向后翻**,**向前翻**,怎么办?我经过查找相关资料,对这个功能进行整理得出结果与大家分享出来,涉及修改到的文件只有下面两个:


<blockquote>\phpcms\languages\zh-cn\system.lang.php
\phpcms\libs\functions\global.func.php
\ phpcms\lib\classes\template_cache.class.php</blockquote>


具体怎么弄,待我慢慢与大家讲解:

首先打开**system.lang.php**,找到29行LANG['next'] = '下一页';处,你可以在下面插入自定义的内容,比如向后翻,向前翻,整理效果应该是这样的,添加完后保存可以关闭了.

    ```php
    $LANG['page_item'] = '条';
    $LANG['previous'] = '上一页';
    $LANG['next'] = '下一页';
    $LANG['page_item_my'] = '篇';			//自定义
    $LANG['previous_my'] = '向前翻';		//自定义
    $LANG['next_my'] = '向后翻';				//自定义
    ......
    ```
    
    然后打开<strong>global.func.php</strong>,搜索<strong>分页函数</strong>找到找到<span style="color: #ff0000;">function pages...</span>,在这个函数后复制原函数并修改添加自己想要定义的函数,例如:

    ```php
    //自定义分页函数
    function pages_my($num, $curr_page, $perpage = 20, $urlrule = '', $array = array(),$setpages = 10) {
    	if(defined('URLRULE') && $urlrule == '') {
    		$urlrule = URLRULE;
    		$array = $GLOBALS['URL_ARRAY'];
    	} elseif($urlrule == '') {
    		$urlrule = url_par('page={$page}');
    	}
    	$multipage = '';
    	if($num > $perpage) {
    		$page = $setpages+1;
    		$offset = ceil($setpages/2-1);
    		$pages = ceil($num / $perpage);
    		if (defined('IN_ADMIN') && !defined('PAGES')) define('PAGES', $pages);
    		$from = $curr_page - $offset;
    		$to = $curr_page + $offset;
    		$more = 0;
    		if($page >= $pages) {
    			$from = 2;
    			$to = $pages-1;
    		} else {
    			if($from <= 1) {
    				$to = $page-1;
    				$from = 2;
    			}  elseif($to >= $pages) {
    				$from = $pages-($page-2);
    				$to = $pages-1;
    			}
    			$more = 1;
    		}
    		$multipage .= '<a class="a1">'.$num.L('page_item_my').'</a>';
    		if($curr_page>0) {
    			$multipage .= ' <a href="'.pageurl($urlrule, $curr_page-1, $array).'" class="a1">'.L('previous_my').'</a>';
    			if($curr_page==1) {
    				$multipage .= ' <span>1</span>';
    			} elseif($curr_page>6 && $more) {
    				$multipage .= ' <a href="'.pageurl($urlrule, 1, $array).'">1</a>..';
    			} else {
    				$multipage .= ' <a href="'.pageurl($urlrule, 1, $array).'">1</a>';
    			}
    		}
    		for($i = $from; $i <= $to; $i++) {
    			if($i != $curr_page) {
    				$multipage .= ' <a href="'.pageurl($urlrule, $i, $array).'">'.$i.'</a>';
    			} else {
    				$multipage .= ' <span>'.$i.'</span>';
    			}
    		}
    		if($curr_page<$pages) {
    			if($curr_page<$pages-5 && $more) {
    				$multipage .= ' ..<a href="'.pageurl($urlrule, $pages, $array).'">'.$pages.'</a> <a href="'.pageurl($urlrule, $curr_page+1, $array).'" class="a1">'.L('next_my').'</a>';
    			} else {
    				$multipage .= ' <a href="'.pageurl($urlrule, $pages, $array).'">'.$pages.'</a> <a href="'.pageurl($urlrule, $curr_page+1, $array).'" class="a1">'.L('next_my').'</a>';
    			}
    		} elseif($curr_page==$pages) {
    			$multipage .= ' <span>'.$pages.'</span> <a href="'.pageurl($urlrule, $curr_page, $array).'" class="a1">'.L('next_my').'</a>';
    		} else {
    			$multipage .= ' <a href="'.pageurl($urlrule, $pages, $array).'">'.$pages.'</a> <a href="'.pageurl($urlrule, $curr_page+1, $array).'" class="a1">'.L('next_my').'</a>';
    		}
    	}
    	return $multipage;
    }
    ```



最后打开**template_cache.class.php**,找到

    ```php
    $str .= '$pages = pages($'.$op.'_total, $page, $pagesize, $urlrule);';
    ```


处,在下面添加:

    ```php
    $str .= '$pages_my= pages_my($'.$op.'_total, $page, $pagesize, $urlrule);';
    ```



当然如果使用过程中，发现SQL分页的不能正常使用，再在

    ```php
    $str .= '$r = $get_db->sql_query("'.$sql.'");$s = $get_db->fetch_next();$pages=pages($s[\'count\'], $page, $pagesize, $urlrule);';
    ```


添加这段代码:

    ```php
    $str .= '$r = $get_db->sql_query("'.$sql.'");$s = $get_db->fetch_next();$pages_my=pages_my($s[\'count\'], $page, $pagesize, $urlrule);';
    ```



至此大功告成,接下来,你只用在你想要的模板的分页出使用就可以了,例如开头的格式

    ```php
    <div id="pages" class="myListPage">{$pages_my}</div>
    ```



并写上对应的CSS就可以了.

