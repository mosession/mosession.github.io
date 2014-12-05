---
layout: post
title: 'overflow及其如何清除浮动'
category: 文档
tags: CSS 
---

# CSS overflow 及其如何去除浮动


---
问：  
今天突然发现overflow:hidden这个能清除浮动，想知道overflow:hidden到底这个属性做了哪些动作，竟然能够清除浮动，解析的时候到底是怎样解析的... 


答：  
是因为overflow（除了visible)会重新给他里面的元素建立块级格式化(block formatting context)
floats, position absolute, inline-block, table-cell和table-caption都不是块级样式，所以才会用到clear来控制浮动
overflow也可以清除浮动是因为当在父级元素设置overflow时候，除了visible，就是只有auto, hidden或者scroll时候，也会建立新的块级格式给他的子元素, 从而起到清楚浮动效果
虽然clear是旧的方式，但还是推荐用clear来做，有些情况会比overflow处理的要好
#CSS overflow 属性
__实例__
设置 overflow 属性：  

```HTML
div
  {
  width:150px;
  height:150px;
  overflow:scroll;
  }
```  

__浏览器支持__
所有主流浏览器都支持 overflow 属性。
注释：任何的版本的 Internet Explorer （包括 IE8）都不支持属性值 "inherit"。
__定义和用法__
overflow 属性规定当内容溢出元素框时发生的事情。
__说明__
这个属性定义溢出元素内容区的内容会如何处理。如果值为 scroll，不论是否需要，用户代理都会提供一种滚动机制。因此，有可能即使元素框中可以放下所有内容也会出现滚动条。 
![pic](http://ww1.sinaimg.cn/large/6ff04438gw1eiuvi3ccuvj20jv038dfz.jpg)  
__可能的值__
![pic](http://ww4.sinaimg.cn/large/6ff04438gw1eiuviwzkbfj20jo04faaq.jpg)  
#CSS: 清除浮动－使用:Overflow
**什么是CSS清除浮动？**
网络上流行的说法是：在非IE浏览器（如Firefox）下，当容器的高度（height）为auto，且容器的内容中有浮动（float为left或right）的元素，在这种情况下，容器的高度不能自动伸长以适应内容的高度，使得内容溢出到容器外面而影响（甚至破坏）布局的现象。这个现象叫浮动溢出，为了防止这个现象的出现而进行的CSS处理，就叫CSS清除浮动。  

下面的演示中显示的浮动子元素在父容器高度不自动适应的问题 。为了解决这个问题，您可以简单地添加CSS属性overflow:auto (or overflow:hidden)的包装容器。这也许是最简单的方法来清除浮动。
![pic](http://ww3.sinaimg.cn/large/6ff04438gw1eiuvr0irh6j20se0j5799.jpg)
第一段
HTML             

```HTML
<div class="container-without-overflow">
	<div class="box">
		<p>Curabitur venenatis vehicula mattis. Nunc eleifend consectetur odio sit amet viverra. Ut euismod ligula eu tellus interdum mattis ac eu nulla. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui.</p>
	</div>
	<div class="box">
		<p>Nunc eleifend consectetur odio sit amet viverra. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui. Ut euismod ligula eu tellus interdum mattis ac eu nulla.</p>
	</div>
</div>
```

CSS  

```CSS  
.box {
	background: #cbd4d9;
	width: 400px;
	margin-right: 10px;
	padding: 10px 20px;
	float: left;
}
.container-without-overflow {
	background: #e6eef2;
	border: solid 1px #999;
	padding: 10px;
}
```  

![pic](http://ww2.sinaimg.cn/large/6ff04438gw1eiuwdpx6ooj20rl04eq44.jpg)  
当把.box的float:left去掉之后就是这样了  
![pic](http://ww3.sinaimg.cn/large/6ff04438gw1eiuwejjo3pj20rm0883zr.jpg)  
说明的确是float的问题
**第二段**
HTML  

```HTML
<div class="container-without-overflow">
	<div class="box">
		<p>Curabitur venenatis vehicula mattis. Nunc eleifend consectetur odio sit amet viverra. Ut euismod ligula eu tellus interdum mattis ac eu nulla. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui.</p>
	</div>
	<div class="box">
		<p>Nunc eleifend consectetur odio sit amet viverra. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui. Ut euismod ligula eu tellus interdum mattis ac eu nulla.</p>
	</div>
	<div style="clear:both">&lt;div style="clear:both"&gt;&lt;/div&gt;</div>
</div>
```    

CSS同上
这里额外加了个div用于清除浮动  
如果父div是float：left，而子div没有float就会产生父div没有高度问题，子div无法撑开父div，加入清除浮动，子div就可以撑开父div
具体放的位置就是 父div的结束前  

```HTML
<div id="父div">
<div id="子div">
内容
</div>
<div class="clearfloat"></div>
</div>
```  

**第三段** 
HTML  

```HTML
<div class="container">
	<div class="box">
		<p>Curabitur venenatis vehicula mattis. Nunc eleifend consectetur odio sit amet viverra. Ut euismod ligula eu tellus interdum mattis ac eu nulla. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui.</p>
	</div>
	<div class="box">
		<p>Nunc eleifend consectetur odio sit amet viverra. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui. Ut euismod ligula eu tellus interdum mattis ac eu nulla.</p>
	</div>
</div>
```  

CSS  

```CSS
.container {
	background: #e6eef2;
	border: solid 1px #999;
	padding: 10px;
	overflow: auto;
}
.box {
	background: #cbd4d9;
	width: 400px;
	margin-right: 10px;
	padding: 10px 20px;
	float: left;
}
```  

**缺点**
虽然它是一个很好的的技巧，也有一些弊端：  

* 使用 overflow:auto，会造成一个滚动条，如果您的内容是延长了容器的边界。例如，如果你有一个长unbreaking的文本（即长的URL文本）或一个较大的图像，是更大的，则容器滚动显示。  
* 为了避免一个滚动显示你应该使用overflow:hidden。然而，这种方法也有一个缺点。使用overflow:hidden隐藏任何超出容器的边界的内容。 

HTML  

```HTML
<div class="container">
	<div class="box">
		<p>Curabitur venenatis vehicula mattis. Nunc eleifend consectetur odio sit amet viverra. Ut euismod ligula eu tellus interdum mattis ac eu nulla. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui.</p>
	</div>
	<div class="box">
		<p>Nunc eleifend consectetur odio sit amet viverra. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui. Ut euismod ligula eu tellus interdum mattis ac eu nulla. <img src="http://www.bzjg.com.cn/img/bannerpic/thr.jpg" alt="image"></p>
		<p>http://www.webdesignerwall.com/sample/tutorials/css_clearing_floats_with_overflow</p>
	</div>
</div>
```  

CSS  
```CSS
.container {
	background: #e6eef2;
	border: solid 1px #999;
	padding: 10px;
	overflow: auto;
}
.box {
	background: #cbd4d9;
	width: 400px;
	margin-right: 10px;
	padding: 10px 20px;
	float: left;
}
```
![pic](http://ww3.sinaimg.cn/large/6ff04438gw1eiuxo0xk1zj20sk0f8dio.jpg)  

**Word-wrap**
为了解决大文本问题，只需添加 word-wrap:break-word 到容器，这将迫使文本换行到一个新的行。
CSS

```CSS
.container {
    word-wrap: break-word;
}
```

**Max-width**
为了防止图像扩大超出容器边界，添加的max-width:100%，它会调整图像的大小符合容器的最大宽度。  

```CSS
.container img {
    max-width: 100%;
    height: auto;
}
```
HTML  

```HTML  
<div class="container fixed">
	<div class="box">
		<p>Curabitur venenatis vehicula mattis. Nunc eleifend consectetur odio sit amet viverra. Ut euismod ligula eu tellus interdum mattis ac eu nulla. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui.</p>
	</div>
	<div class="box">
		<p>Nunc eleifend consectetur odio sit amet viverra. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui. Ut euismod ligula eu tellus interdum mattis ac eu nulla. <img src="http://www.bzjg.com.cn/img/bannerpic/thr.jpg" alt="image"></p>
		<p>http://www.webdesignerwall.com/sample/tutorials/css_clearing_floats_with_overflow</p>
	</div>
</div>
```

CSS  

```CSS
.container {
	background: #e6eef2;
	border: solid 1px #999;
	padding: 10px;
	overflow: auto;
}
.box {
	background: #cbd4d9;
	width: 400px;
	margin-right: 10px;
	padding: 10px 20px;
	float: left;
}

.container.fixed {
	word-wrap: break-word;
}
.container.fixed img {
	max-width: 100%;
	height: auto;
}
```
![pic](http://ww1.sinaimg.cn/large/6ff04438gw1eiuxr6dhutj20r809p76j.jpg)

完整HTML

```HTML
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">

<title>CSS: Clear Float Drawbacks</title>

<style type="text/css">
body {
	font: .9em/150% Arial, Helvetica, sans-serif;
	margin: 30px auto;
	width: 960px;
}
p {
	margin: 0 0 1em;
}
h2 {
	font: bold 22px/110% Arial, Helvetica, sans-serif;
	margin: 20px 0 0;
	padding: 20px 0;
	clear: both;
}
h3 {
	font: bold 16px/120% Arial, Helvetica, sans-serif;
	margin: 0 0 5px;
}
.credits {	
	border-bottom: solid 2px #000;
	padding-bottom: 10px;
}

/* with overflow */
.container {
	background: #e6eef2;
	border: solid 1px #999;
	padding: 10px;
	overflow: auto;
}
.box {
	background: #cbd4d9;
	width: 400px;
	margin-right: 10px;
	padding: 10px 20px;
	float: left;
}

/* fixed scrollbar */
.container.fixed {
	word-wrap: break-word;
}
.container.fixed img {
	max-width: 100%;
	height: auto;
}

</style>
</head>

<body>
<h2>Drawbacks: scrollbar</h2>
<div class="container">
	<div class="box">
		<p>Curabitur venenatis vehicula mattis. Nunc eleifend consectetur odio sit amet viverra. Ut euismod ligula eu tellus interdum mattis ac eu nulla. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui.</p>
	</div>
	<div class="box">
		<p>Nunc eleifend consectetur odio sit amet viverra. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui. Ut euismod ligula eu tellus interdum mattis ac eu nulla. <img src="http://www.bzjg.com.cn/img/bannerpic/thr.jpg" alt="image"></p>
		<p>http://www.webdesignerwall.com/sample/tutorials/css_clearing_floats_with_overflow</p>
	</div>
</div>

<h2>Solution: add max-width:100% to img and word-wrap:break-word to container</h2>
<div class="container fixed">
	<div class="box">
		<p>Curabitur venenatis vehicula mattis. Nunc eleifend consectetur odio sit amet viverra. Ut euismod ligula eu tellus interdum mattis ac eu nulla. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui.</p>
	</div>
	<div class="box">
		<p>Nunc eleifend consectetur odio sit amet viverra. Phasellus cursus, lacus quis convallis aliquet, dolor urna ullamcorper mi, eget dapibus velit est vitae nisi. Aliquam erat nulla, sodales at imperdiet vitae, convallis vel dui. Ut euismod ligula eu tellus interdum mattis ac eu nulla. <img src="http://www.bzjg.com.cn/img/bannerpic/thr.jpg" alt="image"></p>
		<p>http://www.webdesignerwall.com/sample/tutorials/css_clearing_floats_with_overflow</p>
	</div>
</div>


</body></html>

```
