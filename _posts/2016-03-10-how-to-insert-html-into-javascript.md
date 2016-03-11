---
layout: post
title: 如何在JavaScript中嵌入HTML代码
category: JavaScript
tags: [html]
summary: 在JavaScript中嵌入HTML代码是一个常用的简单技巧，它的实现方法其实有很多种

---

#### 前言

写实验室项目时，我最常写的代码之一便是通过Ajax接收后台数据后，将其与HTML代码拼接并嵌入页面。开始，我写的代码类似这样：

~~~ javascript
var str = '<li style="padding:5px 5px;"><div><div class="row"><div class="col-xs-5"><img style="height:100%; max-height:70px;width:100%;" src="'+portrait+'" /></div><div class="col-xs-7"><a style="color:black;text-decoration:none;" href="'+info_url+'">'+orgList[i].orgName+'</a><p style="height:50px;margin: 15px 0 0 0;">'+orgList[i].province+'<br/>信用等级：'+orgList[i].creditRating+'</p></div></div></div></li>';					
~~~

后来Review代码时，只觉得

![日了狗了](http://7xit9q.com1.z0.glb.clouddn.com/howToInsertHTMLIntoJS%E6%97%A5%E4%BA%86%E7%8B%97%E4%BA%86.jpg)

除了代码可读性，代码提示也是嵌入HTML时需要考虑的问题。直接在JavaScript中写HTML时，Sublime Text的Emmet插件就几乎不能使用，给实际编码工作带来了极大不便。

于是我主要在[这里](https://www.zhihu.com/question/20240397)发现了在JavaScript代码嵌入HTML的N种方法。现总结如下：

---

#### 常规方法

常规方法主要有四种：

1.	使用"\\"

	利用反斜杠将字符串分隔成多行，效果相当于一行。反斜杠后面必须加换行符。
	

	~~~ javascript
	var str = '\
		-------\
		....\
		-------\';
	~~~

2.	使用"+"

	加号能够连接字符串。


	~~~ javascript
	var str = '-----'+
			  '------'+
			  '...'+
			  '------';
	~~~


3.	String.concat()

	字符串连接函数str.concat(string2, string3[, ..., stringN])。


	~~~ javascript
	var str = ''.concat(
		'------',
		'------',
		...,
		'------'
	);
	~~~


4.	Array.join()

	Array的join()方法将数组的所有元素连接得到一个字符串：str = arr.join([separator = ','])。


	~~~ javascript
	var str = [
	'-----',
	'-----',
	...,
	'-----'
	].join('');
	~~~

Wait！这些方案其实还是直接在JavaScript中写HTML，说好的代码提示呢？实际上，我平时会先在HTML部分写好所需代码，再整体ctrl+v到JavaScript中，利用Sublime的多行编辑功能，统一给HTML代码加上符号……
![我投降](http://7xit9q.com1.z0.glb.clouddn.com/howToInsertHTMLIntoJS%E6%88%91%E6%8A%95%E9%99%8D.jpg)

---

#### 利用注释

这种方法的思路是将待嵌入的HTML代码置于一个函数中，之后将整个函数转化为字符串，截取代码部分。我找到两种实现方法：

* [第一种方式](http://yiding-he.iteye.com/blog/58180)

~~~ javascript
var str = function() {
	/*
		<div>html code</div>
	*/
};
Function.prototype.getMultiLines = function() {
	var lines = new Object(this);
	lines = lines.substring(lines.indexOf('/*')+3, lines.lastIndexOf('*/'));
	return lines;
}
str = str.getMultiLines;
~~~

有人说这种方式在Firefox中会出问题，我自己用Firefox 40测试后并未发现出错。

* [第二种方式](http://javascript.ruanyifeng.com/grammar/string.html)

~~~ javascript
(function () { /*
	line 1
	line 2
	line 3
*/}).toString().split('\n').slice(1,-1).join('\n')
~~~

---

#### HTML独立，使用XHR

这种方法将待嵌入的HTML代码置于单独的文件中，通过同步XHR请求，将代码嵌入JavaScript。

~~~ javascript
var str = Template.load('/template/temp.html'); // Template是一个工具类，负责发送同步XHR请求并返回结果
var target = document.getElementById('element_id');
target.innerHTML = str;
~~~

与这种思想类似的有[seajs文本插件](https://github.com/seajs/seajs-text/issues/1)。

我个人觉得，嵌入的HTML大多都是比较短的代码片段，为此专门建立N个文件，再用XHR请求，有种“杀鸡用牛刀”的感觉嘛~Anyway，
![你们开心就好](http://7xit9q.com1.z0.glb.clouddn.com/howToInsertHTMLIntoJS%E4%BD%A0%E4%BB%AC%E5%BC%80%E5%BF%83%E5%B0%B1%E5%A5%BD.jpg)

---

#### 引用模板

也可以在页面内定义一个模板，需要时引用该模板：

~~~ html
<script type="text/template" id="html_template">
	<div>html code</div>
</script>
<script type="text/javascript">
	var str = document.getElementById('html_template').innerHTML();
</script>
~~~
