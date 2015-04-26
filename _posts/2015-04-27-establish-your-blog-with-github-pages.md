---
layout: post
title: Windows下Github Pages搭建体验
summary: Windows下Github Pages搭建体验
---

建立一个可以自由配置的个人博客对很多人（比如我自己）来说颇有吸引力。关于为什么不用Wordpress等而选择Github Pages无需赘述，可以参见[这篇文章](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html).

很早之前按照该文里的步骤尝试搭建，但一直出现各种错误，甚为头疼。后来终于在Windows下利用Github Pages成功创建里我自己的博客。下面就来分享一下我的经历。

---

首先，Github Pages有两种搭建途径：

1. User & Organization Pages   
2. 项目下的Pages

第一种Pages，每个用户名只能创建一个与自己的用户名同名的博客；而第二种则属于对应的项目，每个项目都可创建对应Pages

之前尝试搭建时，采用阮老师的方法，建立项目Pages，感觉很容易出错。后来发现直接建立第一种Pages更为方便，所以以下只介绍User Pages的情况

---

*Step 1:* 登录github，新建一个repository，命名为username.github.io，其中的username为当前github账户的用户名。

*Step 2:* 依照[官方说明](https://pages.github.com/)建立基本的index.html页面，并push。

*Step 3:* 依照[官方说明](https://help.github.com/articles/using-jekyll-with-pages/)，安装bundle。之后的步骤在cmd中进行：

1. ruby --version 查看ruby版本号。如果未安装ruby则需先安装ruby。推荐使用[Railsinstaller](http://railsinstaller.org/en)，非常快捷简便。
2. 运行
   gem install bundler
   
3. 在项目目录中新建名为Gemfile的文件，不加后缀名。
4. 运行
   source 'https//rubygems.org'
   gem 'github-pages'
    
5. 运行
   bundle install  
如果出现DL开头的两行报错信息，这相当于Warning，可以不管。如果最终提示未安装成功，可以多试几次。
6. 运行
   bundle exec jekyll serve  
   该命令用来启动jekyll server。在浏览器中输入localhost:4000，可以看到博客的index页面。cmd中输入ctrl+c，则可关闭server。运行jekyll server相当于在本地预览效果，之后对博客进行修改或发布博文时可以先在本地随时预览效果。
   
7. 参照[这篇文章](http://justcoding.iteye.com/blog/1959737)中有关目录结构的部分建立目录结构。
8. 参照[这篇文章](http://www.cnblogs.com/purediy/archive/2013/03/07/2948892.html)中配置_config.yml文件的方法进行个人设置。
9. 参照[这篇文章](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)，尝试写一篇博客。注意：不用在_config.yml中配置baseurl，写博客时也不需要引用baseurl。
10. push一下，访问username.github.io查看效果。

如果你的博客成功出现效果，那么恭喜你~

---

进一步配置和修改Jekyll可参照[这篇文章](http://blog.javachen.com/2013/08/31/my-jekyll-config/)。

一些jekyll模板可以[看这里](http://jekyllthemes.org/)。