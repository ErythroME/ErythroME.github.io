---
layout: post
title: 神器Alfred和更神的workflow
category: 工具
tags: [alfred, workflow]
summary: 虽然在Mac下Spotlight有很多强大的功能，但与Alfred相比还是略有欠缺。而武装各式workflow后Alfred堪称神兵利器~

---
#### Spotlight与Alfred

OS X 中集成的Spotlight拥有快速文件检索、快速打开应用、计算等功能，感觉非常方便。Spotlight中我最喜欢的功能是下面这个快速检索和预览文件

![快速文件检索和预览文件](http://7xit9q.com1.z0.glb.clouddn.com/AlfredAndSomeUsefulWorkflowsImage1.png)

[Alfred](http://www.alfredapp.com)与Spotlight相似，它除了使用同Spotlight一样的索引来完成基本功能外，还具有很多优点。不过与其强大功能相对应的是价格：最低要£17，终身免费升级的Mega Supporter需要£32，大约三百软妹币。程序猿建议直接上Mega Supporter，Alfred绝对对得起每一分钱~看到小清新的界面就很舒心有木有~

![Alfred](http://7xit9q.com1.z0.glb.clouddn.com/AlfredAndSomeUsefulWorkflowsImage3.png)

---
#### Alfred中的Snippets

虽然人们一提Alfred必提workflow，但我还是想先介绍一下Snippets。

用户可以利用Snippets设置一些固定的、较长的输入，以option+cmd+c键唤起，之后就可以直接选择或者用关键字搜索Snippet，对应文本将直接填入光标处。![Snippets](http://7xit9q.com1.z0.glb.clouddn.com/AlfredAndSomeUsefulWorkflowsImage2.png)

Snippets功能非常简单，不过用了才发现，小小功能省不少事哟~

---
#### 花式workflow

购买Alfred的Powerpack后，就可以尽情搜索各式workflow，也可以自己动手编写。筒子们，你们的征途是workflow大海~

下面是我常用的workflow

##### [VPN Toggle](https://github.com/superkam/Alfred2_VPNToggle)

由于我是VPN重度用户——每天打开电脑第一件事就是开VPN，这个workflow对我来讲堪称神器。VPN Toogle用来自由开关VPN，或者在多个VPN代理之间切换。我个人用的是[云梯VPN](http://opticalvpn.com/?r=e4898da811f3c34e)（这是我的链接），感觉切换起来很方便，也有多种选择，比一些免费VPN要稳定。

![VPN Toggle](http://7xit9q.com1.z0.glb.clouddn.com/AlfredAndSomeUsefulWorkflowsImage4.png)

##### [Kill Process](https://github.com/nathangreenstein/alfred-process-killer)

这个Workflow用来关掉进程，当然也能关闭应用。由于Mac下点击左上角的红色关闭按钮仅仅是关闭了窗口，并未关闭进程，有时感觉会有不便。导入这个workflow之后只需唤起Alfred，输入kill+应用名称（或进程名），即可将其关闭，十分简捷。

![Kill Process](http://7xit9q.com1.z0.glb.clouddn.com/AlfredAndSomeUsefulWorkflowsImage5.png)

##### [HTTP codes](https://github.com/JoelQ/alfred-http)

一个方便程序猿的小工具。只要在Alfred输入http+状态码，便可以查到其所对应的状态信息。治疗健忘的神器~

![HTTP codes](http://7xit9q.com1.z0.glb.clouddn.com/AlfredAndSomeUsefulWorkflowsImage6.png)

##### [知乎](https://github.com/KJlmfe/Alfred-workflows/raw/master/zhihu.alfredworkflow)

知乎重度患者适用。zh+关键词可以搜索问题、话题和人，zhdaily可以看到知乎日报条目。利用了Alfred 2的feedback特性，搜索结果都可在Alfred中显示条目，很赞。

![知乎](http://7xit9q.com1.z0.glb.clouddn.com/AlfredAndSomeUsefulWorkflowsImage7.png)

---
还有很多有意思的workflow，可以查看这些网页：

* [Alfred官网的分享区](http://www.alfredforum.com/forum/3-share-your-workflows/)
* [知乎上大家的推荐](http://www.zhihu.com/question/20656680)
* [一个收集workflow的网站](http://www.alfredworkflow.com)（这里有的workflow貌似无法下载）