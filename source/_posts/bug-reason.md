---
title: 前端bug产生的一些原因
date: 2016-07-19 16:22:48
categories: 
  - 总结
tags: 
  - 总结
---

前端bug产生的一些原因总结
<!--more-->

#### 后端接口数据异常导致前端取值异常 
eg: 接口规定 res.result.list 为空时返回 res.result.list = []; 然而并没有返回 res.result ,导致浏览器报错误TypeError:res.result id undefined