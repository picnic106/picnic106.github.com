---
layout: post
title: "【翻译】octopress安装"
date: 2014-10-03 00:06:10 +0800
comments: true
categories: [octopress]
description: "octopress安装"
keywords: octopress,翻译octopress文档,octopress安装
---

* any list
{:toc}  

##Octopress安装  

首先我想要强调Octopress是一个为骇客准备的博客框架。你应该很自然的运用shell命令以及很熟悉git的基本知识。假如那听起来让人为难的，可能octopress不适合你。  

<!-- more -->  

###在你开始之前  

1.  [安装git](http://git-scm.com/)  
2.  安装ruby 1.9.3或者很熟练的使用[rbenv](http://{{ site.url }}/blog/2014/10/03/installing-ruby-with-rbenv/)或者[RVM](http://{{ site.url }}/blog/2014/10/03/installing-ruby-with-rvm/)。  

假如`ruby --version`没有告诉你正在使用ruby至少1.9.3版本，重新审视你安装[rbenv](http://{{ site.url }}/blog/2014/10/03/installing-ruby-with-rbenv/)或者[RVM](http://{{ site.url }}/blog/2014/10/03/installing-ruby-with-rvm/)的过程。  

###安装Octopress  

{% codeblock  lang:bash 安装octopress%}
git clone git://github.com/imathis/octopress.git octopress
cd octopress
{% endcodeblock %}  

下一步安装依赖  

{% codeblock  lang:bash 安装依赖%}
gem install bundler
rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
bundle install
{% endcodeblock %}   

安装octopress默认主题   

{% codeblock  lang:bash 安装默认主题%}
rake install
{% endcodeblock %}   

下一步：  

*   [部署设置](http://{{ site.url }}/blog/2014/10/04/deploying/)
*   [博客配置](http://{{ site.url }}/blog/2014/10/04/configuring-octopress/)
*   [正式开始使用octopress撰写博客吧](http://octopress.org/docs/blogging/) 

翻译url:[http://octopress.org/docs/setup/](http://octopress.org/docs/setup/)。
