---
layout: post
title: "【翻译】使用RVM安装ruby"
date: 2014-10-03 00:48:21 +0800
comments: true
categories: [octopress]
description: "octopress安装,ruby,使用RVM安装ruby"
keywords: octopress,翻译octopress文档,octopress安装,ruby,使用RVM安装ruby
---

* any list
{:toc}  

##使用RVM安装ruby  

rbenv处理多个Ruby环境的安装和管理。octopress要求安装Ruby 1.9.3，使用RVM你能很简单的安装它。  

<!-- more -->  

###安装RVM  

在你的终端安装如下命令：  

{% codeblock  lang:bash 安装RVM%}
curl -L https://get.rvm.io | bash -s stable --ruby
{% endcodeblock %}      

务必遵循由安装过程指导的任何后续指令。  

###安装Ruby1.9.3  

下一步安装ruby1.9.3:  

{% codeblock  lang:bash 安装ruby1.9.3%}
rvm install 1.9.3
rvm use 1.9.3
rvm rubygems latest
{% endcodeblock %}     

运行`ruby --version`确定你安装的是ruby 1.9.3。假如发现问题，[查看帮助](https://rvm.io/support)。  

[返回安装](http://{{ site.url }}/blog/2014/10/03/octopress-setup/)  

翻译url:[http://octopress.org/docs/setup/rvm/](http://octopress.org/docs/setup/rvm/)。