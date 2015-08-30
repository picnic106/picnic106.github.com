---
layout: post
title: "【翻译】octopress文档"
date: 2014-10-02 00:13:49 +0800
comments: true
tags: [octopress]
keywords: octopress,翻译octopress文档,octopress文档
---


  

## Octopress文档  

Octopress是为了Jekyll(一个Github Pages支持的静态博客引擎)而设计的框架。假如你遇到困难，看一下文档，[我很高兴帮助你](http://octopress.org/help/)。假如你发现错误在文档里，发布一个错误，或者fork，然后发送一个拉的请求到主支。  

<!-- more -->  

### 开始吧  
这节将帮助你设置以及解释怎样为你的站点配置octopress。注意：假如你已经有一个其他博客，[查看博客迁移界面](http://jekyllcn.com/docs/migrations/)，帮助你为了形成octopress博客而获取当前博客的设置。  

*   [初始化设置](http://octopress.org/docs/setup/)-获取源代码以及安装依赖
*   [基本配置](http://octopress.org/docs/configuring/)-能使用第三方服务以及自定义你自己的博客  

### 使用octopress  
你的博客应该极好的，让人羡慕的，底下能帮助到你变成这样：  

*   [博客基础](http://octopress.org/docs/blogging/) - 怎样创建文章和页面
*   [部署octopress](http://octopress.org/docs/deploying/) - 部署到Rsync和Github界面服务的简单介绍
*   [分享代码片段](http://octopress.org/docs/blogging/code/) - 简单分享代码片段
*   [博客插件](http://octopress.org/docs/blogging/plugins/) - 博客插件概览
*   [主题和定制化](http://octopress.org/docs/theme/) - 改变主题的指南
*   [更新octopress](http://octopress.org/docs/updating/) - 更新到最新octopress的指南  

### octopress插件 - 使用和例子  

Octopress整个套件有如下插件。许多是专门为octopress而写的，但是有一些是从jekelly社区选择的，而且有很多的更新和改进。  

*   [html5视频标签](http://octopress.org/docs/plugins/video-tag/) - 嵌入mp4编码格式的html5视频
*   [简单代码块](http://octopress.org/docs/plugins/backtick-codeblock/) - 简单轻量级的代码分享
*   [代码块	](http://octopress.org/docs/plugins/codeblock/) - 带有标题和代码链接的代码块分享
*   [包含代码](http://octopress.org/docs/plugins/include-code/) - 使用一个可下载的链接从你的文件系统嵌入代码
*   [gist标签](http://octopress.org/docs/plugins/gist-tag/) - 自动下载和嵌入 Github gists
*   [jsFiddle](http://octopress.org/docs/plugins/jsfiddle-tag/) - 从jsFiddle下载内嵌代码
*   [图片标签](http://octopress.org/docs/plugins/image-tag/) - 很容易的发布图片使用类名和标题
*   [渲染部分](http://octopress.org/docs/plugins/render-partial/) - 插入任何文件到另外的文章和页面
*   [引用块](http://octopress.org/docs/plugins/blockquote/) - 生成漂亮的语义引用块
*   [拉引用](http://octopress.org/docs/plugins/pullquote/) - 仅仅拉引用生成css,没有重复数据，没有js
*   [类别生成器](http://octopress.org/docs/plugins/category-generator/) - 为每一个博客类别生成归档页面
*   [包含多个页面](http://octopress.org/docs/plugins/include-array/) - 包含一系列的界面在config.yml配置
*   [提出](http://octopress.org/docs/plugins/puts/) - 将Liquid的日志提出到终端(为了主题和插件开发者)  

底下的过滤器被octopress使用，并作为不要的记录在他们的源里面。  

Octopress过滤器 - 只是octopress建立liquid过滤器   
网站地图生成器  - 生成一个seo友好的sitemap.xml  
Haml转换        - 允许.haml的界面被jekelly解析
代码高亮        - 将代码片段来突出显示并缓存来加快jekelly的处理
Titlecase       - 被许多插件需要的自动生成合适的标题  

[Octopress插件源](https://github.com/imathis/octopress/tree/master/plugins)  

翻译url:[http://octopress.org/docs/](http://octopress.org/docs/)。
