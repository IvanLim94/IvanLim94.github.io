---
layout: post
title:  "jquery属性与样式总结"
date: 2015-07-23 10:21:49
categories: jQuery
tags: 属性与样式 jQuery 原创
---

## 1 .atrr( ) ##
	1个参数：	'attr'					获取该属性值
			{'attr1':'val1','attr2':'val2',..}	传入对象设置属性值
	2个参数：	'attr','val'	设置属性值
			'attr',func	设置属性的函数值

func回调函数接收元素的**索引位置和该元素attr值。**<br/>
	
	eg：
	$('xx').attr('id',function(index,val){<br>
		console.log('当前正在处理第'+ i +'个元素');<br>
		console.log('该被处理元素的attr值为：'+ val );<br>
	})<br>

removeAttr('attr')	:移除一个属性。

## 2 .html( )和.text( ) ##
#### .html( )方法： ####
	0个参数：	.html()			获取第一个匹配元素HTML内容
	1个参数：	.html('str')		设置每一个匹配元素HTML内容
			.html(fuc)		func用来返回设置HTML内容的函数

func回调函数接收 **元素的数组索引和该元素内的html值**。<br/>

#### .text( )方法 ####
和.html( )类似，传参一致。<br>
**区别:**<br>
	1 .html( )方法处理的是**元素内容，包括标签**。而.text()方法处理的仅是文本内容，不包含标签。<br>
	2 .html( )方法在使用在多个元素上时，只能读取第一个元素而text( )会读取所有元素，组成合集输出。

##### .val( )用于处理表单元素的value。 #####

## 3 样式增减和切换 ##
样式增加：<br>

	.addClass(str);
	.addClass(function(index,currentClass));	返回一个或多个要增加的样式名

样式删除：

	.removeClass(str);
	.removeClass(function(index,currentClass));	返回一个或多个要删除的样式名


**注意：** 函数作为参数，返回多个class时，用空格隔开。<br>

样式切换：

	.toggleClass(className);		若有该类，则删除；若无则添加。实现切换

## 4 .css( ) ##
	1个参数	'property'				获取该css样式的值
		{'pro1':'val1','pro2':'val2',...}	批量设置css样式值
	2个参数	'property','val'			设置css样式值
		'property',function(index,val)


func回调函数接收 **元素的数组索引和该元素的css样式值**<br/>

**ps：** .css( )方法设置的样式要**优先**于.addClass( )方法设置的样式。

## 5 临时数据存储 ##
静态接口：<br>

	jQuery.data(element,key,value);		存数据
	jQuery.data(element,key);		取数据
	jQuery.removeData(element [,name]);	删除数据

##### ps：element是DOM对象<br> #####

实例接口：

	$('xx').data(key,value);		存数据
	$('xx').data(key);			取数据
	$('xx').removeData([name]);		删除数据