---
layout: post
title: "使用Octopress和github搭建个人博客"
date: 2014-08-14 16:40:01
comments: true
categories: [Octopress, github]
description: "我的第一篇Octopress博客" 
keywords: Octopress,github,jekyll
---
一、缘起
============================
&emsp;&emsp;一直想搭建一个自己的博客，用于技术积累的记录。例如有些技术问题会一而再、再而三的出现，但是还是每次要上网查找或者花时间回忆解决办法；例如在项目管理中出现的一些感悟，可能是一闪而过，如果不记录下来下次很难再想起来。虽然目前自己有一个技术积累库，记录在word文档里，有两个缺点，一是查找不方便，第二个是不能用于其他码农的相互借鉴：我的解决办法是不是最优解决办法？我的想法是不是有偏差？

&emsp;&emsp;所以花时间搭建了这么一个octopress的博客系统。之前看过wordpress的搭建方法，安装文件越来越大，里面自带的东西也越来越多，php、apache、mysql学习成本也很大。最主要的是需要自己去购买空间安装这些组件。但是我只是需要一个写博客记录并发布给其他志同道合的朋友看而已，为何要这么庞大？所以就一直搁浅。如果我能有一个很方便写博客，且又不需要自己购买空间的方法该有多好！或者是自己太贪心了些。

&emsp;&emsp;正好最近对github感兴趣，听说github是一个在线版本控制平台，许多开源项目都托管在上面，对传统版本控制存有疑虑的人来说，github应该是一个极好的版本控制工具。虽然目前自己也还没有弄明白git的使用方法和规范。某次搜索又看到一篇博文说可以利用github为每个用户以及开源项目创建主页的特性，来创建自己的博客，且不用购买空间来部署，因为github提供jekyll的静态网站生成器。静态网站的一个优势是，不需要用到数据库，文章存储在一个标准的静态网页文件里，随意占用空间小部署简单。我们只需要编写jekyll能解析的轻量级的标签语言(Markdown、Liquid等)书写博客，就可以将博客托管给github。

&emsp;&emsp;但是出于安全问题有些jekyll插件，github不提供解析服务，例如评论、分享功能，但是github提供静态页面解析服务。所以我们可以自己下载jekyll，将轻量级的标签语言转化为静态页面之后，再上传到github，就可以使用博客的一般功能。但是直接使用jekyll可能会带来一些学习成本，所以我找了octopress，这是一个jekyll的博客发布框架，无缝集成git。

&emsp;&emsp;下面具体介绍如何使用这些工具搭建一个轻量级的静态网页博客。
<!-- more -->

* * *



二、需要了解的技术点
============================
**<font size=4>1.git</font>**:是一个开源的项目版本管理工具，如同cvs、svn。由linux的发明者Linus Torvalds编写，用作Linux内核代码的管理。

*   [git主页](http://www.git-scm.com/ "git")。  
*   [git维基百科链接](http://zh.wikipedia.org/wiki/Git "git")。  

**<font size=4>2.github</font>**:利用服务器端部署git技术，提供在线的开源项目版本管理平台，也是一个项目托管平台。提供付费和无偿服务。例如java的很多开源组件都托管在github上。

*   [github主页](https://github.com/ "github")。  
*   [github维基百科链接](http://zh.wikipedia.org/wiki/GitHub "github")。

**<font size=4>3.jekyll</font>**:是一个使用ruby写的，博客形态的静态站点生成器。Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过 Markdown （或者 Textile） 以及 Liquid 转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。

*   [jekyll中国主页](http://jekyllcn.com/docs/home/ "jekyll")。  
*   [jekyll维基百科链接](http://en.wikipedia.org/wiki/Jekyll_(software) "jekyll")。

**<font size=4>4.Liquid</font>**:Liquid是一模板引擎语言，从电子商务系统Shopify提取而来。

*   [Liquid语法](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers "Liquid语法")。

**<font size=4>5.Markdown</font>**:Markdown 是一种轻量级的标记语言，Markdown 的目标是实现「易读易写」。

*   [Markdown语法](http://www.mceiba.com/develop/markdown-syntax.html "Markdown语法")。

**<font size=4>6.Octopress</font>**:是一个为jekyll而设计的框架。单独使用jekyll，你需要写你自己的html模板，css,js,以及设置好配置文件，但是用Octopress，这一切都被托管，你关注的只是写博客。

*   [Octopress主页](http://octopress.org/ "Octopress")。  
*   [Octopress官方安装文档](http://octopress.org/docs/setup/ "octopress官方安装文档")。  

**<font size=4>7.Ruby</font>**:因为jekyll是ruby写的,当然需要按装ruby。Ruby 是一种面向对象、命令式、函数式、动态的通用编程语言。在20世纪90年代中期由日本人松本行弘设计并开发。

*   [Ruby主页](https://www.ruby-lang.org/zh_cn/ "Ruby")。  
*   [ruby维基百科链接](http://zh.wikipedia.org/wiki/Ruby "ruby")。

**<font size=4>8.rubygems</font>**:是一种ruby包管理组件,提供一种分发ruby程序和库的标准格式。

*   [Rubygems主页](http://rubygems.org/ "rubygems")。  
*   [Rubygems维基百科链接](http://en.wikipedia.org/wiki/RubyGems "RubyGems")。

**<font size=4>9.DevKit</font>**:是一个很方便的编译和使用本地c/c++扩展的工具套件，例如windows上的本地ruby扩展。在windows上使用ruby的一个挑战是如何很容易的使用来自于社区的rubygems。因为有些ruby扩展源代码使用了例如make、gcc、sh类似于unix的命令。所以devkit就发明了，为了能在windows上使用类unix命令。

*   [github-DevKit](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit "DevKit")。

**<font size=4>10.python</font>**:是一种面向对象、直译式电脑编程语言，具有近二十年的发展历史，成熟且稳定。它的语法简捷和清晰，尽量使用无异义的英语单词，与其它大多数程序设计语言使用大括号不一样，它使用缩进来定义语句块。

*   [python主页](https://www.python.org/ "python")。  
*   [python维基百科链接](http://zh.wikipedia.org/wiki/Python "python维基百科链接")。


* * *

三、博客搭建
============================
&emsp;&emsp;搭建环境：win7 sp1。  
&emsp;&emsp;主体思路是，既然Octopress是使用jekyll来实现的框架，而jekyll是使用ruby写的，那么必然得安装ruby，ruby扩展需要用到Devkit。而博客空间又需要github实现托管，自然需要下载git工具。另外一个博客代码加亮模块需要python的支持。所以需要安装的软件为：ruby、Devkit、octopress、git、python。  
&emsp;&emsp;为了使ruby使用中文utf-8编码，需要给操作系统加两个环境变量，  

{% codeblock%}
LANG=zh_CN.UTF-8
LC_ALL=zh_CN.UTF-8
{% endcodeblock %}



或者在windows命令窗口执行
{% codeblock windows shell%}
>set LANG=zh_CN.UTF-8
>set LC_ALL=zh_CN.UTF-8
{% endcodeblock %}
这样有一个缺点，一旦命令窗口关掉，又需要重新设置这两个变量。

1.git安装
-------------  
&emsp;&emsp;[git的windows版下载地址](http://git-scm.com/download/win "git的windows版下载地址")。  
&emsp;&emsp;安装没有什么特别之处，按照流程一步一步来就ok。也可参照git官方网站安装介绍：[安装 Git](http://git-scm.com/book/zh/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git "安装 Git")。

2.ruby安装
-------------
&emsp;&emsp;[ruby的windows版下载地址](http://rubyinstaller.org/downloads/ "ruby的windows版下载地址")。    
&emsp;&emsp;Octopress官方文档介绍，最新的Octopress最低依赖于ruby1.9.3。这里如果使用git clone的方式获取的octopress一定要安装大于ruby1.9.3的版本。之前我就是因为clone的是最新版的Octopress，而安装的是ruby1.9.2在之后的操作中出现问题。  
&emsp;&emsp;ruby安装非常简单，需要注意的是，要选中"Add Ruby executables to your PATH"。安装完之后打开windows命令窗口，执行`ruby -v`，如果执行成功，显示ruby版本号，则表示ruby安装成功。  
&emsp;&emsp;更新gem的更新源，ruby的官网经常被拦截，换成国内的更新源。命令如下：
{% codeblock windows shell%}
>gem sources -a http://ruby.taobao.org/
>gem sources -r http://rubygems.org/
>gem sources -l
{% endcodeblock %}

{% img /images/ruby/rubyinstaller.jpg %}
![Add Ruby executables to your PATH](/images/ruby/rubyin.jpg)

3.Devkit安装
-------------
DevKit的下载地址跟ruby的下载地址在一个网页上。选择ruby1.9.3使用的版本。 如果网址打不开，打开[这个网址](https://github.com/oneclick/rubyinstaller/downloads/ )下载devkit。 
安装过程中会要求解压，解压目录最好选择不带中文名和空格的目录。我第一次选择的是带中文的，导致执行之后的命令一直报错。  
安装完之后，使用cmd命令打开windows命令窗口，执行如下命令：  
{% codeblock windows shell%}
>d:
>cd devkit#我的devkit安装在d盘根目录下
>ruby dk.rb init#生成config.yml，这里会检查将要添加DevKit支持的Ruby列表，只支持通过RubyInstaller安装的Ruby。
>ruby dk.rb install
{% endcodeblock %}
4.python安装
-------------
&emsp;&emsp;[python的windows版下载地址](https://www.python.org/downloads/ "ruby的windows版下载地址")，这里下载2.7.8版本。  
&emsp;&emsp;python没有什么特别之处，按照流程来安装就ok。安装成功后，执行`easy_install pygments`，安装博客高亮模块。我执行命令的时候报错，报"不存在的命令"，后来发现是环境变量的问题，python自己加的path环境变量中包含`D:\Python27\Scripts`没有后面的斜杠，正确应该是`D:\Python27\Scripts\`。

5.octopress安装
-------------
&emsp;&emsp;5.1，用命令行下载octopress源码：
{% codeblock windows shell%}
>d:
>git clone git://github.com/imathis/octopress.git  octopress
{% endcodeblock %}
&emsp;&emsp;5.2，更新octopress的更新源：进入d:/octopress目录，用文本编辑器打开gemfile文件，将`source “http://rubygems.org/”`，修改为`source “http://ruby.taobao.org/”`。  
&emsp;&emsp;5.3，安装octopress依赖项： 
{% codeblock windows shell%}
>d:
>cd octopress
>gem install bundler
>bundle install
{% endcodeblock %}
6.登录github，新建主页库(Repositories)。
-------------
&emsp;&emsp;github分为用户主页和项目主页，用户主页就可以作为个人博客，用户主页输入username.github.com就可以进入。用户主页需要登录github用户，建立一个名字为`username.github.com`的库。例如twitter的GitHub主页是：http://twitter.github.com/。       
&emsp;&emsp;没有github的用户，先注册一个github用户。注册之后，登录Github，新建一个库，名字为`username.github.com`,username为你的注册用户名。  
![新建主页库](/images/ruby/github2.jpg)
![新建主页库](/images/ruby/github3.jpg)
![新建主页库](/images/ruby/github4.jpg)  

*说明1*：最好不要勾选init this repo with a readme，因为octopress会自动为我们设置一个readme.md，如果服务器也有一个readme.md,在之后的操作可能会出现不同步的问题。  
*说明2*：需要配置ssh,具体配置请看底下的注意问题1。  


7.部署octopress静态站点到github。
-------------
7.1，进行github_pages设置：  
打开windows命令窗口，输入
{% codeblock windows shell%}
>d:
>cd octopress
>rake setup_github_pages
{% endcodeblock %}
这个rake命令会问你的用户库，按照提示输入新建的用户库地址：
{% codeblock%}
git@github.com:username/username.github.com.git
	或
git@github.com:username/username.github.com
{% endcodeblock %}

不要按照提示来输入`git@github.com:username/username.github.io`，要不然在之后的操作会报错，说找不到库。  
![rake setup_github_pages](/images/ruby/git4.jpg)  


说明1：[rake](http://blog.csdn.net/smilewater/article/details/1683808 "rake")是ruby make，ruby开发的一个项目构建工具。  
说明2：
{% blockquote %}
Github Pages使用master分支，就像web服务器上的公共目录，为我们的站点提供服务。但是在另外一个方面，我们又想要使用source分支，来版本控制项目源代码。`rake setup_github_pages`这个命令就可以全部帮我们设置好。
这个命令会执行如下操作：  
*  询问你主页库地址  
*  重新命名远程点从'origin'到'octopress'  
*  加上我们输入的主页库作为默认的origin remote  
*  转换活动分支从master到source  
*  根据你的库配置博客地址  
*  在_deploy目录设置一个master分支，用于部署。  
{% endblockquote %}

7.2，将静态站点发布到github：
打开windows命令窗口，输入
{% codeblock windows shell%}
>rake install  
>rake generate  
>rake deploy  
{% endcodeblock %}
这个会安装默认博客主题，并生成博客站点，复制博客站点到_deploy文件夹，并将它加入到git,提交发布到github的master分支。几秒之后，在浏览器输入`username.github.com`，应该就可以进入你的博客站点了。  
![blog](/images/ruby/blog.jpg)  

说明：如果想在本地预览博客效果，可以在`rake generate`命令执行之后，执行`rake preview`命令，执行成功，不要关掉命令窗口，在浏览器输入[http://localhost:4000](http://localhost:4000)就可以预览你自己的博客了。  

7.3，别忘了将从github克隆下来的octopress源代码提交到github的source分支：
{% codeblock windows shell%}
>git add .  
>git commit -m 'your message'  
>git push origin source
{% endcodeblock %}
* * *

四、站点配置
============================
&emsp;&emsp;[站点配置介绍](http://jekyllrb.com/docs/variables/)。  
{% blockquote %}
Jekyll允许你很轻松的设计你的网站，这很大程度上归功于灵活强大的配置功能。既可以配置在网站根目录下的 _config.yml 文件，也可以作为命令行的标记来配置。
{% endblockquote %}
&emsp;&emsp;一个_config.yml例子如下：
{% codeblock%}
    url: http://picnic106.github.io
    title: 寧靜致遠
    subtitle: 焚膏油以繼晷，恆兀兀以窮年。
    author: songyj
    simple_search: https://www.google.com/search
    description:
{% endcodeblock %}
你可以修改你博客的url，博客标题，博客的说明，博客作者等。详细站点配置请点击[站点配置](http://jekyllcn.com/docs/configuration/)。

* * *

五、使用博客
============================
&emsp;&emsp;[octopress官方使用文档](http://octopress.org/docs/blogging/)，以下基本是对官方文档的翻译：  

&emsp;&emsp;Octopress提供一些`rake`命令，根据Jekyll的命名规则来创建文章和根据元数据预装载网页。  
1，博客文章
-------------
&emsp;&emsp;博客文章必须被写在`source/_posts`文件夹下，而且命名规则必须依照Jekyll的命名规则：`YYYY-MM-DD-post-title.markdown`。这个文件名字将被用于url解析，时间将被用于定位文件以及文章排序。  
&emsp;&emsp;Octopress提供一些`rake`命令使用正确的命名规则以及正确的yaml元素来创建新的文章：
{% codeblock windows shell%}
rake new_post["title"]
{% endcodeblock %}
&emsp;&emsp;new_post命令要求一个自然的书写标题，以及剥离了创建文件时的不良url字符。默认新文章文章扩展名是markdown，但是在Rakefile文件中可以配置。例如：  
{% codeblock windows shell%}
rake new_post["我的第一篇博客"]
#将创建source/_posts/2014-08-14-我的第一篇博客.markdown文件  
{% endcodeblock %}
&emsp;&emsp;这个文件名决定你的url。根据永久链接设置，新的博客文章访问url将是如下：`http://username.github.com/blog/2014/08/14/我的第一篇博客/index.html`。永久链接的规则是可以设置的，也可以不按照这个规则来，详细规则请看[永久链接设置官方文档](http://jekyllrb.com/docs/permalinks/)。  

&emsp;&emsp;使用一个文本编辑器(例如win7下使用的是notepad++)打开新文章（`source/_posts`）。看到一块yaml头信息设置。
{% blockquote %}
正是头信息开始让 Jekyll 变的很酷。任何只要包含 [YAML 头信息](http://jekyllrb.com/docs/frontmatter/)的文件在 Jekyll 中都能被当做一个特殊的文件来处理。头信息必须在文件的开始部分，并且需要按照 YAML 的格式写在两行三虚线之间。告诉Jekyll如何处理文章和网页。  
{% endblockquote %}
{% codeblock YAML头信息%}
    ---
    layout: post
    title: "我的第一篇博客"
    date: 2014-08-14 5:59
    comments: true
    external-url:
    categories:
    ---   
{% endcodeblock %}
&emsp;&emsp;在这两行的三虚线之间，你可以设置一些预定义的变量或者甚至创建一个你自己定义的变量。这样在接下来的文章和任意模板中或者在包含这些页面或博客的模板中都可以通过使用 Liquid 标签来访问这些变量。  
&emsp;&emsp;这里你还可以把意见（comments）关掉，或者是给你的文章加一个类别。假如这篇文章是几个人同时写的话，还可以加上`author: 你的名字`。如果你的文章只是一个草稿，你还可以加上`published: false`，防止发布到正式博客上。  
你还能加一个简单的类别或者多个类别，例如：
{% codeblock YAML头信息categories配置%}
    # One category
    categories: Sass
     
    # Multiple categories example 1
    categories: [CSS3, Sass, Media Queries]
     
    # Multiple categories example 2
    categories:
    - CSS3
    - Sass
    - Media Queries
{% endcodeblock %}

2，博客网页
-------------
&emsp;&emsp;你可以加一个页面在你博客源目录的任何地方，他们会被Jekyll解析。这个url将直接指定到目录，所以`about.markdown`变成了`site.com/about.html`。Octopress 有一个新建网页的rake命令：  
{% codeblock windows shell%}
rake new_page[super-awesome]
# creates /source/super-awesome/index.markdown
     
rake new_page[super-awesome/page.html]
# creates /source/super-awesome/page.html
{% endcodeblock %}
&emsp;&emsp;跟新建文章命令一样，默认的扩展文件名是markdown，但是你可以在rakefile中配置。一个新生成的页面大概是这样：  
{% codeblock YAML头信息%}
    ---
    layout: page
    title: "Super Awesome"
    date: 2011-07-03 5:59
    comments: true
    sharing: true
    footer: true
    ---
{% endcodeblock %}
3，博客内容
-------------
&emsp;&emsp;在yaml头信息设置后，你可以添加你的博客内容。博客内容可以使用你在站点配置文件中配置的标签语法，（例如Markdown标签语法，第二节有介绍）。这个文章或者网页的内容将被你在站点配置文件设置的标签引擎所渲染。在文章中，你另外你还可以使用liquid模板语法。插入`<!-- more -->`到你的文章将防止低于此标记的后的内容被显示在首页，一个“Continue →”按钮将显示全文。  

3，生成和预览
-------------
{% codeblock windows shell%}
rake generate   # 生成文章或者网页到对外访问的文件夹
rake watch      # Watches source/ and sass/ for changes and regenerates
rake preview    # 查看和启动一个服务，url是http://localhost:4000进行预览。  
{% endcodeblock %}

3，部署到github
-------------
{% codeblock windows shell%}
rake deploy   # 将博客内容发布到github，过几秒，在浏览器网址输入你博客网址(username.github.com)访问你的个人站点。
{% endcodeblock %}

* * *

六、注意问题
============================
1，配置ssh
-------------
在本地安装完git,在github服务器注册完帐号，新建库之后，需要配置ssh密钥。新建库之后需要配置github的ssh密钥,要不然在`rake deploy`部署命令的时候会报错：  
{% codeblock rake deploy报错信息%}
    Permission denied (publickey).  
    fatal: Could not read from remote repository.  
{% endcodeblock %}
[ssh密钥](https://help.github.com/articles/generating-ssh-keys):是一种用来识别受信任计算机的一种方法，而不涉及到密码。下面的步骤将带你产生一个ssh密钥，并将公钥加入到github帐户。  
*步骤1*：检查ssh密钥：检查计算机上是否存在ssh密钥,进入windows用户目录，例如我机器上的用户目录是：C:\Users\username。检查这个目录下是否有.ssh文件夹，如果有检查.ssh文件夹下是否有`id_rsa.pub`或者`id_dsa.pub`文件。如果没有进入第二步，如果已经存在了，进入第三步。  
*步骤2*：生成一个ssh密钥：生成一个密钥，需要执行以下命令，确保git/bin目录存在环境变量PATH里，your_email@example.com修改为你github的注册邮箱：  
{% codeblock windows shell%}
>ssh-keygen -t rsa -C "your_email@example.com"
#这个命令生成一对ssh公钥/私钥，输入一个目录保存ssh密钥，保存到用户目录的.ssh文件夹下。    
{% endcodeblock %}
然后会要求输入密码，不想输入，直接回车，但是官方建议是一定要输入密码。  	
步骤3：配置github帐号的ssh公钥：使用文本文件打开`id_rsa.pub`文件，复制里面的内容，然后把内容加到github帐号。  
&emsp;&emsp;1，点击github帐号设置：  
![进入帐号设置](/images/ruby/zhsz.jpg)  
&emsp;&emsp;2，在左边设置点击“ssh keys”：   
![sshkey](/images/ruby/sshkey.jpg)  
&emsp;&emsp;3，在右边输入ssh密钥描述，然后粘贴你复制的ssh公钥,点击保存：  
![sshsr](/images/ruby/sshsr.jpg)  
&emsp;&emsp;4，测试sshkey是否配置正确，打开本地命令窗口，输入：   
{% codeblock windows shell%} 
>ssh -T git@github.com    
{% endcodeblock %}
如果提示：
{% codeblock ssh提示信息%}   
    Hi picnic106! You've successfully authenticated, but GitHub does not provide shell access.   
{% endcodeblock %}
表示配置成功。  

2，注意rake setup_github_pages命令的库路径
-------------
不要按照提示来输入`git@github.com:username/username.github.io`，要不然在之后的操作会报错，说找不到库。  
![rake setup_github_pages](/images/ruby/git4.jpg)  
那么如果输错了的解决办法是修改octopress/_deploy/.git/config下和你本身站点相关的username.github.io全修改成username.github.com，之后使用`rake deploy`重新部署。例如：  
{% codeblock .git/config配置文件%}
    [remote "origin"]
    url = git@github.com:username/username.github.io.git
{% endcodeblock %}
修改成
{% codeblock .git/config配置文件%}
     [remote "origin"]
     url = git@github.com:username/username.github.com.git
{% endcodeblock %}
3，文件格式问题
-------------
所有文件格式必须是UTF-8的无BOM编码格式，可以使用文本编辑软件进行转换格式，例如notepad++转换格式在菜单：format->转为utf-8无bom编码格式。  
至于什么是bom，且为什么要这样，goole吧，本人也了解不多。如果不这么设置，在有一些命令会报错。  

4，部署到github，报版本不一致问题
-------------
有时候运行`rake deploy`会报错`non-fast-forward errors`,出现这个问题是因为本地文件跟github服务器文件版本不一致，例如上面谈到的，在新建库的时候建立了readme.md文件但是本地进行`rake generate`的时候也生成了readme.md文件，那么就会造成版本不一致问题。  
解决办法：
{% codeblock windows shell%}
>git config branch.master.remote origin  
>git config branch.master.merge refs/heads/master  
>git pull#将远程文件拉到本地，并进行合并merge
>rake deploy#就不会出现问题了
{% endcodeblock %}

（完）
