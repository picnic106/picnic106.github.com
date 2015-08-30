---
layout: post
title: "【翻译】部署到Heroku"
date: 2014-10-03 23:05:33 +0800
comments: true
tags: [octopress]
keywords: octopress,翻译octopress文档,octopress安装,octopress部署,部署到Heroku
---


  

# 部署到Heroku  

假如你还没有heroku帐号，[创建一个](https://api.heroku.com/signup)，它是免费的。然后安装the Heroku gem。  


<!-- more --> 


## 基本的Octopress安装  

第一步确定你安装好了the Heroku gem。  

{% codeblock  lang:bash 安装heroku gem%}
gem install heroku
{% endcodeblock %}    

下一步为你的部署创建应用。假如你是第一次使用heroku,底下的命令将询问你的帐号密码，并自动上传你的ssh的公钥。假如你还没有一个公钥，请点击：[github的向导并创建一个](https://help.github.com/articles/set-up-git/)。  

{% codeblock  lang:bash heroku create%}
heroku create
{% endcodeblock %}   

这个命令将为你的部署创建一个heroku应用，然后创建一个名字叫做“heroku”的git远程点。  

{% codeblock  lang:ruby git远程点%}
#  Set heroku to be the default remote for push/fetch
git config branch.master.remote heroku
{% endcodeblock %}    

编辑库根目录下的`.gitignore`文件，并移除`public`。这个让你将生成后的内容部署到Heroku。  

{% codeblock  lang:bash 部署%}
rake generate
git add .
git commit -m 'site updated'
git push heroku master
{% endcodeblock %}    

这样你就会部署到HeroKu。假如你想配置自己的域名，请看[HeroKu的文档](https://devcenter.heroku.com/articles/custom-domains)。  

翻译url:[http://octopress.org/docs/deploying/heroku/](http://octopress.org/docs/deploying/heroku/)。  