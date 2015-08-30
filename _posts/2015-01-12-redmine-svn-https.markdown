---
layout: post
title: "redmine通过https集成svn"
date: 2015-01-12 19:15:20 +0800
comments: true
tags: [redmine]
keywords: redmine通过https集成svn,redmine,svn,redmine svn,redmine集成svn
---


  

# 缘起  
redmine虽然建好，项目处于使用中，但是没有通过https集成svn，集成后一直报错是心中永远的痛。于是趁周末好好研究了下，其实之前的犯错很简单，没有注意ruby中的反斜杠的重要性。  
我们要明白一点，实际上redmine能集成svn的本质就是：通过ruby调用redmine服务器的svn命令。所以在redmine服务器需要安装svn。因为我的redmine服务器和svn服务器是在同一个服务器，所以这个就不需要再安装svn了。因为我们公司装的是https的svn，所以这里就多了一步在redmine中配置https的客户端证书。  

<!-- more -->

# 安装svn的客户端证书  
输入如下命令：  

{% codeblock lang:cmd%}
cd E:\Bitnami\redmine-2.6.0-1
svn --config-dir webserverRedmine co https://<目标SVN地址>/文件夹名（文件夹名随意，该文件夹会生成在cmd的当前工作目录，是从svn服务器上同步下来的内容，可以删除）
{% endcodeblock %}    

输入完之后会出现提示，输入svn用户名和密码，然后又提示：“是否永久保存ssl凭证?”输入p确定。  
此时会在redmine所在文件夹下生成`webserverRedmine`目录，目录内容为该SVN的ssl凭证。  

# 修改redmine配置  
修改`E:\Bitnami\redmine-2.6.0-1\apps\redmine\htdocs\lib\redmine\scm\adapters\`文件夹下`subversion_adapter.rb`的内容。  
将：
{% codeblock lang:ruby%}
def credentials_string 
str = '' 
str << " --username #{shell_quote(@login)}" unless @login.blank? 
str << " --password #{shell_quote(@password)}" unless @login.blank? || @password.blank? 
str << " --no-auth-cache --non-interactive " 
str end 
{% endcodeblock %}   

修改为：

{% codeblock lang:ruby%}
def credentials_string 
str = '' 
str << " --username #{shell_quote(@login)}" unless @login.blank? 
str << " --password #{shell_quote(@password)}" unless @login.blank? || @password.blank? 
str << " --no-auth-cache --non-interactive --config-dir E:/Bitnami/redmine-2.6.0-1/webserverRedmine" 
str end 
{% endcodeblock %}   

***注意：上面config-dir配置的斜杠:`E:/Bitnami/redmine-2.6.0-1/webserverRedmine`,之前一直没有弄好的主要原因就是，自以为是的直接从windows资源管理器复制路径:`E:\Bitnami\redmine-2.6.0-1\webserverRedmine`，导致ruby读取不到，这里以后要格外注意ruby的路径反斜杠问题。***  


然后在redmine中配置svn就可以使用了。 


 
 