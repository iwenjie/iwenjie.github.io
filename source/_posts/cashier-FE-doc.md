---
title: 收银台前端设计文档
date: 2016-08-01 16:22:48
categories: 
  - 文档
tags: 
  - 文档
---

收银台系统目前是独立于1000应用（但是仍然发布在home.iqunxing.com下）的为群星业务提供支付功能的系统。
<!--more-->

### 目录结构

```bash
└─iqunxing-cashier
  ├─doc                                
  └─iqunxing-cashier-webapp
    └─src                         
      └─main 
        ├─java               
        ├─resources               
        ├─scripts              
		└─webapp     
```

```bash
└─ webapp
  ├─ cashier 
  │  ├─ css  
  │  │  ├─ base                             # 底层CSS
  │  │  ├─ fonts                            # 字体文件
  │  │  └─ page                             # 页面层CSS
  │  ├─ images  
  │  │  ├─ cashier  
  │  │  ├─ icon                             #
  │  │  ├─ loading                          #
  │  │  ├─ logo                             #
  │  │  ├─ modal                            # 弹窗里的相关图片资源
  │  │  └─ payment                          #
  │  ├─ js                                  #
  │  │  ├─ base
  │  │  │  ├─ bootstrap.min.js              #
  │  │  │  ├─ jquery-1.11.2.min.js          #
  │  │  │  ├─ jquery-validate.js            # 表单验证插件
  │  │  │  └─ util.js                       # 封装的一些工具函数
  │  │  └─ page 
  │  │     ├─ cashier.js                    # 收银台主业务流程js
  │  │     ├─ getBankList.js                # 收银台主页一些服务js
  │  │     └─ instant-pay.js                # 快捷支付相关js
  │  ├─ cashier-modal.html                  # 收银台弹框相关内容静态资源
  │  ├─ error.html                
  │  ├─ redirect.html                       #
  │  ├─ test.html                           # 本地测试收银台页面
  │  └─ wait.html                           #
  └─ WEB-INF
     └─ jsp                         
        ├─ cashier.jso             
        ├─ instant-pay.jsp             
        ├─ result.jsp               
	    └─ transfering.jsp 

```


### 代码结构

##### getBankList 所提供的服务
1，渲染历史银行服务

```javascript
renderPersonUsedBanks = {
	data:'',
	init:'',
	formatBankInfo:'',
	formatBankType:'',
	getLimitDetail:'',
	setLimitDetail:'',
	renderBankList:'',
	createPersonUsedBanks:'',
	availIdenBank:'',
	availPersonBank:'',
	availCompanyBank:'',
	initIdenUsedBank:'',
	initCompanyUsedBank:'',
	initPersonUsedBank:''
}
```