# DOM操作

## DOM操作的分类

DOM操作分为3个方面：DOM CORE核心，HTML-DOM和CSS-DOM

## 节点操作：

### 创建节点示例：

```javascript
var $li_1 = $("<li></li>");   //创建<li>元素
var $li_2 = $("<li></li>");      
$("ul").append($li_1).append($li_2);   //追加添加到<ul>节点中
$("ul").appendTo("p");   //追加添加到<p>节点中
$("ul").prepend("p");   //前置添加到<ul>节点中
$("ul").prependTo("p");   //前置添加到<p>节点中
$("ul").after("p");   //每个ul后插入p
$("ul").insertAfter("p");   /每个p后插入ul
$("ul").before("p");   //每个ul前插入p
$("ul").insertbefore("p");   //每个p前插入ul
```

### 删除节点示例：

```javascript
var $ul = $("ul").remove();   //删除元素，返回一个指向已被删除的节点的引用
$ul.appendTo("ul");   //删除后$ul可继续使用
```

detach()方法和remove()类似，不同的是，所有绑定的事件、附加的数据被保留下来。

empty()方法，清空节点和内容。

### 复制节点示例：

```javascript
$(this).clone();    //复制当前节点
$(this).clone(true);   //复制当前节点和其绑定的事件
```

### 替换节点示例：

```javascript
$("p").replaceWith("...");   //把p替换为...
$("...").replaceAll("p");   //把..替换为p
```

### 包裹节点示例：

```javascript
$("strong").wrap("<b></b>");   //每个<strong>包裹一对<b>标签
$("strong").wrapAll("<b></b>");   //用一对<b>标签把所有<strong>包裹起来
$("strong").wrapInner("<b></b>");   //每个<strong>子内容包裹一对<b>标签
```

## 属性操作：

### 获取属性和设置属性示例：

```javascript
var $para = $("p");  
var p_txt = $para.attr("title":"your title","name":"test");   //获取和设置元素节点属性title
```

### 删除属性示例：

```javascript
$("p").removeAttr("title");   //删除元素的属性title
```

## 样式操作：

### 获取样式和样式设置示例:

```javascript
var p_class = $("p").attr("class");   //获取<p>元素的class
$("p").attr("class","high");   //设置元素的class为high
```

### 追加样式示例：

```javascript
$("p").addClass("another");   //给元素追加”another“类
```

### 移除样式示例：

```javascript
$("p").removeClass("high");   //移除元素的high类
```

### 切换样式示例：

```javascript
$("p").toggleClass("another");   //切换为类名”another“
```

### 判断样式示例：

```javascript
$("p").hasClass("another");   //判断是否含有某个样式
```

## 获取和设置HTML、Text和Value

### html()方法示例：

```javascript
var p_html = $("p").html();   //获取元素的html code
```

### text()方法示例：

```javascript
var p_text = $("p").text();   //获取元素的text code
```

### val()方法示例：

val()方法不仅能设置元素的值，获取元素值，还能使select(下拉列表框)、checkbox(多选框)和radio(单选框)相应的选项被选中**(用于表单操作)**

设置和获取元素的值

```javascript
var txt_value = $(this).val();   //获取值
$(this).val("...");   //设置值
```

## 选取节点

### children()方法：

```javascript
var $body = $("body").children();   //匹配元素的所有子元素个数（只考虑子元素）
```

### next()方法：

```javascript
var $pl = $("p").next();   //匹配元素后面紧邻的同辈元素
```

### prev()方法:

```javascript
var $ul = $("ul").prev();   //匹配元素前面紧邻的同辈元素
```

### siblings()方法：

```javascript
$(this).siblings();   //匹配元素前后所有的同辈元素
```

### parent(),parents()与closest()的区别：

parent()   获得集合中每个匹配元素的父级元素，返回一个元素节点

parents()   获得集合中每个匹配元素的祖先元素，返回多个父节点

closeset()   从元素本身开始，逐级向上匹配，返回最先匹配的第一个元素节点

### find()方法：

```javascript
$(this).find(element/selector);   //选取find()方法匹配的element/selector   
```

### end方法():

```javascript
$(this).method().method().end();   //结束在当前链的最近过滤操作，且返回选取元素的先前状态
```

