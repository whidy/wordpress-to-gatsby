---
author: whidy
comments: true
date: 2014-08-05 02:22:42+00:00
template: post
draft: false
link: http://www.whidy.net/jsp-loop-var-a-variable-name.html
slug: /jsp-loop-var-a-variable-name
title: JSP循环中为变量名赋值一个变量名?
wordpress_id: 2570
category: '开发'
tags:
- JSTL
- 技术
---

标题我也不知道怎么说的好.不过还是得描述一下:

在一个三次循环的代码内,我新建一个变量,让每次循环,这个变量的名称都不同,而且三个变量的值也不同.如何才能最简单的写出来呢?

先来看看一段错误的(天真的代码):

    
    ```html
    <%@ page language="java" contentType="text/html; charset=gbk"
     pageEncoding="GBK"%>
    <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
    <%@ taglib prefix="s" uri="http://java.sun.com/jsp/jstl/sql" %>
    <%@ taglib prefix="f" uri="http://java.sun.com/jsp/jstl/fmt" %>
    <%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=gbk">
    <title>Insert title here</title>
    </head>
    <body>
    <c:set var="arry">aaa|6,bbb|6,ccc|4</c:set>
    <c:forTokens var="item" items="${arry}" delims="," varStatus="vs">
     <c:set var="index" value="${vs.count}"></c:set>
     <c:set var="tit">${fn:split(item,'|')[0]}</c:set>
     <c:set var="num">${fn:split(item,'|')[1]}</c:set>
     <c:set var="p${vs.count} }">
     name: ${tit}, number: ${num} <br />
     </c:set>
    </c:forTokens>
    ${p1}${p2}${p3}
    <!--
    期望输出
    栏目名称: 评测, 该栏目输出文章数量为6
    栏目名称: 导购, 该栏目输出文章数量为6
    栏目名称: 文化, 该栏目输出文章数量为4
    -->
    </body>
    </html>
    ```


当然上面肯定不能输出成功的.根本**不能**在c:set内创建一个含有变量的变量名**<del>var="p${vs.count}"</del>**!

所以我只好改成下面这段:

    
    ```html
    <%@ page language="java" contentType="text/html; charset=gbk"
     pageEncoding="GBK"%>
    <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
    <%@ taglib prefix="s" uri="http://java.sun.com/jsp/jstl/sql" %>
    <%@ taglib prefix="f" uri="http://java.sun.com/jsp/jstl/fmt" %>
    <%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=gbk">
    <title>Insert title here</title>
    </head>
    <body>
    <c:set var="arry">aaa|6,bbb|6,ccc|4</c:set>
    <c:forTokens var="item" items="${arry}" delims="," varStatus="vs">
     <c:set var="index" value="${vs.count}"></c:set>
     <c:set var="tit">${fn:split(item,'|')[0]}</c:set>
     <c:set var="num">${fn:split(item,'|')[1]}</c:set>
     <c:set var="p">
     name: ${tit}, number: ${num} <br />
     </c:set>
     <c:if test="${vs.count == 1}">
     <c:set var="p1" value="${p}"></c:set>
     </c:if>
     <c:if test="${vs.count == 2}">
     <c:set var="p2" value="${p}"></c:set>
     </c:if>
     <c:if test="${vs.count == 3}">
     <c:set var="p3" value="${p}"></c:set>
     </c:if>
    </c:forTokens>
    ${p1}${p2}${p3}
    </body>
    </html>
    ```


那么很显然这段代码很臃肿,而且适用条件很有限,我认为在循环次数小于或等于3的情况下或许可以考虑,若是有5条甚至更多的时候,那么写这么多判断不如直接给每个变量进行赋值,那么我最近问了一些朋友,却找不出来更好的解决办法.今天的思考暂时告一段落.下次我来分享一些关于jstl的资料吧.

其他关于jstl学习资料请看: [JSTL相关资料手册打包学习及研究](http://www.whidy.net/jstl-learning-doc-api.html)
