---
title: JS&jQuery相关语法
date: 2019-09-19 15:52:25
tags:
 - web
 - js
 - javascript
 - jquery
 - ECMAScript
categories: tech
photos: https://img-blog.csdnimg.cn/img_convert/7284b29608d31fe6e8b71c8016815518.png
---
# jquery的基础语法：

```html
$(selector).action()
```

## 选择器
### 基本选择器

```html
$("*")
$("#id")
$(".class")
$("element")
$(".class,p,div")
```

## 层级选择器

```html
$(".outer div")
$(".outer&gt;div")
$(".outer+div")
$(".outer~div")
```

## 基本筛选器

```html
$("li:first")
$("li:eq(2)")
$("li:even")
$("li:gt(1)")
```

## 属性选择器
```html
$('[id="div1"]')
$('["alex="sb"][id]')
```

## 表单选择器
```html
$("[type='text']")-----&gt;$(":text")
```
**注意只适用于input标签:$("input:checked")**

