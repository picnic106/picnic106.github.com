---
layout: post
title: "【翻译】使用Rbenv安装ruby"
date: 2014-10-03 00:24:57 +0800
comments: true
categories: [octopress]
description: "octopress安装,ruby,使用Rbenv安装ruby"
keywords: octopress,翻译octopress文档,octopress安装,ruby,使用Rbenv安装ruby
---

* any list
{:toc}  

##使用Rbenv安装ruby  

rbenv处理多个Ruby环境的安装和管理。octopress要求安装Ruby 1.9.3，使用rbenv你能很简单的安装它。  

<!-- more -->  

###标准的Rbenv安装  

安装Rbenv的标准方法是使用git。运行如下命令：  

{% codeblock  lang:bash 安装Rbenv%}
cd
git clone git://github.com/sstephenson/rbenv.git .rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
source ~/.bash_profile
{% endcodeblock %}   

Zsh用户：将上面的`~/.bash_profile`替换为`~/.zshenv`。  
注意：你可能需要添加`source ~/.bash_profile`到`~/.profile`，依赖于你的bash配置。  

###使用Homebrew替代安装  

假如你在Mac OS X使用  Homebrew，你可能会喜欢这样的安装： 

{% codeblock  lang:bash 安装Rbenv%}
brew update
brew install rbenv
brew install ruby-build
{% endcodeblock %}    

###安装Ruby1.9.3  

下一步安装ruby1.9.3:  

{% codeblock  lang:bash 安装ruby1.9.3%}
rbenv install 1.9.3-p0
rbenv local 1.9.3-p0
rbenv rehash
{% endcodeblock %}    

注意：`rbenv local 1.9.3-p0`确保你自己在使用Ruby 1.9.3-p0安装octopress，而不是其他地方。假如你希望在任何地方使用1.9.3-p0，使用`rbenv global 1.9.3-p0`命令行替代。  

运行`ruby --version`确定你安装的是ruby 1.9.3。假如发现问题，[查看帮助](https://github.com/sstephenson/rbenv/issues)。  

[返回安装](http://{{ site.url }}/blog/2014/10/03/octopress-setup/)  

翻译url:[http://octopress.org/docs/setup/rbenv/](http://octopress.org/docs/setup/rbenv/)。