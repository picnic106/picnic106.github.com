---
layout: post
title: "【翻译】部署到Rsync"
date: 2014-10-03 23:23:46 +0800
comments: true
categories: [octopress]
description: "octopress部署,部署到Rsync"
keywords: octopress,翻译octopress文档,octopress安装,octopress部署,部署到Rsync
---

* any list
{:toc}  

##通过SSH部署rsync  

将你的服务器配置加到Rsync部署配置目录的`rakefile`文件下。部署到rsync，确认你的公钥在文件`~/.ssh/authorized_keys`文件里列出来了。  

{% codeblock  lang:ruby authorized_keys%}
ssh_user       = "user@domain.com"
document_root  = "~/website.com/"
rsync_delete   = true
deploy_default = "rsync"
{% endcodeblock %}  

下一步运行  

{% codeblock  lang:bash %}
rake generate   # If you haven't generated your blog yet
rake deploy     # Syncs your blog via ssh
{% endcodeblock %}   


<!-- more --> 


在你的终端，你的`public`目录将被同步到你服务器帐号的根目录。  

##关于rsync删除  

假如在同步中选择删除，rsync将创建一个1:1的比对。文件将被添加，修改以及删除从你部署目录到你的本地复制镜像。  

假如没有选择删除：  

*  你能存储文件在你的网站部署目录，而这个部署目录还没有被本地版本发现。
*  你本地网站删除的文件必须手动移除服务器端的文件。  

##从同步中排除文件  

假如你想保持octopress文件同步，但是同时你也想很方便的排除一些文件或者目录不跟服务器同步，你可以在rsync中排除他们。  

当同步的时候，rsync可以排除服务器或者本地的文件或者目录。简单的加一个`rsync-exclude`文件，到你项目的根目录，像这样：  

{% codeblock  lang:ruby rsync-exclude%}
some-file.txt
some-directory/
*.mp4
{% endcodeblock %}  

注意：使用排除将防止rsync上传本地文件，或者假如你指定了删除选项，它将防止rsync从服务器删除排除列表里面的文件。  

##版本控制  

你想要在远程git库同步你的博客源。所以设置一个[github库](https://github.com/new)或者[建立一个你自己的主机](#section-2)，然后运行如下命令：  

{% codeblock  lang:bash 配置远程点%}
# Since you cloned Octopress, you'll need to change the origin remote
git remote rename origin octopress
git remote add origin (your repository url)
# set your new origin as the default branch
git config branch.master.remote origin  
{% endcodeblock %}   

##建立你自己的远程仓库  

假如你想设置在你自己服务器的私人git仓库，底下是怎么做。你需要ssh维持访问。  

{% codeblock  lang:bash git ssh%}
ssh user@host.com
mkdir -p git/octopress.git
cd git/octopress.git
git init --bare
pwd  # print the working directory, you'll need it below.
logout
{% endcodeblock %}   

你远程访问库的url是：`ssh://user@host.com/(output of pwd above)`。  

##部署到子目录  

假如你想要建立一个博客在`http://yoursite.com/blog/`,你将需要为[部署到子目录](http://{{ site.url }}/blog/2014/10/04/deploying-to-a-subdirectory/)配置octopress。  

翻译url:[http://octopress.org/docs/deploying/rsync/](http://octopress.org/docs/deploying/rsync/)。   