---
layout: post
title: "在win7下编译apache"
date: 2014-10-20 01:13:20 +0800
comments: true
published: false
tags: [apache]
keywords: apache,编译apache,在win7下编译apache
---


  

# 缘起  

前端时间，公司需要用到[cas单点登录技术](http://zh.wikipedia.org/wiki/%E9%9B%86%E4%B8%AD%E5%BC%8F%E8%AE%A4%E8%AF%81%E6%9C%8D%E5%8A%A1)(Central Authentication Service)，而web服务器是使用apache，所以考虑使用apache的cas客户端模块。但是网上搜寻发现，网上下载的几乎所有的apache的cas模块在windows环境下不能工作，应该都是在linux环境下编译的。所以琢磨着自己在windows环境下编译cas。但是对apache又很陌生，所以为了更好的熟悉apache的编译流程以及原理，自己又在网上下载apache源码，准备在windows环境下编译apache。实际上apache的官方文档中，[windows的编译和安装部分](http://httpd.apache.org/docs/2.2/install.html)说的不是太全面，在编译过程中遇到了很多问题，但是还好都已解决且成功编译。想法是美好的，过程是痛苦的，所以在博客将痛苦的编译过程记录下来，为其他苦逼的程序猿提供借鉴。  


《未完待续》