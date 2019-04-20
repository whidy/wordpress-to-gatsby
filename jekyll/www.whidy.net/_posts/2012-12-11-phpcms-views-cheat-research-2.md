---
author: whidy
comments: true
date: 2012-12-11 07:49:13+00:00
template: post
link: http://www.whidy.net/phpcms-views-cheat-research-2.html
slug: /phpcms-views-cheat-research-2
title: phpcms点击数作弊深度研究(下)
wordpress_id: 1275
category: '开发'
tags:
- 技术
- 网站
---

上期讲解了我个人突然想到的两个方法,当然其实哪些方法并不完美.至于完美的方法,我后来也在网上找了一些,没有一个令人满意,而大多数作者仅仅是草草写了些方法,不做任何说明.我还是到处收集资料,对这个功能进行分析研究,也已互联网上的一些例子进行介绍分析,找出更好的方法.

其中有一个是来自新浪博客的一篇文章[<<phpcms v9 新增文章时,随机增加点击数修改方法>>](http://blog.sina.com.cn/s/blog_95a82dde01011lww.html),当然这个是随机找的,其他的基本上是大同小异,原理就是在文章发布后就有个初始值,然后以后点击一次,点击量递增1.对于访问量较小的网站来说效果其实不好.

<!-- more -->

而且[上期](http://www.whidy.net/phpcms-views-cheat-research-1.html)提到的作弊方式,有个弊端,当然也是我后来发现的,本来这篇是想解剖网络上流传的方式,我觉得也没有意义了.而经过后来研究发现,我这个方法好像是网上根本找不到的.也是根本上解决了上期提到的问题:文章列表和其他调用点击数的地方虽然点击量一致,但是在数据库内依然是原始值,而在**show**模版里面显示的就是原始值,他通过JS调用出点击数,这段JS就是:<script language="JavaScript" src="{APP_PATH}api.php?op=count&id={$id}&modelid={$modelid}"></script>

由此我开始想办法找到通过JS调用出点击率的方法.于是找到PHPCMS V9安装目录的**api目录**,可以看到一个**count.php**文件,这就是个点击统计的输出代码.我先上我修改后的文件代码:


    
    ```php
    <?php
    defined('IN_PHPCMS') or exit('No permission resources.'); 
    /**
     * 点击统计
     */
    $db = '';
    $db = pc_base::load_model('hits_model');
    if($_GET['modelid'] && $_GET['id']) {
    	$model_arr = array();
    	$model_arr = getcache('model','commons');
    	$modelid = intval($_GET['modelid']);
    	$hitsid = 'c-'.$modelid.'-'.intval($_GET['id']);
    	$r = get_count($hitsid);
    	if(!$r) exit;
        extract($r);
        hits($hitsid);
    	$fdayviews = $dayviews * 9 + rand(1,4);
    	$fweekviews = $weekviews * 9 + rand(1,4);
    	$fmonthviews = $monthviews * 9 + rand(1,4);
        echo "\$('#todaydowns').html('$fdayviews');";
        echo "\$('#weekdowns').html('$fweekviews');";
        echo "\$('#monthdowns').html('$fmonthviews');";
    } elseif($_GET['module'] && $_GET['id']) {
    	$module = $_GET['module'];
    	if((preg_match('/([^a-z0-9_\-]+)/i',$module))) exit('1');
    	$hitsid = $module.'-'.intval($_GET['id']);
    	$r = get_count($hitsid);
    	if(!$r) exit;
        extract($r);
        hits($hitsid);
    }
    
    /**
     * 获取点击数量
     * @param $hitsid
     */
    function get_count($hitsid) {
    	global $db;
        $r = $db->get_one(array('hitsid'=>$hitsid));  
        if(!$r) return false;	
    	return $r;	
    }
    
    /**
     * 点击次数统计
     * @param $contentid
     */
    function hits($hitsid) {
    	global $db;
    	$r = $db->get_one(array('hitsid'=>$hitsid));
    	if(!$r) return false;
    	$views = $r['views'] + 1;
    	$yesterdayviews = (date('Ymd', $r['updatetime']) == date('Ymd', strtotime('-1 day'))) ? $r['dayviews'] : $r['yesterdayviews'];
    	$dayviews = (date('Ymd', $r['updatetime']) == date('Ymd', SYS_TIME)) ? ($r['dayviews'] + 1) : 1;
    	$weekviews = (date('YW', $r['updatetime']) == date('YW', SYS_TIME)) ? ($r['weekviews'] + 1) : 1;
    	$monthviews = (date('Ym', $r['updatetime']) == date('Ym', SYS_TIME)) ? ($r['monthviews'] + 1) : 1;
    	$sql = array('views'=>$views,'yesterdayviews'=>$yesterdayviews,'dayviews'=>$dayviews,'weekviews'=>$weekviews,'monthviews'=>$monthviews,'updatetime'=>SYS_TIME);
        return $db->update($sql, array('hitsid'=>$hitsid));
    }
    
    ?>
    $('#hits').html('<?php echo $views*9 + rand (1,4)?>');
    ```



高亮部分时我修改过的,我在这里定义了一个假的点击数,并让这段代码在读取后输出了,那么现在在文章内容页的点击数也就完美解决了,除了在后台看的到真实的点击数,那么一切前台显示都是假的,而且很逼真.至此这个算是完美解决了.
