---
title: 编程技巧
date: 2017年1月5日14:54:20
categories: 
  - 文档
  - 工具
tags: 
  - 文档
  - 工具
---

暂时没有介绍
<!--more-->


```
var a = a;//不确定a之前是否定义过  a||undefined
(function(a){
	a = 2;
	console.warn(a);
)(a)
console.info(a);
//等价于定义函数 传参
```

```
(function(a){
	a = 2;
	console.warn(a);
)(a)
console.info(a);

```