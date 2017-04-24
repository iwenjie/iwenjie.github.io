---
title: 群星一些前端插件和服务API
date: 2017-01-01 16:22:48
categories: 
  - 文档
  - 工具
tags: 
  - 文档
  - 工具
---

群星一些前端插件和服务API，使用示例，和参数说明
<!--more-->

### 日期控件

##### 依赖资源

jquery 和 select相关资源

```html
<link href="/assets/js/lib/jquery/plugin/select2/select2.min.css" rel="stylesheet">
<link href="/assets/js/lib/jquery/plugin/dropdown/jquery.dropdown.css" rel="stylesheet">
<script src="/assets/js/lib/jquery/plugin/select2/select2-v2.min.js"></script>
<script src="/assets/js/lib/jquery/plugin/select2/i18n/zh-CN.js"></script>
<script src="/assets/js/lib/jquery/plugin/dropdown/jquery.daterange.js"></script>
```

##### 调用示例

html 代码

```html
<div class="form-group">
    <label for="" class="breakword">融资申请日</label>
    <div class="btn-group">
        <div class="input-mask"></div>
        <input type="text" id="applyDate" />
    </div>
</div>
```

input-mask实现禁用遮罩 代码如下：

```css
.input-mask{
    position: absolute;
    display: none;
    z-index: 5;
    width: 100%;
    height: 31px;
    border-radius: 4px;
    cursor: not-allowed;
}
```

```javascript
//初始化
$element.DateRange({
    width: 210,  //宽度
    showClear: true,  //是否允许清空
    placeholder:'请选择XXX',
    pos: function($trigger,pos){

        var screenWidth = window.screen.width;

        pos.left = pos.left + 280 > screenWidth ? pos.left - 68 : pos.left;

        return pos;
    }//定位信息，相对左侧偏移量
});
//取值
$element.val(); //格式 2016/08/08|2016/08/08
//设值
$element.DateRange().setValue({
    startDate:new Date(new Date().getTime()-7*24*60*60*1000),
    endDate:new Date()
});
//渲染日期组件下拉的初始日期指示位置
$element.DateRange().renderBody({
    date: new Date(new Date().getTime()-7*24*60*60*1000)
});
```

### select2

##### 依赖资源

jquery

```html
<link href="/assets/js/lib/jquery/plugin/select2/select2.min.css" rel="stylesheet">
<script src="/assets/js/lib/jquery/plugin/select2/select2-v2.min.js"></script>
<script src="/assets/js/lib/jquery/plugin/select2/i18n/zh-CN.js"></script>
```
##### 调用示例
```javascript
$('.xxxx').select2({
    language: 'zh-CN',
    width: '210px',
    allowClear: true,
    placeholder: '请选择客户名称',
    data : results1
});


$('#xxx').select2({
    language: 'zh-CN',
    width: '210px',
    allowClear: true,
    placeholder: '请选择客户名称',
    dropdownParent: $('.select2-box'),
    ajax: {
        url: URL.SEARCH_CUSTOMER,
        type: 'GET',
        data: function (params) {
            console.info(params);
            var query = {
                customerName: params.term||'',
                dataSize: 10,
                page: params.page
            }
            // Query paramters will be ?search=[term]&page=[page]
            return query;
        },
        processResults: function (res, params) {
            
            params.page = params.page || 1;

            var items = []
            
            if(res.ret == 1 && res.result && res.result.length>0){

                for(var i = 0; i<res.result.length; i++){

                    items.push({
                        id: res.result[i].customerName,
                        text: res.result[i].customerName
                    })
                }
                return {
                    results: items,
                    // pagination: {
                        // more: (params.page * 10) < 20
                    // }
                };
            }
        },
        error: function(res){
            console.info('error');
        },
        delay: 250,
        cache: true
    }
});
```

### 查看微合同服务

##### 依赖资源

jquery

```html
<script src="/assets/js/lib/jquery/business/get-microContract/get-microContract.js"></script>

```
##### 调用示例

```javascript
$element.showMicroContract(id,{
    print:true //是否调用打印服务
});//id为单据id
```
### 查看单据详情服务

##### 依赖资源

jquery

```html
<script src="/assets/js/lib/jquery/business/docs-detail/docs-detail.js"></script>
```

##### 调用示例
```javascript
$.ShowDocsDetail(id);//id为单据id
```
