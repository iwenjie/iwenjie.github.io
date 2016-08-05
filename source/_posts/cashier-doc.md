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
└─ webapp                                   # 前端资源文件夹
  ├─ cashier                                # 静态资源文件夹
  │  ├─ css                                 # css文件夹
  │  │  ├─ base                             # 底层CSS
  │  │  ├─ fonts                            # 字体文件
  │  │  └─ page                             # 页面层CSS
  │  ├─ images  
  │  │  ├─ cashier                          # 主页面
  │  │  ├─ icon                             # icon
  │  │  ├─ loading                          # loading
  │  │  ├─ logo                             # logo
  │  │  ├─ modal                            # 弹窗里的相关图片资源
  │  │  └─ payment                          # 第三方支付调用的
  │  ├─ js                                  # js文件夹
  │  │  ├─ base                             # 基础组件js
  │  │  │  ├─ bootstrap.min.js              # bootstrap
  │  │  │  ├─ jquery-1.11.2.min.js          # jquery
  │  │  │  ├─ jquery-validate.js            # 表单验证插件
  │  │  │  └─ util.js                       # 封装的一些工具函数
  │  │  └─ page 
  │  │     ├─ cashier.js                    # 收银台主业务流程js
  │  │     ├─ getBankList.js                # 收银台主页一些服务js
  │  │     └─ instant-pay.js                # 快捷支付相关js
  │  ├─ cashier-modal.html                  # 收银台弹框相关内容静态资源
  │  ├─ error.html                
  │  ├─ gulpfile.js                         # gulp配置文件
  │  ├─ package.json                        # 依赖资源管理文件
  │  ├─ redirect.html                       # 
  │  ├─ test.html                           # 本地测试收银台页面
  │  └─ wait.html                           #
  └─ WEB-INF
     └─ jsp                         
        ├─ cashier.jso                      # 收银台主页面
        ├─ instant-pay.jsp                  # 快捷支付页面
        ├─ result.jsp                       # 支付结果页面
        └─ transfering.jsp                  # 转账中页面
```
### 代码运行环境

收银台应用ID: 1035
本地调试启动文件: `test/java/Startup.java`

*gulp使用介绍：*
目前gulp只使用加版本号功能，进入webapp/cashier文件夹 执行`gulp`
*warning*  如果有修改到`/cashier/cashier-modal.html` 避免页面缓存务必要加上版本号
```javascript
$('.modalList').load('/cashier/cashier-modal.html?v=2016080501');
```

### 百度分析

百度分析账号：薄荷少年半心凉丶
密码：***********
统计内容：

### 代码结构

##### Util 所提供的工具函数
```javascript
isNumber();
isEmpty();
isArray();
isObject();
formatTime(time,dateType);
formatMoney();
formatMoneyToNum();
getRequestParams();
applyTpl();
alert();
_million();
getCookie();
showLoding();
closeLoding();
maskInit();               // 遮罩
resetInit();              // 重置一些check、radio的默认样式
```

##### getBankList 所提供的服务
1，渲染历史银行服务

```javascript
renderPersonUsedBanks = {
	data:'',  // 数据缓存
	init:'',  // 入口
	formatBankInfo:'',  // 处理银行信息
	formatBankType:'',  // 处理银行类型
	getLimitDetail:'',  // 获取额度信息
	setLimitDetail:'',  // 设置额度信息
	renderBankList:'',  // 渲染列表
	createPersonUsedBanks:'',  // V2版本暂时不调用
	availIdenBank:'',  // V2版本暂时不调用
	availPersonBank:'',  // V2版本暂时不调用
	availCompanyBank:'',  // V2版本暂时不调用
	initIdenUsedBank:'',  // V2版本暂时不调用
	initCompanyUsedBank:'',  // V2版本暂时不调用
	initPersonUsedBank:''  // V2版本暂时不调用
}
```

### 前端页面渲染流程

加载模态框相关静态资源(cashier-modal.html),回调绑定事件
渲染群星账户列表，群星账户的数据从页面${options}上获取，设置默认支付方式
获取第三方支付相关银行列表，获取到之后依次渲染网银列表、快捷支付列表、历史银行选择器

### 前端页面交互流程

进入页面默认选择一种支付方式(优先级：群星账户>第三方支付账户第一个)，
切换支付方式，同时切换支付参数(支付参数说明见代码中_PAY_PARAM)，
如果没有符合支付条件的群星账户和历史支付账户则显示选择银行的列表

### 前端支付流程

群星支付 > gotoPay

第三方支付 > 获取支付渠道(payment_channel) > gotoPay

gotoPay 
        > 失败
        > 成功
        > 处理中
        > 支付中 > getPayResult > gotoBank
        > 异常处理

getPayResult 
             > 成功
             > 转账中 > getPayResult
             > 失败
             > 异常处理 > getPayResult

### cashier-modal.html提供的模态框服务说明

```bash
#modal_paymentToAccountTip  # 还款到账时间提醒模态框
#modal_payWait              # 支付等待中模态框
#modal_paySuccess           # 支付成功模态框
#modal_payFail              # 支付失败模态框
#modal_paying               # 支付中模态框
#modal_deleteCard           # 删除银行卡提示模态框
```