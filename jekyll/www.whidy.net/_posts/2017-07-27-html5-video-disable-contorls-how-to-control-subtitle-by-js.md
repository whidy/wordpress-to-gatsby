---
author: whidy
comments: true
date: 2017-07-27 03:23:52+00:00
description: 最近研究html5的video标签,尝试自己做一个播放器.然后既然是自己做必然要将video的controls给关掉.那我们该如何控制字幕的显示和隐藏了呢?
template: post
draft: false
link: http://www.whidy.net/html5-video-disable-contorls-how-to-control-subtitle-by-js.html
slug: /html5-video-disable-contorls-how-to-control-subtitle-by-js
title: HTML5视频VIDEO标签播放器关闭了controls时的字幕通过JS关闭方法
wordpress_id: 2950
category: '开发'
tags:
- 技术
---

最近研究html5的video标签,尝试自己做一个播放器.然后既然是自己做必然要将video的controls给关掉.

然后想到了如果要控制字幕这可怎么办呢,找了好久才找到如何通过js来控制字幕的显示与隐藏开关.其实也很简单.

这个测试仅针对视频有一个track标签.

HTML:

    
    ```html
    <video class="video" id="video" width="640" height="480" preload="auto" poster="https://github.com/whidy/video-player/blob/master/src/poster.png?raw=true">
      <source src="http://ie.microsoft.com/testdrive/ieblog/2011/nov/pp4_blog_demo.mp4" type="video/mp4">
      <p>Your browser doesn't support HTML5 video. YOU ARE BAD!</p>
      <track kind="subtitles" src="./subtitles.vtt" srclang="en" default>
    </video>
    <a href="javascript:;" id="btnCapSwitcher">Subtitle On/Off</a>
    ```


JAVASCRIPT:

    
    ```javascript
    var video = document.getElementById('video'),
      btnCapSwitcher = document.getElementById('btnCapSwitcher');
    // 字幕开关(注意在本次demo测试中只有一个字幕因此可以这样处理,如果存在多个字幕需可能需要修改)
    btnCapSwitcher.addEventListener('click', function () {
      if (video.textTracks[0].mode == 'hidden') {
        video.textTracks[0].mode = 'showing';
      } else {
        video.textTracks[0].mode = 'hidden';
      }
    }, 'false');
    ```


参考 [Toggling Closed Caption in HTML5 video and disabling default video controls](https://stackoverflow.com/questions/14916914/toggling-closed-caption-in-html5-video-and-disabling-default-video-controls)

如果有多个字幕参考 [Subtitle implementation](https://developer.mozilla.org/en-US/Apps/Fundamentals/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video#Subtitle_implementation)
