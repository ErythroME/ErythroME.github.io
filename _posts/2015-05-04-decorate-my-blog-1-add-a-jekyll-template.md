---
layout: post
title: 博客装修记(1)——添加一个Jekyll主题
updated: 2015-05-17
category: 博客装修记
tags: [github-pages, jekyll]
summary: 要搞一个炫酷的个人博客，搭建好Github Pages只是第一步，接下来就要引入一个Jekyll主题。我选择的主题是Pixyll

---

#### 为什么要选择主题

因为懒TAT。

首先，刚接触Jekyll时，引入主题可以让我们快速地了解Jekyll。模板的目录结构及参考代码一般都比较工整，值得参考。其次，对于广大程序猿来说，辛苦手写的页面很容易丑到掉渣，引入模板之后再根据自己的心意修改更为便捷。

在[Jekyll Themes](http://jekyllthemes.org)上有一些简单的主题，我选择了[Pixyll](https://github.com/johnotander/pixyll)。看着太简单？简单才有修改的空间嘛~

为了再现我的博客装修过程，我在Github上新建了一个Jekyll主题项目：[Mixyll](https://github.com/ErythroME/Mixyll)。

---

#### 引入Pixyll

引入Pixyll非常简单——复制+粘贴。

* 在Github上fork Pixyll。
* 在本机的Github目录下运行 <span class="command"><span>git clone https://github.com/johnotander/pixyll.git</span></span> 将Pixyll clone下来。

在将Pixyll中的内容复制到我们的博客目录前，先来看一下Pixyll中原本都有些什么内容：
![Pixyll 目录](http://7xit9q.com1.z0.glb.clouddn.com/decorateMyBlog1st1.png)

* 大体了解以后在命令行中运行 <span class="command"><span>cp -r pixyll/ Mixyll</span></span> 将pixyll目录下的所有文件复制到博客目录中（我的目录名称为Mixyll）。

---

#### 修改Pixyll的配置信息

在配置文件\_config.yml中，将下面的代码修改为自己的信息：
{% highlight yaml %}
# Site settings
title:       Pixyll
email:       your_email@example.com
author:      John Otander
description: "A simple, beautiful theme for Jekyll that emphasizes content rather than aesthetic fluff."
baseurl:     ""
url:         "http://pixyll.com"
{% endhighlight %}
在这里还可添加文章url的格式，我的设置是/类别/年份/月份/日期/题目
{% highlight yaml %}
permalink: /:category/:year/:month/:day/:title
{% endhighlight %}

接下来,

* 开启页面浮现的动画效果：animated置为true
* 可在每篇文章的末尾添加作者信息：将show\_post\_footers置为true

    > 需要注意：如果show\_post\_footers设为true，则需要将\_include文件夹下的post\_footer.html中的相应内容替换为自己的信息。
	
* 在博客header内显示社交网络图标：show\_social\_icons置为true，并填写相应社交网络的用户名、id等信息

配置文件\_config.yml修改完毕后，运行 <span class="command"><span>jekyll serve</span></span> 会看到页面头部标题已经变成了自己在\_config.yml中设置的title，nice~

---

#### 修改Pixyll的基本信息

之后就是修改页面啦~需要修改的页面有以下几个：

* about.md
* footer.html (_includes内)
* post\_footer.html  (\_includes内)

分别将其修改为自己的信息，不要忘记感谢模板的原作者哟~

---

至此，主题的基本信息修改完成，在本地运行jekyll没有报错的话就可以提交了。

将修改的内容push后，你会看到修改完成的页面；如果没看到，可以稍等几分钟；如果等了半天也没看到……duang duang duang

> <strong>运行 <span class="command"><span>git commit -m 'rebuild pages' --allow-empty</span></span> 来强制github pages rebuild</strong>

刷新后顿时![有意思~](http://7xit9q.com1.z0.glb.clouddn.com/decorateMyBlog1st2.jpg)


