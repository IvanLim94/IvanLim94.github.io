---
layout: post
title:  "jQuery操纵DOM常用方法"
date: 2016-04-15 08:34:09
categories: jQuery
tags: 操纵DOM jQuery 原创
---
## 1 操作'$()'合集 ##

	$('xx').each(function(index,ele))	遍历合集对象，调用回调方法

每读取一次，便调用一次回调方法。<br>
*ps：回调函数内的ele==this*

	$('xx').add(html结构/ele)			向合集对象添加新元素	
## 2 插入DOM ##
#### 子元素插入： ####

	$('xx').append(element)	元素里面插个小儿子
	$('xx').prepend(element)	元素里面插个大儿子
#### 兄弟元素插入： ####

	$('xx').after(element)		紧挨着元素后面跟个兄弟
	$('xx').before(element)	紧挨着元素前面顶个大哥

## 3 删除DOM ##
	$('xx').empty()			清空结点,保留自身
	$('xx').detach()			保留数据与事件的临时删除，“我会回来的！”
	$('xx').remove()			删除节点。
	以下支持传表达式参数：
	$('xx').remove(express)
	$('xx').detach(express)	根据表达式筛选过滤后删除
eg：

	$('xx').remove(':contains("3")')			筛选子文本后删除结点
	等同于：
	$('xx').filter(':contains("3")').remove()

**ps:**三者之间的区别：<br/>

1. .empty( )丢盔弃甲，孤身一人，.remove( )战败，自刎。<br/>
2. .remove( )和detach( )可以传一个表达式，.empty( )不能。
3. .detach( )后依然存于内存中，append( )会回到DOM tree中，同时数据和事件依然存在，满战斗力复活。

## 4 复制和替换 ##

	$('xx').clone([boolean])		复制。true时事件与数据一并克隆
	$('xx').replaceWith(element)	替换目标集合每个元素

## 5 包裹，加减个爸爸 ##
加个爸爸：

	$('xx').wrap('html结构/ele/$')			操作单个元素，给一个人加个爸爸
	$('xx').wrapAll('html结构/ele/$')			操作多个元素，给一群人加个爸爸
	ps:都可传function(){return 'html结构'}每遇到匹配元素，执行函数。
	

减个爸爸：

	$('xx').unwrap()			只能无参

eg：

	1 如下html结构：
	<p>爸爸去哪了</p>

	2 经过jQuery代码：$('p').wrap('<div></div>')后

	3 变为如下html结构:
	<div>
		<p>爸爸去哪了</p>
	</div>

转让儿子，我当爷爷：

	$('xx').wrapInner('html结构/ele/$')
	ps：可传回调函数。function(){return 'html结构'}

eg:

	1 如下html结构：
	<div>测试</div>
	<div>测试</div>

	2 经过jQuery代码：$('div').wrapInner('<p></p>')后

	3 变为以下html结构：
	<div>
		<p>p测试</p>
	</div>
	<div>
		<p>测试</p>
	</div>

此时“测试”文本结点的父元素变为**p元素**，div元素成功晋级为“测试”文本结点的爷爷辈。

## 6 找亲戚（遍历） ##
**注意：** $('xx')是合集对象，便于理解。<br>

找后代：

	$('xx').children()			只找儿子,可传express过滤条件
	$('xx').find(express)		找符合条件的所有后代

找祖宗：

	$('xx').parent()				只找爸爸，可传express
	$('xx').closets(express)		找祖宗，找到一个匹配便停止

找兄弟：

	$('xx').next()			找紧挨着的后面的兄弟,可传express
	$('xx').prev()			找紧挨着的前面的兄弟,可传express
	$('xx').siblings()		找所有兄弟，可传express