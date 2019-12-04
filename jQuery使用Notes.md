# **jQuery使用Notes：**

## **概念**:

 **jQuery对象和DOM对象：**

DOM对象： Document Object Model，即文档对象模型。

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

加载DOM：

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

#### 3.2DOM对象获取某元素的src属性：

获取某元素的src属性：

element.getAttribute("src");

设置某元素的src属性：

element.setAttribute("src");

#### 3.3jQuery对象初始化：

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



### 四. DOM操作：

#### 4.1DOM操作的分类：

DOM操作分为3个方面：DOM CORE核心，HTML-DOM和CSS-DOM

#### 4.2节点操作：

##### 4.2.1创建节点示例：

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

##### 4.2.2删除节点示例：

```javascript
var $ul = $("ul").remove();   //删除元素，返回一个指向已被删除的节点的引用
$ul.appendTo("ul");   //删除后$ul可继续使用
```

detach()方法和remove()类似，不同的是，所有绑定的事件、附加的数据被保留下来。

empty()方法，清空节点和内容。

##### 4.2.3复制节点示例：

```javascript
$(this).clone();    //复制当前节点
$(this).clone(true);   //复制当前节点和其绑定的事件
```

##### 4.2.4替换节点示例：

```javascript
$("p").replaceWith("...");   //把p替换为...
$("...").replaceAll("p");   //把..替换为p
```

##### 4.2.5包裹节点示例：

```javascript
$("strong").wrap("<b></b>");   //每个<strong>包裹一对<b>标签
$("strong").wrapAll("<b></b>");   //用一对<b>标签把所有<strong>包裹起来
$("strong").wrapInner("<b></b>");   //每个<strong>子内容包裹一对<b>标签
```

#### 4.3属性操作：

##### 4.3.1获取属性和设置属性示例：

```javascript
var $para = $("p");  
var p_txt = $para.attr("title":"your title","name":"test");   //获取和设置元素节点属性title
```

##### 4.3.2删除属性示例：

```javascript
$("p").removeAttr("title");   //删除元素的属性title
```

#### 4.4样式操作：

##### 4.4.1获取样式和样式设置示例:

```javascript
var p_class = $("p").attr("class");   //获取<p>元素的class
$("p").attr("class","high");   //设置元素的class为high
```

##### 4.4.2追加样式示例：

```javascript
$("p").addClass("another");   //给元素追加”another“类
```

##### 4.4.3移除样式示例：

```javascript
$("p").removeClass("high");   //移除元素的high类
```

##### 4.4.4切换样式示例：

```javascript
$("p").toggleClass("another");   //切换为类名”another“
```

##### 4.4.5判断样式示例：

```javascript
$("p").hasClass("another");   //判断是否含有某个样式
```

#### 4.5获取和设置HTML、Text和Value

##### 4.5.1html()方法示例：

```javascript
var p_html = $("p").html();   //获取元素的html code
```

##### 4.5.2text()方法示例：

```javascript
var p_text = $("p").text();   //获取元素的text code
```

##### 4.5.3val()方法示例：

val()方法不仅能设置元素的值，获取元素值，还能使select(下拉列表框)、checkbox(多选框)和radio(单选框)相应的选项被选中**(用于表单操作)**

设置和获取元素的值

```javascript
var txt_value = $(this).val();   //获取值
$(this).val("...");   //设置值
```

#### 4.6遍历节点

##### 4.6.1children()方法：

```javascript
var $body = $("body").children();   //匹配元素的所有子元素个数（只考虑子元素）
```

##### 4.6.2next()方法：

```javascript
var $pl = $("p").next();   //匹配元素后面紧邻的同辈元素
```

##### 4.6.3prev()方法:

```javascript
var $ul = $("ul").prev();   //匹配元素前面紧邻的同辈元素
```

##### 4.6.4siblings()方法：

```javascript
$(this).siblings();   //匹配元素前后所有的同辈元素
```

##### 4.6.5parent(),parents()与closest()的区别：

parent()   获得集合中每个匹配元素的父级元素，返回一个元素节点

parents()   获得集合中每个匹配元素的祖先元素，返回多个父节点

closeset()   从元素本身开始，逐级向上匹配，返回最先匹配的第一个元素节点



### 五.jQuery中的事件和动画：

#### 5.1jQuery中的事件：

自定义事件见5.1.7

##### 5.1.1加载DOM

```javascript
$().ready(function(){
   //编写代码
})
```

##### 5.1.2事件绑定

element.bind(eventType,event.data,function);

element.bind(eventType, function).bind(eventType,function);

eventType: blur, focus, load, resize, scroll, unload, click, dbclick, mousedown, mouseup, mousemove, mouseover, mouseout, mouseenter, mouseleave, change, select, submit, keydown, keypress, keyup和error等

##### 5.1.3事件触发

.trigger()方法可以用作模拟用户操作，也可用于自定义事件和传递参数

```javascript
element.trigger(event.type);   //trigger an event
```

```javascript
element.bind(event.selfDefinedType, function(){
    ...
});
element.trigger(event.selfDefinedType);  
//trigger a self-defined event
```

```javascript
element.bind(event.selfDefinedType,function(event,data){
    ...
});
element.trigger(event.selfDefinedType,data);   
//trigger a self-defined event with data
```

##### 5.1.4移除事件

```javascript
element.unbind(event.type, function);   //解除绑定
```

```javascript
element.one(event.type, function);   //只触发一次
```

##### 5.1.5事件命空间

可为eventType添加命名空间eventType.namespace, 之后解绑定时可直接使用

```
element.unbind(".namespace")；
```

当只触发不包含在命名空间中的eventType时，可以使用

element.trigger("eventType!");   //作用是匹配所有不包含在命名空间的方法

##### 5.1.6hover()方法

```javascript
element.hover(function(){
    ...
}.function(){
    ...
});   //模拟光标悬停
```

等价于：

```javascript
element.mouseover(function(){
    ...
}).mouseout(function(){
    ...
})
```

##### 5.1.7事件冒泡

多层元素内嵌时，触发事件将按照DOM的层次结构由内向外响应。

event.stopPropagation()将阻止事件的冒泡

##### 5.1.8事件对象的属性

event.type:获取事件类型

event.preventDefault()：阻止默认的事件行为

```html
<a href="https://jquery.com">default click action is prevented</a>
<script>
$( "a" ).click(function( event ) {
  event.preventDefault();
});
</script>
```

event.stopPropagation()：阻止事件的冒泡

event.relatedTarget: 相关元素

event.pageX和event.pageY: 获取光标相对于页面的x坐标和y坐标

event.which: 获取鼠标左、中、右键

#### 5.2jQuery中的动画

##### 5.2.1show()和hide()方法

```javascript
element.show();
element.hide();
```

还可指定参数：fast、normal、slow和显示速度

##### 5.2.2fadeIn()和fadeOut()方法

只改变元素的不透明度

##### 5.2.3slideUp()和slideDown()方法

只改变元素的高度，slideUp()和slideDown()需一起使用

##### 5.2.4自定义动画animate()

```javascript
element.animate(params, speed, callback);
```

params: 样式属性及值的映射，{property1:"value1", property2:"value2"}

speed: 速度参数, fast、normal、slow和显示速度

callback: 动画完成时执行的回调函数

示例：

```javascript
element.click(function(){
    $(this).anmiate({left:"+=500px"},300,function(){
        $(this).css("border","5px solid blue");
    });
});
```

##### 5.2.5停止和延迟动画

```javascript
element.stop([clearQueue],[gotoEnd]);
```

clearQueue: boolean, 清空未执行的动画队列

gotoEnd: boolean, 直接跳转至未状态

```javascript
element.delay(speed);
```

##### 5.2.6判断是否处于动画状态

```javascript
element.is(":animated")
```



### 六.jQuery对表单、表格的操作及应用

表单组成部分：

表单标签：包含处理表单数据的服务端程序URL和数据提交到服务器的方法；

表单域：包含文本框、密码框、单选复选框等

表单按钮：包含提交按钮、复位按钮和一般按钮

#### 6.1表单应用

6.1.1单行文本框应用









































### .较复杂的jquery操作说明：

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

















