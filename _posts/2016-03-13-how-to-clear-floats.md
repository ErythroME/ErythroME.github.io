---
layout: post
title: 清除浮动与clear both
category: CSS
tags: [style]
summary: 很多情况下都需要清除浮动，本文介绍一些清除浮动的方法

---

#### 为什么要清除浮动

简单来说，有时出于布局考虑，需要对一些元素设置float属性，这时经常会引起与之相关的元素的位置产生变化，为了让这些元素的位置恢复正常，就需要清除浮动。

[这里](http://stackoverflow.com/questions/12871710/what-does-the-css-rule-clear-both-do)有对为什么要清除浮动的详细解释。用更精确的话来解释：

> ...why the background of a container element is not stretched when it holds floated elements. It's because the container element is a POOL here and the POOL has no idea how many objects are floating, or what the length or breadth of the floated elements are, so it simply won't stretch.

> Another reason the clear: both; is used is to prevent the element to shift up in the remaining space.

总结起来，在两种情况下需要清除浮动：

1. 兄弟元素：未设float属性的元素可能会出现在我们不希望它出现的空白处
2. 父子元素：由于子元素设置了float，导致父元素不能正常包裹子元素

---

#### 处理兄弟元素

先来看一种简单情况：将bottom块放在left和right块下方

~~~ html
<div>
	<div class="left">left</div>
	<div class="right">right</div>
	<div class="bottom">bottom</div>
</div>
~~~

相关CSS如下：

~~~ css
.left {
	float: left;
	width: 100px;
	height: 100px;
	background-color: red;
}
.right {
	float: right;
	width: 100px;
	height: 100px;
	background-color: blue;
}
.bottom {
	/* clear: both; */
	width: 100%;
	height: 100px;
	background-color: yellow;
}
~~~

这时的显示效果：

![未clear: both的兄弟元素](http://7xit9q.com1.z0.glb.clouddn.com/howToClearFloats1.png)

这种情况下，只需简单地**为.bottom添加clear: both**，就会得到正常显示：

![clear: both后的兄弟元素](http://7xit9q.com1.z0.glb.clouddn.com/howToClearFloats2.png)

---

#### 处理父子元素

代码如下：

~~~ html
<div>
	<div class="box">
		<div class="left">left</div>
		<div class="right">right</div>
	</div>
</div>
~~~

~~~ css 
.box {
	border: 5px solid #aaaaaa;
}
.left {
	float: left;
	width: 100px;
	height: 100px;
	background-color: red;
}
.right {
	float: right;
	width: 100px;
	height: 100px;
	background-color: blue;
}
~~~

我们希望用box包裹left和right，但此时会出现如下效果：

![未清除浮动的父子元素](http://7xit9q.com1.z0.glb.clouddn.com/howToClearFloats3.png)

这时，有4种解决方法：

* 子元素最后添加一个空节点

~~~ html
<div>
	<div class="box">
		<div class="left">left</div>
		<div class="right">right</div>
		<div style="clear: both"></div> // 添加的空节点
	</div>
</div>
~~~
	
* 父元素添加overflow属性

	可以**为父元素设置overflow为hidden或auto**，但需要注意触发IE的hasLayout。[触发方式](http://stackoverflow.com/questions/1794350/what-is-haslayout)有很多，但我看到网上有人反映：这种方法在IE6/7下还是会出问题。我用Safari的用户代理测了IE7，并未发现有问题。所以，使用这种方法时候还是需要测试一下~


~~~ css
.box {
	overflow: auto;
	_hight: 1%; // 触发IE的hasLayout		
}
~~~

或

~~~ css
.box {
	overflow: hidden;
	_zoom: 1; // 触发IE的hasLayout
}
~~~

或

~~~ css
.box {
	overflow: hidden;
	display: inline-block; // 触发IE的hasLayout
	display: block; 
}
~~~


* 父元素设置:after伪类

~~~ css
.box:after {
	content: '';
	display: table; // 或display: block;
	clear: both;
}
~~~

* 父元素设置:before、:after伪类

~~~ css
.box:before, .box:after {
	content: '';
	display: table;
}
.box:after {
	clear: both;
}
~~~

应用这些解决方案后，父元素都会正常包裹子元素：

![清除浮动后的父子元素](http://7xit9q.com1.z0.glb.clouddn.com/howToClearFloats4.png)

---

##### 参考资料

[CSS clear both 清除浮动](http://www.divcss5.com/rumen/r424.shtml)

[Which method of ‘clearfix’ is best?](http://stackoverflow.com/questions/211383/which-method-of-clearfix-is-best)