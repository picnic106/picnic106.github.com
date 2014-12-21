---
layout: post
title: "【翻译】Octopress配置"
date: 2014-10-04 00:47:21 +0800
comments: true
categories: [octopress]
description: "octopress配置"
keywords: octopress,翻译octopress文档,octopress配置
---

[上一篇文章：octopress安装](http://{{ site.url }}/blog/2014/10/03/octopress-setup/)

* any list
{:toc}  

#Octopress配置  

我尝试着让octopress的配置尽量简单，你很可能只需要修改`rakefile`以及`_config.yml`。底下是octopress配置文件的列表：  

{% codeblock  lang:bash octopress配置文件列表%}
    _config.yml       # 主要配置文件 (Jekyll的设置)
    Rakefile          # 部署配置
    config.rb         # Compass配置
    config.ru         # Rack config
{% endcodeblock %}   

Rakefile文件里面的配置关联的几乎都是部署，你甚至都不需要接触他们，除非你使用rsync。  


<!-- more -->  

##博客配置  

在`_config.yml`有三个部分是用于配置你的octopress博客。注意：你必须改变`url`,你很可能改变`title`,`subtitle`以及使用第三方服务。  

{% codeblock  lang:xml octopress配置文件%}
    url:                # 为RSS重新url, 等等。
    title:              # 在页的头和标题标签使用
    subtitle:           # 在头里面的描述
    author:             # 为RSS的作者, Copyright, Metadata
    simple_search:      # 简单的搜索引擎
    description:        # 为你的站点默认的描述
    date_format:        # 使用ruby的时间格式化
    subscribe_rss:      # 你的博客源订阅url，默认是到/atom.xml
    subscribe_email:    # 邮件订阅email
    category_feeds:     # 使用每一个类别rss源订阅
    email:              # Email address for the RSS feed if you want it.
{% endcodeblock %}   

注意：假如你的站点是多作者，你也许想要设置配置文件里面的`author`为你们项目或者公司的名称，然后加作者元数据到文章或者页面，为这些工作添加合适的属性。  

##Jekyll & Plugins  

这些配置被 Jekyll以及插件使用。假如你不熟悉Jekyll，你也许需要看一下[配置文档](https://github.com/jekyll/jekyll/wiki/Configuration)，这个文档列出了这儿没有覆盖的更多属性。  

{% codeblock  lang:xml octopress配置文件%}
    root:               # Mapping for relative urls (default: /)
    permalink:          # Permalink structure for blog posts
    source:             # Directory for site source files
    destination:        # Directory for generated site files
    plugins:            # Directory for Jekyll plugins
    code_dir:           # Directory for code snippets (for include_code plugin)
    category_dir:       # Directory for generated blog category pages
 
    pygments:           # Toggle python pygments syntax highlighting
    paginate:           # Posts per page on the blog index
    pagination_dir:     # Directory base for pagination URLs eg. /blog/page/2/
    recent_posts:       # Number of recent posts to appear in the sidebar
 
    default_asides:     # Configure what shows up in the sidebar and in what order
    blog_index_asides:  # Optional sidebar config for blog index page
    post_asides:        # Optional sidebar config for post layout
    page_asides:        # Optional sidebar config for page layout
{% endcodeblock %}   

假如你想改变为你的博客文章所设置的永久链接方式，请看[Jekyll的永久链接文档](http://jekyllcn.com/docs/permalinks/)。  

**注意**：Jekyll有一个`baseurl`配置，这个配置通过加一个重定向到Jekyll的WEBrick服务提供模拟子目录发布支持。**请不要使用这个**。假如你想要发布你的站点到二级目录，请看[部署octopress到子目录](http://{{ site.url }}/blog/2014/10/04/deploying-to-a-subdirectory/)。  

##第三方服务设置  

这里已经为你设置了第三方集成。简单的填写配置，就会在你的博客展现效果。  

*  **Github** - 在侧边栏列出你的github库
*  **Twitter** - 在文章或者页面加一个分享到Twitter的按钮
*  **Google Plus One** - 为google+社交网络加分享按钮
*  **Pinboard** - 在侧边栏分享你最近的Pinboard记录
*  **Delicious** - 在侧边栏分享你最近的Delicious记录
*  **Disqus Comments** - 加你的Disqus短名使你可以使用评论
*  **Google Analytic** - 加你的谷歌记录id，开启谷歌分析追踪。
*  **Facebook** - 加一个facebook喜欢按钮。

octopress布局将读取这些配置，以及仅仅为可以使用的第三方服务加载需要的js和html。   

[下一篇文章, Octopress博客 »](http://octopress.org/docs/blogging/)  

翻译url:[http://octopress.org/docs/configuring/](http://octopress.org/docs/configuring/)。