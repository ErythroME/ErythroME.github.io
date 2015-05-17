---
layout: post
title: 博客装修记(2)——为博客添加分类和标签
category: 博客装修记
tags: [github-pages, jekyll]
summary: 简单的博客搭建完成，可以开始写文章啦~可是纵观整个博客主题，文章页面居然没有分类和标签(◞‸◟)
---

####插件or手动添加
说到给博客添加分类和标签功能，最简单的方法当然是……使用一个带分类和标签功能的Jekyll主题~然而好折腾的我们显然不满意——“教练，有没有更麻烦的方法？”这样的话也可以选择引入一个分类标签插件，然而我们还不满意——
> “教练，我们想要diy！”

---
####认识Liquid
[Liquid](http://docs.shopify.com/themes/liquid-basics)是Jekyll使用的模板语言，它是一种基于Ruby的、非常简单的语言。Liquid的语法详见前面的链接，这里不赘述。

不过，关于Liquid，有一点需要注意：

* 语句用\{ \}包裹，而对象用\{\{ \}\}包裹（改了好久bug发现是括号问题让人忧郁）。

---
####在文章中添加分类和标签
这部分主要参照这位德国小哥[Stephan Groß](http://www.minddust.com)的博文[How To Use Tags And Categories On Github Pages Without Plugins](http://www.minddust.com/post/tags-and-categories-on-github-pages)。

#####分类Category
*Step 1:* 在\_layouts目录下的post.html中,

![decorateMyBlog2nd1](http://7xit9q.com1.z0.glb.clouddn.com/decorateMyBlog2nd1.png)

在Add category处添加如下代码：

![deocrateMyBlog2nd2](http://7xit9q.com1.z0.glb.clouddn.com/decorateMyBlog2nd2.png)










