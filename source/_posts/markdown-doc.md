---
title: markdown使用手册
date: 2016-06-01 16:22:48
categories: 
  - 文档
  - 工具
tags: 
  - 文档
  - 工具
---

Markdown是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式。
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
列表: * 添加星号或 - 成为一个新的列表项。
引用: > 引用内容
内嵌代码: `alert('Hello World');`
画水平线(HR): --------
```
##### 示例:
[链接百度](http://www.baidu.com) **加粗的文字** *斜体的文字* ~~带删除线的文字~~

* *号列表1
* *号列表2
- -号列表3
- -号列表4
  * 二级*号列表1
  - 二级*号列表2
  * 二级-号列表3
  - 二级-号列表4

> 这是引用内容

`alert('Hello World 内嵌代码');`

下面画水平线(HR)

--------

### 图片和代码相关:

使用代码`![Image](https://octodex.github.com/images/yaktocat.png)`

eg:
![Image](https://octodex.github.com/images/yaktocat.png)

普通代码：
```
	` ` `
		you code(使用时去除空格)
	` ` `

```

eg:
```
if (isAwesome){
  return true
}
```

指定语言类型：
```
	` ` `javascript
		you code(使用时去除空格)
	` ` `

```

eg:
```javascript
if (isAwesome){
  return true
}
```
##### emoji表情:

`:smile:` `:heart_eyes:` `:flushed:` `:stuck_out_tongue_winking_eye:` `:stuck_out_tongue_winking_eye:`

eg：
:smile: :heart_eyes: :flushed: :stuck_out_tongue_winking_eye: :stuck_out_tongue_winking_eye:
注：有些markdown解析引擎不支持
 [查看更多emoji表情](http://www.emoji-cheat-sheet.com/) 
