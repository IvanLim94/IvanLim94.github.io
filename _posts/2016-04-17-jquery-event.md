---
layout: post
title:  "jQuery常用事件总结"
date: 2016-04-17 09:24:39
categories: jQuery
tags: 事件 jQuery 原创
---

## 1 鼠标事件 ##

	.click()			鼠标点击，不用说了，最基础的
	.dbclick()						双击
	.mousemove()					移动
	.mouseenter()					移入
	.mouseleave()					移出
	.mousehover(func1(){},func2(){})	移入移出
	以下不常用
	.mouseover()		移入，具有冒泡效应
	.mouseout()			移出，具有冒泡效应
	.mousedown()		鼠标按键按下
	.mouseup()			鼠标按键松开

*ps: .mousehover( )方法两个参数都是函数，分别是处理进入和离开的回调函数。*<br>
**除mousehover外的方法，参数都有以下几种：**

1. 无参：指定触发该事件
2. 有参数：[eventData]，function(event){ }
<br>其中eventData是数据参数，用于处理**不同作用域**数据传递问题。event.data获取该数据。
<br>*ps：event指的是该事件。*

### 事件间的冒泡 ###

> “冒泡”是一种排序算法，这个算法的名字由来是因为越大的元素会经由交换慢慢“浮”到数列的顶端，故名。

	例如以下html结构：
	<div style='width=100%;height=100%'>
		<p>绑定mouseout事件</p>
	</div>

**冒泡现象：**
假如div和p都绑定了mouseout事件，当鼠标移出p元素，触发p元素的mouseout事件，但并没有移出div元素区域，依然会触发div元素的mouseout事件。<br>
“冒泡”形义为水泡越往上浮体积越大，将他移植到事件间的触发上很容易理解。<br>
**阻止冒泡：**event.stopPropagation()阻止事件冒泡

## 2 表单事件 ##

	.focusin()			得到光标焦点时
	.focusout()			失去光标焦点时
	.change()			value值改变则触发
	.select()			input元素与textarea元素内容被选中则触发
	.submit()			表单提交时触发

其中:

	.submit(function(){
		...
		return false;	阻止表单提交
	})

return false等效于**同时调用**e.preventDefault( )和e.stopPropagation( )
> 
e.preventDefault( )阻止默认行为。如：`<a>`的默认行为是跳转，`<form>的默认行为是提交`。<br>
return false 除了阻止默认行为之外，还会阻止事件冒泡。如果手上有一份jquery源代码的话，可查看其中有如下代码：


	if (ret===false){
		event.preventDefault();
		event.stopPropagation();
	}

## 3 键盘事件 ##

	.keydown()		键盘按下触发
	.keyup()		键盘松开触发

可用event.target.value监听用户的按键

## 4 ‘on’绑定事件 ##

> 函数结构：<br>
> on( events ,[ selector ] ,[ data ], handler(eventObject) )

常规方式：

	$ele.on('click',function( ){ })

多事件绑定同一函数：*多事件名之间空格分隔*

	$ele.on('mouseenter mouseleave',function( ){ })

多事件绑定不同函数：*只有一个对象参数*

	$(ele).on({
		mouseenter:function( ){},
		mouseleave:function( ){},
	})

传递数据：*第二个参数为对象数据*

	$ele.on('click',{name:'ivan'},function(event){
		alert(event.data.name);
	})

#### 委托机制 ####
on第二个参数提供了一个selector选择器。

	如下html结构：
	<div>
		<p>
			<a>目标节点</a>
		</p>
	</div>

	jQuery代码：
	$('div').on('click','p',fn)

虽然绑定的是div元素，但通过第二个selector参数将事件委托到了p元素上。