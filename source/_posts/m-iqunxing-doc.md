layout: '[;ayout]'
title: '群星移动端文档 -- fanpaa'
date: 2016-07-07 18:26:33
tags: 
  - 文档 
  - 群星
---

[1004] 群星h5站点

这个项目包含所有跟mobile browser,weixin,iOS,Andorid以及一部分PC端有关的web代码.
主要有 mobile官网，mobile企业后台（停止维护阶段），iOS & Andorid 内嵌webview，微信红包活动（未上线），pc版移动端运营平台，pc版运营在线聊天工具
<!--more-->

### 目录结构

```
└─iqx_mob_webapp
   ├─api                        # AT发布系统HealthCheck接入
   ├─config                     # 不同环境部署配置
   ├─css 
   ├─kf                 # 移动端运营平台，基于angular
   ├─video                # 手机官网video
   ├─webim                # 运营聊天平台,入口是 kf/#/login
   ├─webview              # native app webview html
   ├─minisite               # deprecated.手机minisite(2014版)
   ├─weixin               # deprecated.微信红包项目静态页(未上线)，基于react 
   ├─im                 # deprecated.原运营聊天平台，基于pc机构端im代码改写(2015版)
   ├─img 
   ├─js 
   │  ├─main.js                     # 大部分页面都会引入的js，包含全局变量，本地环境配置，常用函数，封装ajax，全局处理，native app通信
   │  ├─doc-record                  # 群星app ［我的记录］webview，基于react
   │  │  ├─build
   │  │  └─src
   │  ├─webview                   # native app webview js
   │  │  ├─doc-record-detail.js     # 群星app ［我的记录］webview
   │  │  ├─hack4app.js          # 保理app内嵌群星社区相关代码
   │  │  ├─project-detail.js      # 保理app［发现］webview
   │  │  └─project-list.js        # 保理app［发现］webview
   │  ├─vendor                    # js库
   │  │  └─WebViewJavascriptBridge.js   # webview bridge
   │  └─weixin                    # deprecated.微信红包项目(未上线)，基于react 
   └─html                       # 手机官网静态页 
      ├─maintenance.html                # 维护页面
      ├─registration.html               # 机构端注册页面
      └─registration-minisite.html    # minisite注册页面
```

### 运行方式

1. http-server

    ```
$> npm install -g http-server
$> http-server -p 端口号
    ```

    注意修改/js/main.js 的default_host，置为T环境

2. nginx
    
    如果方式1因为跨域问题报错（有时T环境会有），可以采用nginx反向代理方式启动
    nginx.conf 添加如下代码(以下例子使用t5 api)
    
    ```
location ^~ /services/{
  proxy_pass  http://at5.dcfservice.com/services/;
}
    ```

    注意修改/js/main.js 的default_host，置为空字符串

### 调试方式

- mobile browser 调试可以采用chrome的device mode

- 内嵌webview 采用Charles(Mac)代理抓取请求。具体见[移动端前端开发调试](http://f2e.im/t/882)
   
### 注意事项

- 根目录下的html文件大部分属于mobile企业后台。

- d.htm org.html分别为企业端和保理端app下载地址。

- session没有采用cookie，而是http header中添加自定义tk。至于token是base64编码后作为url参数传递的。


------

## 移动端运营平台项目

### 项目简介

这个SPA项目基于angular 1.5，使用ngRoute作为路由，ui-bootstrap作为UI库。
模块化方面抛弃requirejs，而使用ng自带的module，配合gulp合并打包所有js和css。
代码方面前期页面的CRUD操作会分成不同的controller和template（比如UserAddModal和UserEditModal），
后期合并成一个controller和template（比如EditClientModal）。

### 目录结构

```
└─kf
   ├─app                        # src
   │  ├─app.js              # 入口js，包含路由，全局拦截器及导航
   │  ├─controllers                 
   │  ├─directives                  
   │  └─services  
   │     └─DCMResources.js        # api       
   ├─dist                       # 生成目录
   ├─fonts 
   ├─img                
   ├─lib              
   ├─partials               # html模版
   └─style
      └─all.scss              # 主要css
```

### 运行方式

```
$> npm install
$> gulp
```

### 注意事项

- 开发时browserSync会作为server并监听文件变化，不需要起其他web容器

- session没有采用cookie，而是POST中作为参数传递。至于token是保存在localstorage中的。

------

## 运营聊天工具

### 项目简介

项目基于环信 WebIM sdk，在此基础上侵入式修改😅。
主要修改了UI，增加了聊天的加密解密，聊天记录的保存。

### 目录结构

```
└─webim
   ├─custom.js                      # 主要js
   ├─easemob.im.config.js               # 配置        
   ├─index.html                     # 有些逻辑在index.html上，主要是sdk的锅     
   ├─css                        
   ├─sdk                        
   └─img
```

### 运行方式

使用移动端运营平台登录，当登录账号的角色是**客服**时自动跳转到运营聊天工具


------

## 群星金融APP-我的记录

### 项目简介

项目基于react，采用requirejs进行模块化管理，react-router进行路由管理。
更新:2016.6 增加还款记录/还款记录详情，其中还款记录详情还是采用zepto编写。

### 目录结构

```
└─js
   ├─webview                  
   │  └─doc-record-detail.js        # 还款记录详情
   └─doc-record                   
      ├─build
      └─src                   # 主要js
```

### 运行方式

主项目里启动，以下是额外的jsx编译（在doc-record目录运行）

```
$> npm install -g react-tools
$> jsx --watch src/ build/
```

### 注意事项

- 开发时browserSync会作为server并监听文件变化，不需要起其他web容器

- API原因导致token混合在http header和POST参数中。其中 *融资纪录* *货款记录* 属于前者，*还款记录* 属于后者

- 因为顶部导航tab是由native app控制，所以当在浏览器调试时切换tab可在url中切换hash
    - #/loan
    - #/payment
    - #/repayment

------

## 群星金融保理APP-发现

### 项目简介

项目基于zepto，内嵌于APP

### 目录结构

```
└─iqx_mob_webapp
   ├─webview
   │  ├─project-detail.html
   │  └─project-list.html
   └─js
      └─webview
         ├─project-detail.js
         └─project-list.js
```

### 运行方式

主项目里启动

### 注意事项

- token由群星金融保理APP传递在url中，且不与mobile企业后台共同。建议用charles抓取url后在本地调试。
