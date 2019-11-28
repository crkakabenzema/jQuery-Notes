# jQuery-Notes
Notes about jQuery

# **jQuery使用Notes：**

## **概念**:

 jQuery对象和DOM对象：

DOM对象：var domObj = document.getElementById("id");  //获得DOM对象

​                     var item = document.getElementsByTagName("p"); //获取网页中的p元素

jQuery对象：指通过jQuery包装DOM对象后产生的对象,通过$()函数制造出来，该函数就是一个jQuery对象的制造工厂。

当使用jQuery.noConflict()时，程序将jQuery()函数作为jQuery对象的制造工厂。

也可自定义制造工厂的快捷方式，如：var $j = jQuery.noConflict();

CSS选择器：

1.标签选择器：以文档元素作为选择符   E{CSS规则}

2.ID选择器：以文档元素的唯一标识符ID作为选择符   #ID{CSS规则}

3.类选择器：以文档元素的class作为选择符   E.className{CSS规则}

4.群组选择器：多个选择符应用同样的样式规则   E1,E2,E3{CSS规则}

5.后代选择器：元素E的任意后代元素F   #links a {CSS规则}

6.通配符选择器：以文档所有元素作为选择符   * {CSS规则}

jQuery选择器：

沿用CSS选择器规则

## **操作**：

### 一.创建项目的jQuery：

1.创建项目文件夹，run the code:

```bash
git clone git://github.com/jquery/jquery.git
```

```bash
cd jquery && npm run build
```

### 二.配置jquery：

1.下载文件jquery.js

2.引入jQuery库,<head>标签内引入jQuery：

```html
<script src="jquery/src/jquery.js" type="text/javascript"></script>
<script type="text/javascript">
    $(function(){  //等待网页中所有Dom结构绘制完毕
        ...
    });
</script>
```

### 三.较复杂的jquery操作说明：

#### 3.1 jQuery对象的常用初始化方法:

3.1.1初始化含有idName的html元素，添加符号#：

```html
<input type="checkbox" id="cr"/>
```

```javascript
var $cr = $("#cr");
```

3.1.2初始化含有className的html元素，添加符号 . :

```html
<li class="level1">
```

```javascript
var $a = $(".level1");
```

3.1.3 初始化含有className的子元素，添加符号>:

```html
<li class="level1">
  <a>A</a>
</li>
```

```javascript
var $a = $(".level1>a");

```

#### 3.2 jquery同一对象的较多操作

为保持代码清晰易读，建议每行写一个操作：

```javascript
$(".level1>a").click(function(){   //选取class含有level1的a元素
    $(this).removeClass("mouseout")
        .addClass("mouseover")
        .stop()
        .fadeTo("fast",0.6)
        .fadeTo("fast",1)
        .unbind("click")
        .click(function(){
              // do something
        });
});

```

#### 3.3 较复杂的jQuery选择器说明：

在一个id为table的表格的tbody中，如果每行的一列中的checkbox没有被禁用，则该行背景设为红色：

```javascript
$("#table>tbody>tr:has(td:has(:checkbox:enabled))").css("background","red");            

```

#### 3.4 jQuery对象转成DOM对象：

有两种方法

3.4.1方法1：jQuery对象是一个类似数组的对象，通过[index]方法得到相应的DOM对象：

```javascript
var $cr = $("#cr");    //jQuery object
var cr = $cr[0];         //DOM object
alert(cr.checked);     //检测checkbox是否被选中

```

3.4.2方法2：通过get(index)方法得到相应的DOM对象：

```javascript
var $cr = $("#cr");
var cr = $cr.get(0);
alert(cr.checked);

```

3.5 DOM对象转成jQuery对象：

对于一个DOM对象，只需要用$()把DOM对象包装起来，就可以获得jQuery对象：

```
var cr = document.getElementById("cr");   //DOM对象
var $cr = $(cr);   //jQuery对象

```
