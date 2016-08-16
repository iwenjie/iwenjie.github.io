---
title: dcf doc
date: 2016-08-16 16:22:48
categories: 
  - 文档
tags: 
  - 文档
---

dcf doc
<!--more-->
### dcf相关资源目录结构

```bash
└─ webapp                                   # 前端资源文件夹
  ├─ views
  │  ├─ dcf 
  │  │  └─ index                      
  │  │     └─ index.jsp                     # 装饰器配置
  └─ WEB-INF
     ├─ layouts                             # 布局用到的一些公用模板  
     │  ├─ includes                         # 基础组件js
     │  │  ├─ dcfHeader.html                # 头部
     │  │  ├─ dcfLeftBar.html               # 侧边栏
     │  │  ├─ headerInvite.jsp              # 
     │  │  └─ footerSearch.jsp              #                        
     │  ├─ dcf-new.jsp                      # 新版首页装饰器
     │  ├─ dcf.jsp                          # 
     │  └─ dcfIndex.jsp                     # 
     └─ decorators.xml                      # 装饰器配置
```

### header 头部

> 资源: `layouts/includes/dcfLeftBar.html`

### slideBar 侧边栏

> 资源: `layouts/includes/dcfLeftBar.html`

提供功能：
- 菜单
- 动态

提供方法：

```bash
slideBar.init()       # 渲染入口
slideBar.init()
```

### footer
