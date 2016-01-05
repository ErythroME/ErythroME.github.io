---
layout: post
title: favicon和Apple touch icon——以小见大
category: 小细节
tags: [html]
summary: favicon和Apple touch icon都可以作为网站的logo，它们虽然简单且不起眼，却是我们经常见到的标识
---

####什么是favicon？什么是Apple touch icon？
大家有意无意扫过浏览器标签时，很可能看到像这样的页面名前的小图片：

![favicon](http://7xit9q.com1.z0.glb.clouddn.com/faviconAndAppleTouchIcon1.png)

这种小图片就是favicon（favourite icon），它常见于多种浏览器中网页title的左边，收藏夹栏和书签栏中。favicon是一种ico格式的小文件，常用16x16像素的规格，图片要求不超过16色。

而使用苹果系产品时，在Safari中将某个网站加入个人收藏，或将网站添加到主屏后，会看到这样的图片：

![apple touch icon](http://7xit9q.com1.z0.glb.clouddn.com/faviconAndAppleTouchIcon2.png)

这样的小图片就是Apple touch icon，它的作用类似于favicon，也用来标识网站。Apple touch icon一般是png或jpg（不推荐）格式的图片，需要多种规格，如57x57、72x72、114x114和144x144等，分别用来对应不同设备。

---

####制作favicon和Apple touch icon
有很多网站可以根据上传的图片自动生成一系列favicon和Apple touch icon。诸如

*  [Favicon & App Icon Generator](http://www.favicon-generator.org):在这个网站上可以快速制作出包含一个16x16的favicon和一系列Apple touch icon在内的一系列icon，网站还提供完整的引用代码，十分方便。网站还有很多他人制作的icon供下载。
*  [iconifier](http://iconifier.net):和favicon generator类似，但功能较为单一，只能上传文件后生成icon。网站提供图片预览，可以先看效果后下载。
*  [favicon.cc](http://www.favicon.cc):专门制作16x16favicon的网站，十分有趣。用户可以选择上传图片生成favicon（图片不能过于复杂），也可以自己在网站上16x16的网格内作画。制作时可以选择制作静态图片，也可以制作带动态效果的favicon，简直会玩～网站照例会有其他人制作的favicon供分享，不过个人觉得不妨自己尝试制作一下，是非常有意思的体验。

当然也可以自己用Photoshop制作icon。

---

####使用favicon和Apple touch icon
可以直接在页面的head标签内添加

```html
<head>
	<link rel="icon" href="icon-name.ico" type="image/x-icon" />
	<link rel="shortcut icon" href="icon-name.ico" type="image/x-icon" />
</head>
```
即可添加名为icon-name的favicon。

而要Apple touch icon通过link标签的apple-touch-icon属性标明，还需设置sizes属性。以57x57大小的icon为例，代码为：

```html
<head>
	<link rel="apple-touch-icon" href="icon-name.png" sizes="57x57" />
</head>
```

---

####使用中的细节问题
[这篇文章](http://blog.csdn.net/freshlover/article/details/9310437)中介绍了Apple touch icon应用时的图标搜索顺序规则，和去掉图片效果的方法。

而[这篇文章](http://www.jb51.net/article/60004.htm)介绍了在Android中将网页添加到主屏所需的对Apple touch icon的调用方法。

最后，[这篇文章](http://www.cnblogs.com/LoveJenny/archive/2012/05/22/2512683.html)提出了一种解决favicon兼容问题的方法。

