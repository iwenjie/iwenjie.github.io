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

## 一些常用markdown命令 

### 文本相关:

H1 - H6 标题

```
H1: # 标题示例 1
H2: ## 标题示例 2
H3: ### 标题示例 3
H4: #### 标题示例 4
H5: ##### 标题示例 5
H6: ###### 标题示例 6
```

### 文本样式相关:
```
链接: [Title](URL)
加粗: **Bold**
斜体字: *Italics*
删除线: ~~text~~
列表: * 添加星号成为一个新的列表项。
引用: > 引用内容
内嵌代码: `alert('Hello World');`
画水平线(HR): --------
```
##### 示例:
[链接百度](http://www.baidu.com) **加粗的文字** *斜体的文字* ~~带删除线的文字~~

* 列表1
* 列表2
* 列表3

> 这是引用内容

`alert('Hello World 内嵌代码');`

下面画水平线(HR)

--------

- 后端接口数据异常导致前端取值异常，eg: 接口规定 res.result.list 为空时返回 res.result.list = []; 然而并没有返回 res.result ,导致浏览器报错误TypeError:res.result id undefined