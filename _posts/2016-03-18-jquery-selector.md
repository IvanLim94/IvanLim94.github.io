---
layout: post
title:  "jquery选择器总结"
date: 2015-07-23 10:21:49
categories: Jquery
tags: 选择器 jquery 原创
---
## 1. Jquery对象与DOM转换： ##
`$(document.getElementById('div'))`;//jquery对象转dom对象  
`var div1 = $div.get(0);`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //方法1：dom对象转jquery对象<br/>
`var div2=$div[0];`&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;//方法2：dom对象转jquery对象

## 2. 常规选择器: ##
	‘#’		:id选择器		源码getElementById()
	‘.’		:类选择器		源码getElementsByClassName()
	‘xx’		:xx元素选择器		源码getElementsByTagName()
	‘*’		:全选择器

## 3. 层选择器： ##
	通过与参考选择器的关系选择
	‘>’		:子选择（第一代后代）
	‘ ’		:所有后代选择
	‘+’		:相邻兄弟选择
	‘~’		:一般兄弟选择。匹配参考选择器的所有兄弟

## 4. 筛选选择器 ##
###### 筛选选择器用法与css伪元素相似，以‘:’当头，但其中属性筛选选择器例外，以'[ ]'限定 ######

### 4.1 基本筛选: ###
	‘:first’		:匹配第一个元素
	‘:last’		:匹配最后一个
	‘not(selector)’ 	:匹配除指定selector以外的所有
	‘:eq(index)’		:匹配第index个
	‘:gt(index)’		:匹配索引大于index的所有
	‘:lt(index)’		:匹配索引小于index的所有
	‘:even’		:匹配偶数索引
	‘:odd’		:匹配奇数索引
	以下不常用
	‘:header’		:匹配标题元素，如h1--h4
	‘:lang(language)’	:匹配指定语言的所有元素
	‘:root’		:匹配该文档的根元素
	‘:animated’		:选择正在指定动画效果的所有元素

### 4.2 内容筛选： ###
##### 根据子元素或者文本内容来筛选 #####
	‘:contains(text)’	:选择所有包含指定文本的元素
	‘:has(selector)’	:选择所有至少包含指定selector的元素
	‘:parent’		:选择所有含有子元素或者文本的元素
	‘:empty’		:选择所有不含子元素或者文本的元素

### 4.3可见性筛选： ###
	‘:visible’		:选择所有显示元素
	‘:hidden’		:选择所有隐藏元素

**ps:** 若元素占据文档一定空间，则被认为是可见的。
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**css属性**中的visibility：hidden或opacity: 0的元素都被认为是可见的，因为他们占据空间布局。

### 4.4 属性筛选： ###
###### 基于属性名和值筛选 ######
	‘[attr]’		:选择具有指定属性的元素，不限制值
	‘[attr='value']’	:选择指定属性值等于value的元素。
	‘[attr*='value']’	:选择指定属性具有包含value的元素
	以下不常用
	‘[attr|='value']’	:选择指定属性值等于value或以value为前缀（value-xxxx）的元素。
	‘[attr~='value']’	:选择指定属性值用空格分隔的值中包含value的元素
	‘[attr!='value']’	:选择不存在的指定属性或者指定的属性值不等于value的元素
	‘[attr^='value']’	:选择指定属性是以value开始的元素
	‘[attr$='value']’	:选择指定属性是以value结尾的元素，区分大小写

### 4.5 子元素筛选：(不常用) ###
###### 根据参考元素和他父元素的关系来筛选 ######
	‘:first-child’		:选择所有作为其父元素的第一个子元素的元素
	‘:last-child’			:选择所有作为其父元素的最后一个子元素的元素
	‘:only-child’			:选择所有作为其父元素的唯一子元素的元素
	‘:nth-child(index)’		:选择所有作为其父元素的第index个子元素的元素
	‘:nth-last-child(index)’	:选择所有作为其父元素的倒数第index个子元素的元素

如以下html结构:
    
	<div>
		<div>
			<a>1</a>
		</div>
		<div>
			<a>2</a>
			<a>3</a>
			<a>4</a>
		</div>
		<div>
			<a>5</a>
			<a>6</a>
		</div>
	</div>

jquery代码:
    
	$(div a:first-child)		会选中1,2,5。等同于$(div a:nth-child(0));
	$(div a:only-child)		会选中1
	$(div a:nth-child(1))		会选中3,6
	$(div a:nth-last-child(0))	会选中1,4,6。等同于$(div a:last-child);

### 4.6 表单元素选择器 ###
	‘:input’		匹配所有input，textarea，select和button元素
	‘:text’		匹配所有文本框
	‘:password'’		匹配所有密码框
	‘:radio’		匹配所有单选框
	‘:checkbox’		匹配所有复选框
	‘:submit’		匹配所有提交按钮
	‘:image’		匹配所有图像域
	‘:reset’		匹配所有重置按钮
	‘:button’		匹配所有按钮
	‘:file’		匹配所有文件域

##### `大部分表单类型筛选器都可以类似于$('input:password') == $('input[type=password]')来替换` #####

### 4.7 表单对象属性筛选选择器 ###
	‘:enabled’		匹配可用的表单元素
	‘:disabled’		匹配不可用的表单元素
	‘:checked’		匹配被选中的input元素
	‘:selected’		匹配被选中的option元素，下拉框适用

## 总结 ##
这些选择器表达式都应该放在' $() '中的'( )'里面，匹配根据**元素名，元素与其父或其子的关系，元素的属性，元素的位置，元素的子内容等**，结果返回为Jquery对象。