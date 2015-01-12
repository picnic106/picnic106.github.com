---
layout: post
title: "redmine安装代码评审和编辑器插件"
date: 2015-01-12 17:49:13 +0800
comments: true
categories: [redmine]
description: "redmine安装代码评审(redmine_code_review)和编辑器插件(redmine_wysiwyg)"
keywords: redmine代码评审插件,redmine_code_review,redmine_wysiwyg,redmine编辑器插件,代码评审插件,redmine编辑器插件,redmine
---

* any list
{:toc}  

#缘起  

redmine用了一段时间,感觉还不错。如果加一个编辑器标签，加一个代码评审标签就更好了。网上搜了很多，决定加redmine_code_review代码评审插件和redmine_wysiwyg编辑插件。   

redmine版本：redmine-2.6.0  
ruby版本：2.0.0  
ruby on rails版本：3.2.19  

<!-- more -->

#插件下载   

##code_review代码评审插件下载  

*   [redmine的code_review代码评审主页](http://www.redmine.org/plugins/redmine_code_review)  
*   [代码评审插件最新0.6.4版本下载地址](https://bitbucket.org/haru_iida/redmine_code_review/downloads)    

##redmine_wysiwyg编辑插件下载  

*   [redmine的编辑插件github主页](https://github.com/stpl/redmine_wysiwyg)   
*   下载：点击github主页右下角"Download ZIP"就可以下载下来。  

#插件安装   

##复制到redmine的plugin目录  
将下载下来的打包文件解压缩，复制到redmine服务器的plugin目录，因为我是通过Bitnami组件安装的redmine，所以我自己服务器的redmine插件路径是：`E:\Bitnami\redmine-2.6.0-1\apps\redmine\htdocs\plugins`。  

##插件集成  
如果你的redmine是1.X.X的版本，集成命令是`rake db:migrate RAILS_ENV=production`，如果是2.X.X版本，命令是`rake redmine:plugins:migrate RAILS_ENV=production`。  

***注意：因为rake命令在htdocs\bin文件夹下，而rake文件却在htdocs文件夹下，所以如果在htdocs文件夹下输入rake命令是找不到的，因为rake命令在bin文件加下，所以我使用了一个变通的方法：`ruby bin\rake redmine:plugins:migrate RAILS_ENV=production`。我认为这是一个bug，但是通过变通方式可以解决。***  



###环境变量设置  
在执行集成命令之前需要设置环境变量，以便命令环境知道ruby、rake、gem命令。Bitnami的环境变量文件在`E:\Bitnami\redmine-2.6.0-1\scripts\setenv.bat`,设置好环境变量后，将目录切换到redmine目录，输入集成命令。  

###代码评审插件集成  
代码评审插件集成步骤比较简单因为不用额外加载另外的ruby插件。命令如下：  
  
{% coderay lang:cmd%}
cd E:\Bitnami\redmine-2.6.0-1\scripts  
setenv  
cd E:\Bitnami\redmine-2.6.0-1\apps\redmine\htdocs
ruby bin\rake redmine:plugins:migrate RAILS_ENV=production
{% endcoderay %}  

输出如下图就算集成成功了：   

![img](/images/redmine/评审插件安装.png)

###编辑器插件集成  
编辑器插件集成就复杂一点，因为它还依赖了其他的包。  
***1,安装需要的gem***    

{% coderay lang:cmd%}
bundle install --without development test
{% endcoderay %}  

但是我输入之后报如下错误：  

![img](/images/redmine/编辑器安装1.png)  

因为对ruby不是太熟悉，虽然自学过。网上说就按照ruby的提示来就行。  

{% blockquote %}
ruby的伟大之处就是，即使你出错了，但是你按照ruby的提示一步一步来就没问题。
{% endblockquote %}

所以我按照提示输入：`bundle install --no-deployment`,但是还是报错了，报如下错误：  

![img](/images/redmine/编辑器插件安装2.png)   
![img](/images/redmine/3.png)

根据提示来，貌似是少了python相关包，如果真是少了python这个包，心想麻烦了，还得安装python。  
但是先继续按照提示来吧，输入如下命令：`gem install libv8 -v '3.11.8.17'`，却报如下错：  
![img](/images/redmine/4.png)    
之前遇到过这个问题，貌似原因是，gem库是`https://rubygems.org`，客户端链接https链接的时候缺少证书认证。想到一招是指定gem库为http的。  
于是输入如下命令：`gem install libv8 -v '3.11.8.17' --source http://rubygems.org`  
但是还报错了：  
![img](/images/redmine/5.png)    
这下没招了，继续google吧，还别说真找到老外一篇相关文章，还真别说google的准确度比baidu要强不知多少倍。  
根据搜索结果输入如下命令：  

{% coderay lang:cmd%}
gem install libv8 -v '3.11.8.17' --source http://rubygems.org -- --with-system-v8
{% endcoderay %}  

这里不知`--with-system-v8`这个参数有什么作用，留着以后自学ruby的时候再思考吧，这里先把插件安装搞定了。  

这里libv8插件安装成功了，继续输入`bundle install --no-deployment`吧。结果如下就表示没有问题了，编辑器依赖的包终于安装成功了。  
![img](/images/redmine/6.png)  

***2,编辑器插件集成***   
到这一步就是编辑器集成了，输入如下命令：   

{% coderay lang:cmd%}
ruby bin\rake redmine:plugins:migrate RAILS_ENV=production
{% endcoderay %}  

输入如下所示就表示，将redmine重启时候，代码审核和编辑插件都可以使用了：  

![img](/images/redmine/7.png)   

#插件使用

##代码审核插件使用  
redmine重启之后，需要使用管理员帐号登录redmine帐号，配置代码审核模块，就可以正常同svn使用代码审核功能了。如下图所示：  
 
![img](/images/redmine/8.png)   

![img](/images/redmine/10.png) 

![img](/images/redmine/9.png)   

![img](/images/redmine/11.png)    

##编辑器插件使用  
redmine重启之后，需要使用管理员帐号登录redmine帐号，修改配置中的文本格式。如下图所示：  
![img](/images/redmine/12.png)   
![img](/images/redmine/13.png) 
