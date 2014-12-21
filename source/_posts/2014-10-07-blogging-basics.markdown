---
layout: post
title: "【翻译】博客基础"
date: 2014-10-07 00:00:41 +0800
updated: 2014-10-19 23:40:41 +0800
comments: true
categories: [octopress]
description: "octopress,博客基础,Blogging Basics"
keywords: octopress,翻译octopress文档,博客基础,Blogging Basics
---

* any list
{:toc}  

#博客基础

Octopress提供一些创建文章和页面的rake任务，而这些文章和页面会根据jekyll的命名规则和元数据预先装载。它也会为你的文章生成基于feed的分类和全局(你能在`atom.xml`以及`blog/categories/<category>/atom.xml`发现他们)。  

##博客文章

博客文章必须被保存在`source/_posts`文件夹，而且必须按照jekyll的命名规则来命名：`YYYY-MM-DD-post-title.markdown`。这个文件的名字将被解析做为url的级数，（译者注：例如文件名字是`2014-10-10-test.markdown`，url将是：`/blog/2014/10/10/test`,其实这个url解析设置是可以修改的），文章名称中间的时间帮助文件区别和决定对文章排序顺序。  

<!-- more -->  

Octopress	提供一个rake任务，这个任务使用一个正确的命名约定以及合理的yaml元数据来创建新的文章。  

**语法**

{% codeblock  lang:bash new_post%}
rake new_post["title"]
{% endcodeblock %}  


`new_post`当创建一个文件名时，需要一个自然的文件名，同时会剥离不良的url字符。新文章的默认文件扩展名是`markdown`，但是你能在`Rakefile`里配置它。  

**例子**  


{% codeblock  lang:bash new_post%}
rake new_post["Zombie Ninjas Attack: A survivor's retrospective"]
# 创建 source/_posts/2011-07-03-zombie-ninjas-attack-a-survivors-retrospective.markdown
{% endcodeblock %}    


文件名决定你的访问url。使用默认的[永久链接](http://jekyllcn.com/docs/permalinks/)设置，访问地址会像如下：`http://site.com/blog/2011/07/03/zombie-ninjas-attack-a-survivors-retrospective/index.html`。  

在一个文本编辑器里打开一篇文章，你会在文章最前面看到一块[yaml头信息](http://jekyllcn.com/docs/frontmatter/)，这块代码告诉Jekyll如何处理文章和页面。   


{% codeblock  lang:yaml yaml头信息%}
layout: post
title: "Zombie Ninjas Attack: A survivor's retrospective"
date: 2011-07-03 5:59
comments: true
external-url:
categories:
{% endcodeblock %}    


在这里，你可以给你的文章关掉评论或者分类。假如你的文章有多个作者，你可以加`author: Your Name`到头信息的元数据。假如你正在做草稿，你能加`published: false`到头信息，预防在生成博客的时候，也将草稿生成文章。假如你想发布一个`linklog`形式的文章(博客条目指向外部链接)，只需简单的加一个`external-url`到你的文章。  

你能加一个或者多个分类：  

{% codeblock  lang:yaml yaml头信息%}
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


##新页面  

你能在你博客源目录的任何地方加一个新页面，它们都会被jekyll解析。URL将正确的指向文件路径，所以`about.markdown`将变成`site.com/about.html`。假如你喜欢你的url是`site.com/about/`，那么你要创建的页面为`about/index.markdown`。也有一个很简单的rake任务来生成页面。  

{% codeblock  lang:bash new_page%}
rake new_page[super-awesome]
# creates /source/super-awesome/index.markdown
 
rake new_page[super-awesome/page.html]
# creates /source/super-awesome/page.html
{% endcodeblock %}    


跟创建新文章的任务一样，默认的扩展名也是`markdown`，但是你能在`Rakefile`文件里配置它。一个刚生成的页面可能是这样子的：  


{% codeblock  lang:yaml  new_page%}
layout: page
title: "Super Awesome"
date: 2011-07-03 5:59
comments: true
sharing: true
footer: true
{% endcodeblock %}    

标题是从文件名衍生出来的，所以你可能想改变它。这根生成一个新文章是一样的，除了不包含分类，你可以切换分享以及评论或者干脆移除底部。假如你不想在页面显示时间，你从`yaml`移除它就是了。    

##内容  

网页和文章将被你网站配置文件指定的markup引擎渲染。此外你能使用在 [Jekyll 文章](http://jekyllcn.com/docs/variables/)里描述的任何 [liquid模板功能](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers)。  

插入一个`<!-- more -->`标签到你的文章，将会预防这篇文章这个标签底下的部分显示在你的博客首页。一个`Continue →`的按钮链接到整篇文章。  

##生成和预览  

{% codeblock  lang:bash  生成和预览%}
rake generate   # Generates posts and pages into the public directory
rake watch      # Watches source/ and sass/ for changes and regenerates
rake preview    # Watches, and mounts a webserver at http://localhost:4000 
{% endcodeblock %}    

假如你不想发布这篇文章，而又想生成博客。你可以加`published: false`，到你文章的YAML头。你可以通过`rake preview`在你本地服务器预览这篇文章，但是不会被发布，通过`rake generate`这个命令。  

使用`rake preview`命令是很棒的，因为可以预览。但是假如你有一个[POW](http://pow.cx/)服务，你能像下面这样设置Octopress：  

{% codeblock  lang:bash  POW设置Octopress%}
cd ~/.pow
ln -s /path/to/octopress octopress
cd -
{% endcodeblock %}    

现在你安装好POW，你只要运行`rake watch`和装载`http://octopress.dev`就可以了，代替使用`rake preview`命令。  

也可以看[分享代码片段](http://octopress.org/docs/blogging/code/)和[博客插件](http://octopress.org/docs/blogging/plugins/)。


翻译url:[http://octopress.org/docs/blogging/](http://octopress.org/docs/blogging/)。
