# 操作：

## 创建项目的jQuery：

1.创建项目文件夹，run the code:

```bash
git clone git://github.com/jquery/jquery.git
```

```bash
cd jquery && npm run build
```



## 配置jquery：

1.下载文件jquery.js

2.引入jQuery库,在body标签尾部添加script标签，尽量在window.onload=function(){}函数内进行：

```html
<script src="jquery/src/jquery.js" type="text/javascript"></script>
<script type="text/javascript">
    $(function(){  //等待网页中所有Dom结构绘制完毕
        ...
    });
</script>
```



## 配置jQuery插件:

在<script>标签的src属性添加外部插件,常见的插件有：

jQuery UI插件：优化UI界面

jQuery Mobile插件：优化移动端的UI界面

Validation插件：简化表单验证

Form插件：将html表单升级为Ajax提交方式

<u>具体详见jQuery插件的使用和写法</u>

























































