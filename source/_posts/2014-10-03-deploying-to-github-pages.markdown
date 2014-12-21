---
layout: post
title: "【翻译】部署到Github Pages"
date: 2014-10-03 01:19:23 +0800
comments: true
categories: [octopress]
description: "octopress部署,部署到Github Pages"
keywords: octopress,翻译octopress文档,octopress安装,octopress部署,部署到Github Pages
---

* any list
{:toc}  

##使用github的用户或者组织页  

假如你想要从`http://username.github.io`拥有一个博客(虽然你也有[自己的域名](http://{{ site.url }}/blog/2014/10/03/deploying-to-github-pages/#section))，就使用这个方法。在过去github使用`http://username.github.com`作为域名,但是正在使用io扩展代替Pages。  

创建一个[新的github库](https://github.com/new)，将这个库的名字命名为这种格式的：`username.github.io`，username是你的github用户名或者组织名。  

Github Pages为用户以及组织使用主分支就像web服务器使用公共目录，在你的http://username.github.io网页提供文件。但是你想要在source分支下工作，例如编辑博客文章，然后提交生成后的博客内容到主分支。Octopress有一个帮助你这样设置好的配置命令。  

<!-- more --> 

{% codeblock  lang:bash github pages配置%}
rake setup_github_pages
{% endcodeblock %}    

这个rake命令将询问你的github库url。复制来自于你新创建好的库的ssl或者https的url(例如：`git@github.com:username/username.github.io.git`)，然后作为回应粘贴到里面。  

这个命令将会做如下动作：  

1.  询问以及存储你的github pages的库url。
2.  将imathis/octopress远程点的名称'origin'修改为'octopress'。
3.  加入你的github pages库作为默认的origin远程点。  
4.  切换活动分支从主分支到源分支。  
5.  根据你的库url配置你的博客url。  
6.  在_deploy文件夹设置一个主分支用于部署。	  

下一步运行：  

{% codeblock  lang:bash github rake deploy%}
rake generate
rake deploy
{% endcodeblock %}  

这个将生成你的博客，复制生成好的文件到`_deploy/`,然后将他们加入到git，提交以及推送他们到github的主分支。在之后几秒钟之内，你会收到一封来自与github的email，告诉你你的提交已经被接收以及将被部署到你的站点。  

**不要忘记**将你的博客开发代码提交到源分支。  

{% codeblock  lang:bash github 提交到源分支%}
git add .
git commit -m 'your message'
git push origin source
{% endcodeblock %}   

注意：使用新库，github会设置基于你第一次推送的分支作为你的默认的分支，然后它将存放你生成的内容。假如你使用github部署你的博客出现问题，点击你库的管理面板，然后确认主分支是默认的分支。  

更多关于你第一篇文章的信息，请阅读[博客基本设置](http://octopress.org/docs/blogging/)。  

##使用github项目页（gh-pages）  

github项目页服务允许你为你的开源项目形成一个站点。github将寻找你库里面的`gh-pages`分支，然后确定在url（例如：`http://username.github.io/project`）的内容是可用的。  

底下能设置octopress站点到gh-pages库：  

{% codeblock  lang:bash github pages配置%}
rake setup_github_pages
{% endcodeblock %}    

有如下几个步骤：  

1.  询问你项目库的url。
2.  将imathis/octopress远程点的名称'origin'修改为'octopress'。
3.  在_deploy文件夹设置一个gh-pages分支用于部署。	  

下一步运行：  

{% codeblock  lang:bash github rake deploy%}
rake generate
rake deploy
{% endcodeblock %}  

这个将生成你的博客，复制生成好的文件到`_deploy/`,然后将他们加入到git，提交以及推送他们到github的主分支。在之后几秒钟之内，你会收到一封来自与github的email，告诉你你的提交已经被接收以及将被部署到你的站点。  

现在你已经有一个地方用于提交生成好的内容，但是你也应该设置一个库用于存储博客的源代码。在你为博客源代码设置好一个库之后，把如下加到origin的远程点。  

{% codeblock  lang:ruby 添加origin远程点%}
git remote add origin (your repo url)
# set your new origin as the default branch
git config branch.master.remote origin
{% endcodeblock %}    

目前位置你可以推送你所有的改变了。  

##自定义域名  

第一步在你的博客源代码路径新建一个名为cname的文件。  

{% codeblock  lang:bash 新建cname%}
echo 'your-domain.com' >> source/CNAME
# OR
echo 'www.your-domain.com' >> source/CNAME
{% endcodeblock %}     

下一步你需要访问你的域名注册商或者DNS主机，然后在你的域名字加一条记录。  

*  创建一个子域名，例如：`www.example.com`,你应该很简单的创建一个cname记录点到`charlie.github.io.`。  
*  假如你使用顶级域名，例如：`example.com`，你必须使用一个A记录到`192.30.252.153`或者`192.30.252.154`。  

**不要使用顶级域名创建一条CNAME记录**！！它也许在其他服务例如邮件有不良的副作用。许多DNS服务允许你在TLD上创建CNAME,虽然你不会。记住dns的改变也许需要一整天才会生效，所以需要耐心。  

源：[github pages向导](https://help.github.com/categories/github-pages-basics/)  

翻译url:[http://octopress.org/docs/deploying/github/](http://octopress.org/docs/deploying/github/)。