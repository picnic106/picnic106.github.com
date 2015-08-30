---
layout: post
title: "【翻译】部署到子目录"
date: 2014-10-04 00:04:41 +0800
comments: true
tags: [octopress]
keywords: octopress,翻译octopress文档,octopress安装,octopress部署,部署到子目录
---

假如你部署一个子目录到你的网站，你可以使用github的项目页，确信你正确配置好了你的urls。你几乎可以自动化实现：  

{% codeblock  lang:bash 配置urls%}
rake set_root_dir[your/path]
 
#  To go back to publishing to the document root
rake set_root_dir[/]
{% endcodeblock %}   

<!-- more --> 

然后如下更新你的`_config.xml`以及`Rakefile`:  

{% codeblock  lang:xml _config.xml%}
#  _config.yml
url: http://yoursite.com/your/path
 
#  Rakefile (if deploying with rsync)
document_root = "~/yoursite.com/your/path"
{% endcodeblock %}     

要手动配置部署到子目录，你将改变`_config.yml`，`config.rb` 以及`Rakefile`。底下是一个部署站点到`/awesome`子目录的例子：  

{% codeblock  lang:ruby _config.xml，config.rb，Rakefile %}
#  _config.yml
destination: public/awesome
url: http://example.com/awesome
subscribe_rss: /awesome/atom.xml
root: /awesome
 
#  config.rb - for Compass & Sass
http_path = "/awesome"
http_images_path = "/awesome/images"
http_fonts_path = "/awesome/fonts"
css_dir = "public/awesome/stylesheets"
 
#  Rakefile
public_dir = "public/awesome"
#  If deploying with rsync, update your Rakefile path
document_root = "~/yoursite.com/awesome"  
{% endcodeblock %}  

翻译url:[http://octopress.org/docs/deploying/subdir/](http://octopress.org/docs/deploying/subdir/)。   
