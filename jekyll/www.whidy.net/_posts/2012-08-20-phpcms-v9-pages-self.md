---
author: whidy
comments: true
date: 2012-08-20 08:49:42+00:00
template: post
link: http://www.whidy.net/phpcms-v9-pages-self.html
slug: /phpcms-v9-pages-self
title: PHPCMS V9修改分页函数在当前页面翻页
wordpress_id: 961
category: '开发'
tags:
- 技术
- 网站
---

大家在做网站的时候经常会用到<base target="_blank" />这个代码,放在<head></head>内,这样默认情况下整个页面的所有超链接都会点击后自动开启新的标签或窗口来打开网址.的确方便了不少,然而,有些情况下比较特殊,我们不需要它开启新的窗口,要不然在早期电脑比较卡的时候,用户保留了窗口或标签不多开习惯,总要手动关闭很多窗口或标签,从用户体验上来说是及其不合理的.一般来说解决办法也很简单,只要给那个特殊的a标签加个**target="_self"**就可以了.当然,今天我们要讨论的问题远没有这么简单,事实上当你研究后,觉得其实也是很简单的事情.
<!-- more -->
进入正题,那么,PHPCMS V9系统中所有翻页功能都是通过一个**{$pages}**来实现分页的.事实上,一共有两种,一种是栏目页的文章列表分页;另一种是,文章内容页内的分页...所以今天我就是简单的跟大家说一下这两种分页修改方式,先来说第一种情况:

找到文件\phpcms\libs\functions\global.func.php并打开,搜索分页函数,大概在580行,修改这个注释下面的函数(修改前请备份该文件):


    
    ```php
    function pages($num, $curr_page, $perpage = 20, $urlrule = '', $array = array(),$setpages = 10) {
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
        $multipage .= '<a class="a1" target="_self">'.$num.L('page_item').'</a>';
        if($curr_page>0) {
          $multipage .= ' <a href="'.pageurl($urlrule, $curr_page-1, $array).'" class="a1" target="_self">'.L('previous').'</a>';
          if($curr_page==1) {
            $multipage .= ' <span>1</span>';
          } elseif($curr_page>6 && $more) {
            $multipage .= ' <a href="'.pageurl($urlrule, 1, $array).'" target="_self">1</a>..';
          } else {
            $multipage .= ' <a href="'.pageurl($urlrule, 1, $array).'" target="_self">1</a>';
          }
        }
        for($i = $from; $i <= $to; $i++) {
          if($i != $curr_page) {
            $multipage .= ' <a target="_self" href="'.pageurl($urlrule, $i, $array).'">'.$i.'</a>';
          } else {
            $multipage .= ' <span>'.$i.'</span>';
          }
        }
        if($curr_page<$pages) {
          if($curr_page<$pages-5 && $more) {
            $multipage .= ' ..<a href="'.pageurl($urlrule, $pages, $array).'" target="_self">'.$pages.'</a> <a href="'.pageurl($urlrule, $curr_page+1, $array).'" class="a1" target="_self">'.L('next').'</a>';
          } else {
            $multipage .= ' <a href="'.pageurl($urlrule, $pages, $array).'" target="_self">'.$pages.'</a> <a href="'.pageurl($urlrule, $curr_page+1, $array).'" class="a1" target="_self">'.L('next').'</a>';
          }
        } elseif($curr_page==$pages) {
          $multipage .= ' <span>'.$pages.'</span> <a href="'.pageurl($urlrule, $curr_page, $array).'" class="a1" target="_self">'.L('next').'</a>';
        } else {
          $multipage .= ' <a href="'.pageurl($urlrule, $pages, $array).'" target="_self">'.$pages.'</a> <a href="'.pageurl($urlrule, $curr_page+1, $array).'" class="a1" target="_self">'.L('next').'</a>';
        }
      }
      return $multipage;
    }
    ```



其实就是在a标签内添加了一个target="_self"而已.保存,问题就解决了.

接下来是内容页的翻页功能的修改方法是一样的,但是这个函数找了好半天...实际上是这个文件:

**\phpcms\modules\content\functions\util.func.php**

看着就感觉很诡异...打开它,代码不多,修改成这个样子:


    
    ```php
    <?php
    /**
     * 分页函数
     * 
     * @param $num 信息总数
     * @param $curr_page 当前分页
     * @param $pageurls 链接地址
     * @return 分页
     */
    function content_pages($num, $curr_page,$pageurls) {
    	$multipage = '';
    	$page = 11;
    	$offset = 4;
    	$pages = $num;
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
    		} elseif($to >= $pages) {
    			$from = $pages-($page-2);
    			$to = $pages-1;
    		}
    		$more = 1;
    	}
    	if($curr_page>0) {
    		$perpage = $curr_page == 1 ? 1 : $curr_page-1;
    		$multipage .= '<a class="a1" href="'.$pageurls[$perpage][0].'" target="_self">'.L('previous').'</a>';
    		if($curr_page==1) {
    			$multipage .= ' <span>1</span>';
    		} elseif($curr_page>6 && $more) {
    			$multipage .= ' <a href="'.$pageurls[1][0].'" target="_self">1</a>..';
    		} else {
    			$multipage .= ' <a href="'.$pageurls[1][0].'" target="_self">1</a>';
    		}
    	}
    	for($i = $from; $i <= $to; $i++) {
    		if($i != $curr_page) {
    			$multipage .= ' <a href="'.$pageurls[$i][0].'" target="_self">'.$i.'</a>';
    		} else {
    			$multipage .= ' <span>'.$i.'</span>';
    		}
    	}
    	if($curr_page<$pages) {
    		if($curr_page<$pages-5 && $more) {
    			$multipage .= ' ..<a href="'.$pageurls[$pages][0].'" target="_self">'.$pages.'</a> <a class="a1" href="'.$pageurls[$curr_page+1][0].'" target="_self">'.L('next').'</a>';
    		} else {
    			$multipage .= ' <a href="'.$pageurls[$pages][0].'" target="_self">'.$pages.'</a> <a class="a1" href="'.$pageurls[$curr_page+1][0].'" target="_self">'.L('next').'</a>';
    		}
    	} elseif($curr_page==$pages) {
    		$multipage .= ' <span>'.$pages.'</span> <a class="a1" href="'.$pageurls[$curr_page][0].'" target="_self">'.L('next').'</a>';
    	}
    	return $multipage;
    }
    ?>
    ```



保存,更新一下后台缓存,问题解决,经测试成功!

这只是一个简单的案例.另外一方面,之前也写了一个自定义分页函数的文章,如果大家希望同时存在默认功能和自己加的直接当前页面打开新的链接功能,可以参考这篇文章**[PHPCMS V9 自定义列表分页功能实现方法](/phpcms-v9-list-page-customize.html)**自己写一个函数,用其他方式调用比如$pages_customs
