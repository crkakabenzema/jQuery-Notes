# DOM对象和jQuery对象的初始化

## DOM对象初始化

加载DOM,有id型、Tag型和Name型三种类型：

```javascript
$(window).load(function(){
  //编写代码
})
```

Id型：

```javascript
document.getElementById("btn"); //获得id为btn的DOM对象
```

Tag型：

```javascript
document.getElementsByTagName("p"); //获取网页中的p元素
```

elementName型：

```javascript
document.getElementByName("check"); //获得name为check的元素
```

## DOM对象获取某元素的src属性

获取某元素的src属性：

element.getAttribute("src");

设置某元素的src属性：

element.setAttribute("src");

## jQuery对象初始化

##### 基本的初始化：

加载DOM:

```javascript
$(document).ready(function(){
    ...
});   //DOM就绪就执行

$(document).load(function(){
    one();
    two();
});   //元素内容加载完毕后触发
    
$().ready(function(){
    ...
});   //简写
```

### id选取

$("#test"):选取id为test的元素   (单个元素，id选取用符号#）

### class选取

$(".test"):选择class为test的元素    (集合元素，class选取用符号.）

### element选取

$("p"):选择elementName为p的元素   (集合元素)

### 多元素选取

$("div,span,p.myClass"):选择所有<div>,<span>和拥有class为myClass的<p>标签的一组元素   (集合元素)

### 多元素下的单个选取

$("option:selected", this);   //获取选中的选项

### 层次型初始化

$("ancestor descendant"): 选取ancestor元素里所有的descendant元素

$("parent>child"):仅选取child元素

$("prev").siblings("siblings"):无论前后位置，选取prev所有siblings元素

$("prev~siblings")或者$("prev").nextAll("siblings"):选取prev元素之后的所有siblings元素

$("prev+next")或者$("prev").next("next"):仅选取紧接在prev元素后的next元素

### 过滤型初始化（在第一二两种类型里添加过滤条件）

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

### 内容过滤型初始化（在第一二两种类型里添加过滤条件）

:contains(‘text’):选取含有文本内容为text的元素

:empty:选取不包含子元素或文本的空元素

:has(selector):选取含有选择器所匹配的元素的元素

:parent:选取含有子元素或者文本的元素

可见性过滤型初始化（在第一二两种类型里添加过滤条件）：

:hidden:选取所有不可见的元素

:visible:选取所有可见的元素

### 属性过滤型初始化（在第一二两种类型里添加过滤条件）

[attribute]:选择拥有此属性的元素
[attribute=value]:选择属性的值为value的元素

!=value: 不等于；^=value: 以value开始；$value: 以value结束；

*=value: 含有value; |=value: 等于给定字符串或以该字符串为前缀的元素

~=value: 用空格分隔的值中包含给定值的元素

### 子元素过滤型初始化（在第一二两种类型里添加过滤条件）

:nth-child(index/even/odd/equation): 选取每个父元素下的第index个子元素或者奇偶元素

:first-child:选取每个父元素的第一个子元素

:last-child:选取每个父元素的最后一个子元素

:only-child:选取如果某元素是它父元素中唯一的子元素，如果父元素含有其他元素，则不会被匹配

### 表单对象属性过滤型初始化（在第一二两种类型里添加过滤条件）

:enabled:选取所有可用元素

:disabled:选取所有不可用元素

:checked:选取所有被选中的元素

:selected:选取所有被选中的选项元素

##### 表单对象初始化，除第一个外，其他元素用type值来标记：

$(":input"):选取所有的<input>/<textarea>/<select>和<button>元素

$(":text"):选取所有的单行文本框

$(":password"):选取所有的密码框

$(":radio"):选取所有的单选框

$(":checkbox"):选取所有的多选框

$(":submit"):选取所有的提交按钮

$(":image"):选取所有的图像按钮

$(":reset"):选取所有的重置按钮

$(":button"):选取所有的按钮

$(":file"):选取所有的上传域

$(":hidden"):选取所有不可见元素

### 特殊字符的处理

含有"."、”#“、”(“、”]“等特殊字符，需使用转义字符\\转义

### 含有空格的注意事项

$('.test :hidden')和$('.test:hidden')有空格和没有空格表达的结果不同，前者为后代选择器，后者为过滤选择器















