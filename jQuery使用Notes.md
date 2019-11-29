# **jQuery使用Notes：**

## **概念**:

 **jQuery对象和DOM对象：**

DOM对象： DOM是以[层次结构](https://baike.baidu.com/item/层次结构)组织的节点或信息片断的集合 

jQuery对象：指通过jQuery包装DOM对象后产生的对象,通过$()函数制造出来，该函数就是一个jQuery对象的制造工厂。

当使用jQuery.noConflict()时，程序将jQuery()函数作为jQuery对象的制造工厂。

也可自定义制造工厂的快捷方式，如：var $j = jQuery.noConflict();

**CSS选择器：**

1.标签选择器：以文档元素作为选择符   E{CSS规则}

2.ID选择器：以文档元素的唯一标识符ID作为选择符   #ID{CSS规则}

3.类选择器：以文档元素的class作为选择符   E.className{CSS规则}

4.群组选择器：多个选择符应用同样的样式规则   E1,E2,E3{CSS规则}

5.后代选择器：元素E的任意后代元素F   #links a {CSS规则}

6.通配符选择器：以文档所有元素作为选择符   * {CSS规则}

**jQuery选择器：**

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

2.引入jQuery库,在body标签尾部添加script标签，尽量在window.onload=function(){}函数内进行：

```html
<script src="jquery/src/jquery.js" type="text/javascript"></script>
<script type="text/javascript">
    $(function(){  //等待网页中所有Dom结构绘制完毕
        ...
    });
</script>
```

### 三.DOM对象和jQuery对象的初始化：

#### 3.1DOM对象初始化：**

Id型：

document.getElementById("btn"); //获得id为btn的DOM对象

Tag型：

document.getElementsByTagName("p"); //获取网页中的p元素

elementName型：

document.getElementByName("check"); //获得name为check的元素

#### 3.2jQuery对象初始化：

##### 基本的初始化：

$("#test"):选取id为test的元素   (单个元素，id选取用符号#）

$(".test"):选择class为test的元素    (集合元素，class选取用符号.）

$("p"):选择elementName为p的元素   (集合元素)

$("div,span,p.myClass"):选择所有<div>,<span>和拥有class为myClass的<p>标签的一组元素   (集合元素)

##### 层次型初始化：

$("ancestor descendant"): 选取ancestor元素里所有的descendant元素

$("parent>child"):仅选取child元素

$("prev").siblings("siblings"):无论前后位置，选取prev所有siblings元素

$("prev~siblings")或者$("prev").nextAll("siblings"):选取prev元素之后的所有siblings元素

$("prev+next")或者$("prev").next("next"):仅选取紧接在prev元素后的next元素

##### 过滤型初始化（在第一二两种类型里添加过滤条件）：

:first:选取第一个元素

:last:选取最后一个元素

:not(selector):去除与给定选择器匹配的元素

:even:选取索引是偶数的元素

:odd:选取索引是奇数的元素

:eq(index):选取索引等于index的元素

:gt(index):选取索引大于index的元素

:lt(index):选取索引小于index的元素

:header:选取所有的标题元素

:animated:选取正在执行动画的元素

:focus: 选取当前获取焦点的元素

##### 内容过滤型初始化（在第一二两种类型里添加过滤条件）：

:contains(‘text’):选取含有文本内容为text的元素

:empty:选取不包含子元素或文本的空元素

:has(selector):选取含有选择器所匹配的元素的元素

:parent:选取含有子元素或者文本的元素

可见性过滤型初始化（在第一二两种类型里添加过滤条件）：

:hidden:选取所有不可见的元素

:visible:选取所有可见的元素

##### 属性过滤型初始化（在第一二两种类型里添加过滤条件）：

[attribute]:选择拥有此属性的元素
[attribute=value]:选择属性的值为value的元素

!=value: 不等于；^=value: 以value开始；$value: 以value结束；

*=value: 含有value; |=value: 等于给定字符串或以该字符串为前缀的元素

~=value: 用空格分隔的值中包含给定值的元素

##### 子元素过滤型初始化（在第一二两种类型里添加过滤条件）：

:nth-child(index/even/odd/equation): 选取每个父元素下的第index个子元素或者奇偶元素

:first-child:选取每个父元素的第一个子元素

:last-child:选取每个父元素的最后一个子元素

:only-child:选取如果某元素是它父元素中唯一的子元素，如果父元素含有其他元素，则不会被匹配

##### 表单对象属性过滤型初始化（在第一二两种类型里添加过滤条件）：

:enabled:选取所有可用元素

:disabled:选取所有不可用元素

:checked:选取所有被选中的元素

:selected:选取所有被选中的选项元素

##### 表单对象初始化，除第一个外，其他元素用type值来标记：

$(":input"):选取所有的<input>、<textarea>、<select>和<button>元素

$(":text"):选取所有的单行文本框，

$(":password"):选取所有的密码框

$(":radio"):选取所有的单选框

$(":checkbox"):选取所有的多选框

$(":submit"):选取所有的提交按钮

$(":image"):选取所有的图像按钮

$(":reset"):选取所有的重置按钮

$(":button"):选取所有的按钮

$(":file"):选取所有的上传域

$(":hidden"):选取所有不可见元素

##### 特殊字符的处理：

含有"."、”#“、”(“、”]“等特殊字符，需使用转义字符\\转义

##### 含有空格的注意事项：

$('.test :hidden')和$('.test:hidden')有空格和没有空格表达的结果不同，前者为后代选择器，后者为过滤选择器



































### 四.较复杂的jquery操作说明：

#### 4.1 jQuery对象的常用初始化方法:

4.1.1初始化含有idName的html元素，添加符号#：

```html
<input type="checkbox" id="cr"/>
```

```javascript
var $cr = $("#cr");
```

4.1.2初始化含有className的html元素，添加符号 . :

```html
<li class="level1">
```

```javascript
var $a = $(".level1");
```

4.1.3 初始化含有className的子元素，添加符号>:

```html
<li class="level1">
  <a>A</a>
</li>
```

```javascript
var $a = $(".level1>a");
```

#### 4.2 jquery同一对象的较多操作

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

#### 4.3 较复杂的jQuery选择器说明：

在一个id为table的表格的tbody中，如果每行的一列中的checkbox没有被禁用，则该行背景设为红色：

```javascript
$("#table>tbody>tr:has(td:has(:checkbox:enabled))").css("background","red");            
```

#### 4.4 jQuery对象转成DOM对象：

有两种方法

4.4.1方法1：jQuery对象是一个类似数组的对象，通过[index]方法得到相应的DOM对象：

```javascript
var $cr = $("#cr");    //jQuery object
var cr = $cr[0];         //DOM object
alert(cr.checked);     //检测checkbox是否被选中
```

4.4.2方法2：通过get(index)方法得到相应的DOM对象：

```javascript
var $cr = $("#cr");
var cr = $cr.get(0);
alert(cr.checked);
```

4.5 DOM对象转成jQuery对象：

对于一个DOM对象，只需要用$()把DOM对象包装起来，就可以获得jQuery对象：

```
var cr = document.getElementById("cr");   //DOM对象
var $cr = $(cr);   //jQuery对象
```

















