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

**jQuery对象转换为DOM对象：**

有两种方法

方法1：jQuery对象是一个类似数组的对象，通过[index]方法得到相应的DOM对象：

```javascript
var $cr = $("#cr");    //jQuery object
var cr = $cr[0];         //DOM object
alert(cr.checked);     //检测checkbox是否被选中
```

方法2：通过get(index)方法得到相应的DOM对象：

```javascript
var $cr = $("#cr");
var cr = $cr.get(0);
alert(cr.checked);
```

**DOM对象转成jQuery对象：**

对于一个DOM对象，只需要用$()把DOM对象包装起来，就可以获得jQuery对象：

```
var cr = document.getElementById("cr");   //DOM对象
var $cr = $(cr);   //jQuery对象
```



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

###### id选取：

$("#test"):选取id为test的元素   (单个元素，id选取用符号#）

###### class选取：

$(".test"):选择class为test的元素    (集合元素，class选取用符号.）

###### element选取：

$("p"):选择elementName为p的元素   (集合元素)

###### 多元素选取：

$("div,span,p.myClass"):选择所有<div>,<span>和拥有class为myClass的<p>标签的一组元素   (集合元素)

###### 多元素下的单个选取：

$("option:selected", this);   //获取选中的选项

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

#### 4.6选取节点

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

##### 4.6.6find()方法：

```javascript
$(this).find(element/selector);   //选取find()方法匹配的element/selector   
```

##### 4.6.7end方法():

```javascript
$(this).method().method().end();   //结束在当前链的最近过滤操作，且返回选取元素的先前状态
```



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

```javascript
element.bind(eventType,event.data,function);
element.bind(eventType, function).bind(eventType,function);
```

eventType: blur, focus, load, resize, scroll, unload, click, dbclick, mousedown, mouseup, mousemove, mouseover, mouseout, mouseenter, mouseleave, change, select, submit, keydown, keypress, keyup和error等

##### 5.1.3事件触发

.trigger()方法可以用作模拟用户操作，也可用于自定义事件和传递参数

```javascript
element.trigger(event.type);   //trigger an event
```

自定义触发事件（触发元素绑定的selfDefinedType事件，和浏览器默认的selfDefinedType事件）

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

自定义触发事件（仅触发元素绑定的selfDefinedType事件）

```javascript
element.triggerHandler(event.selfDefinedType);
```

事件的迭代触发

```javascript
element.each(function(index,element){
    ...
});
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

jQuery通过attr()访问对象的属性

##### 6.1.1单行文本框应用示例：

```html
<form action="#" method="POST" id="regForm">
    <fieldset>
        <legend>Personal Information</legend>
        <div>
            <label for="username">名称：</label>
            <input id="username" type="text">
        </div>
        <div>
            <label for="pass">密码：</label>
            <input id="pass" type="password">
        </div>
        <div>
            <label for="msg">详细信息：</label>
            <textarea id="msg"></textarea>
        </div>
    </fieldset>
</form>
```

```css
input:focus, textarea:focus {
            border: 1px solid #f00;
            background: #fcc;
}
```

```javascript
$(":input").focus(function () {
                $(this).addClass("focus");
            }).blur(function () {
                $(this).removeClass("focus");
            });
```

##### 6.1.2多行文本框应用示例：

文本框高度属性：height; 文本框滚动条属性：scrollTop

```html
<form>
        <div class="msg">
            <div class="msg_caption">
                <span class="up">向上</span>
                <span class="down">向下</span>
                <span class="bigger">放大</span>
                <span class="smaller">缩小</span>
            </div>
            <div>
                <textarea id="comment" rows="8" cols="20">多行文本框高度变化，多行文本框高度变化,
多行文本框高度变化，多行文本框高度变化，多行文本框高度变化，多行文本框高度变化
                </textarea>
            </div>
        </div>
</form>
```

```javascript
var $comment = $('#comment');   //获取评论框
$('.bigger').click(function () {   //放大按钮绑定单击事件
    if (!$comment.is(":animated")) {
        if ($comment.height() < 500) {
            $comment.animate({ height: "+=50" }, 400);
        }
    }
})

$('.smaller').click(function () {
    if (!$comment.is(":animated")) {
        if ($comment.height() > 50) {
            $comment.animate({ height: "-=50" }, 400);
        }
    }
});

$('.up').click(function () {   //向上按钮绑定单击事件                if (!$comment.is(":animated")) {
    $comment.animate({ scrollTop: "-=50" }, 400);
   }
});

$('.down').click(function () {   //向下按钮绑定单击事件                if (!$comment.is(":animated")) {
    $comment.animate({ scrollTop: "+=50" }, 400);
    }
});
```

##### 6.1.3复选框应用示例：

通过设置input的flag，使input之间联动

```html
<form>
    <fieldset>
        你爱好的运动是？<br />
        <input type="checkbox" id="CheckedAll"/>全选/全不选<br/>
        <input type="checkbox" name="items" value="soccer" />soccer
        <input type="checkbox" name="items" value="basketball" />basketball
        <input type="checkbox" name="items" value="badminton" />badminton
        <input type="checkbox" name="items" value="table tennis" />table tennis<br />
        <input type="button" id="CheckedRev" value="反选" />
        <input type="button" id="Send" value="提交" />
    </fieldset>
</form>
```

```javascript
$("#CheckedAll").click(function () {   //全选/全不选
    $('[name=items]:checkbox').attr("checked", this.checked);
});
//通过flag使input与checkbox联动

$('[name=items]:checkbox').click(function () {            
    var flag = true;
    $('[name=items]:checkbox').each(function () {
        if (!this.checked) {
            flag = false;
        }
    });
    $('#CheckedAll').attr('checked', flag);
});

$("#CheckedRev").click(function () {   //反选    
    $('[name=items]:checkbox').each(function () {
        $(this).attr("checked", !$(this).attr("checked"));
    });
});

$("#Send").click(function () {   //提交
    var str = "你选中的是： \r\n";
    $('[name=items]:checkbox:checked').each(function () {
        str += $(this).val() + "\r\n";
    });
    alert(str);
});            
```

##### 6.1.4下拉框应用示例：

```html
<div class="centent">
    <select multiple id="select1" style="width:100px;height:160px;">
        <option value="1">Option 1</option>
        <option value="2">Option 2</option>
        <option value="3">Option 3</option>          
        <option value="4">Option 4</option>
        <option value="5">Option 5</option>
        <option value="6">Option 6</option>           
        <option value="7">Option 7</option>
        <option value="8">Option 8</option>
    </select>
    <div>
        <span id="add">选中添加到右边&gt;&gt;</span>
        <span id="add_all">全部添加到右边&gt;&gt;</span>
    </div>
</div>
<div class="centent">
    <select multiple id="select2" style="width:100px;height:160px;" >
    </select>
    <div>
        <span id="remove">&lt;&lt;选中删除到左边</span>
        <span id="remove_all">&lt;&lt;全部删除到左边</span>
    </div>
</div>
```

```javascript
$('#add').click(function () {
    var $options = $('#select1 option:selected');   //获取选中的选项
    $options.appendTo('#select2');   //追加给对方
});

$('#add_all').click(function () {
    var $options = $('#select1 option');   //获取全部的选项
    $options.appendTo('#select2');   //追加给对方
});

$('#select1').dblclick(function () {
    var $options = $("option:selected", this);   //获取选中的选项
    $options.appendTo('#select2');
});
```

##### 6.1.5表单验证示例：

```html
<form method="post" action="">
    <div class="int">
        <label for="username">Username:</label>
        <input type="text" id="username" class="required" />
    </div>
    <div class="int">
        <label for="email">Email:</label>
        <input type="text" id="email" class="required" />
    </div>
    <div class="int">
        <label for="personinfo">PersonInfo:</label>
        <input type="text" id="personinfo" />
    </div>
    <div class="sub">
        <input type="submit" value="submit" id="send"/>
        <input type="reset" id="res"/>
    </div>
</form>
```

element.triggerHandler(eventType); (仅触发元素绑定的事件，不会触发浏览器默认的eventType事件)

```javascript
$("form :input.required").each(function () {
    var $required = $("<strong class='high'> *</strong>");   //创建元素
    $(this).parent().append($required);   //将其追加到文档中
});

$('form :input').blur(function () {   //为表单元素添加失去焦点事件
    var $parent = $(this).parent();
    $parent.find(".formatips").remove();   //删除以前的提醒元素
    //验证用户名
    if ($(this).is('#username')) {
        if (this.value == "" || this.value.length < 6) {
            var errorMsg = "请输入至少6位的用户名.";
            $parent.append('<span class="formatips onError">' + errorMsg + '</span>');
        } else {
            var okMsg = '输入正确.';
                $parent.append('<span class="formatips onSuccess">' + okMsg + '</span>');
        }
    }
    //验证邮箱
    if ($(this).is('#email')) {
        if (this.value == "" || (this.value !== "" && !/.+@.+\.[a-zA-Z]{2.4}$/.test(this.value))) {
            var errorMsg = '请输入正确的E-Mail地址';
            $parent.append('<span class="formatips onError">'+errorMsg+'</span>');
        }else{
            var okMsg = '输入正确.';
            $parent.append('<span class="formatips onSuccess">' + okMsg + '</span>');
        }
    }
}).keyup(function () {
    $(this).triggerHandler("blur");
}).focus(function () {
    $(this).triggerHandler("blur");
});

$("#send").click(function () {
    $("format .required:input").trigger('blur');          
    var numError = $('form.onError').length;
    if (numError) {
        return false;
    }
    alert('register successfully');
});
```

##### 6.1.6表格高亮和展开/关闭示例：

```html
<span>筛选：<input type="search" id="filterName"><input type="button" value="确认" id="confirm"></span>
<table>
    <thead>
        <tr><th></th><th>Name</th><th>Gender</th>     <th>Residence</th></tr>
    </thead>
    <tbody>
        <tr class="parent" id="row_01"><td colspan="4">前台设计组</td></tr>
        <tr class="child_row_01"><td><input type="checkbox" id="checkbox" /></td><td>张三</td><td>男</td><td>宁波</td></tr>
        <tr class="child_row_01"><td><input type="checkbox" id="checkbox" /></td><td>张三</td><td>男</td><td>宁波</td></tr>

        <tr class="parent" id="row_02"><td colspan="4">前台开发组</td></tr>
        <tr class="child_row_02"><td><input type="checkbox" id="checkbox" /></td><td>张三</td><td>男</td><td>宁波</td></tr>
        <tr class="child_row_02"><td><input type="checkbox" id="checkbox" /></td><td>张三</td><td>男</td><td>宁波</td></tr>

        <tr class="parent" id="row_03"><td colspan="4">后台开发组</td></tr>
        <tr class="child_row_03"><td><input type="checkbox" id="checkbox" /></td><td>张三</td><td>男</td><td>宁波</td></tr>
        <tr class="child_row_03"><td><input type="checkbox" id="checkbox" /></td><td>张三</td><td>男</td><td>宁波</td></tr>
    </tbody>
</table>
```

```javascript
$('tbody :checkbox').click(function () {
    //判断当前是否选中
    if (!this.checked) {
        $(this).parent().parent()
            .removeClass('selected')
            .find('#checkbox').attr('checked', false);                } else {
            $(this).parent().parent()
                .addClass('selected')
                .find('#checkbox').attr('checked', true);        }
});

$('tr.parent').click(function () {
    $(this)
        .toggleClass('selected')
        .siblings('.child_' + this.id).toggle();   
        //隐藏/显示所谓子行
});
```

##### 6.1.7表格内容筛选示例：

```javascript
$("#confirm").click(function () {
    $("table tbody tr").hide()
        .filter(":contains('" + ($("#filterName").val()) + "')").show();
}); 
```

##### 6.1.8网页选项卡示例：

element.index(this)方法用于返回当前元素的index;

.hover(function(){ ... }), function(){ ... };用于鼠标悬浮事件;

```css
.tab_box {
    margin-left:35px;
    padding: 5px;
    border-style: solid;
    border-width: 3px;
}

div.tab_menu {
    padding: 5px;
    max-height:35px;
}

.tab_menu li {
    border-style: solid;
    border-width: 3px;
    list-style-type: none;
    display: inline-block;
    vertical-align: text-top;
}

.selected {
    background-color: deepskyblue;
}

.hover {
    background-color:aquamarine;
}

.hide {
    display:none;
}
```

```html
<div class="tab">
    <div class="tab_menu">
        <ul>
            <li class="selected">Time</li>
            <li>Sports</li>
            <li>Entertainment</li>
        </ul>
    </div>
    <div class="tab_box">
        <div>Time</div>
        <div class="hide">Sports</div>
        <div class="hide">Entertainment</div>
    </div>
</div>
```

```javascript
$(document).ready(function () {
    var $div_li = $(".tab_menu ul li");
    $div_li.click(function () {
        $(this).addClass("selected")
            .siblings().removeClass("selected");
        var index = $div_li.index(this);  //获取当前单击<li>元素在全部元素的index
        $("div.tab_box>div")
            .eq(index).show()
            .siblings().hide();
    }).hover(function () {   //光标滑过效果          
        $(this).addClass("hover");
    },function(){
        $(this).removeClass("hover");
    });
});
```



#### 七.jQuery操作网页样式示例：

修改字体大小：

element.css('propertyName', propertyValue);

```html
<div class="msg_caption">
    <span class="bigger">放大</span>
    <span class="smaller">缩小</span>
</div>
<div>
    <p id="para">
        This is some text
    </p>
</div>
```

```javascript
$("span").click(function () {
    var thisEle = $("#para").css("font-size");   //获取id为para的字体大小
    var textFontSize = parseInt(thisEle, 10);    //获取int值
    var unit = thisEle.slice(-2);   //获取px
    var cName = $(this).attr("class");
    if (cName == "bigger") {
        textFontSize += 2;
    } else if (cName == "smaller") {
        textFontSize -= 2;
    }
    $("#para").css("font-size", textFontSize + unit);
});
```



#### 八.jQuery与Ajax的应用:

Ajax的核心是XMLHttpRequest对象，通过它来完成异步请求、接受响应及执行回调。

##### 8.1 JavaScript的Ajax应用示例：

```html
<input type="button" value="Ajax提交" onclick="Ajax();">
<div id="resText"></div>
```

```javascript
function Ajax() {
    var xmlHttpReq = null;
    if (window.ActiveXObject) {   //IE5 IE6 是以ActiveXObject方式引入XMLHTTPRequest对象
        xmlHttpReq = new ActiveXObject("Microsoft.XMLHTTP");
    } else if (window.XMLHttpRequest) {
        xmlHttpReq = new XMLHttpRequest();   //除IE5 IE6外的浏览器,XMLHttpRequest是window的子对象
    }
    if (xmlHttpReq != null) {
        xmlHttpReq.open("GET", "test.php", true);   //调用open()并采用异步方式
        xmlHttpReq.onreadystatechange = RequestCallBack;   //设置回调函数
        xmlHttpReq.send(null);   //使用get方法提交，使用null作为参数调用
    }
    
    function RequestCallBack() {   //一旦readyState值改变，会调用该函数
        if (xmlHttpReq.readyState == 4) {
            if (xmlHttpReq.status == 200) {
                //将xmlHttpReq.responseText的值赋予id为resText的元素                
                document.getElementById("resText").innerHTML = xmlHttpReq.responseText;
            }
        }
    }
}
```

##### 8.2 load()方法：通常用来获取server的静态数据文件

load data from the server and place the returned HTML into the matched elements.    

`load(url[, data][, callback])`

url: 包含请求HTML页面的URL地址的字符串

data: 发送至服务器的key/value数据，如果无参数传递，则采用GET方式传递；反之，则自动转换为POST方式。

callback: 请求完成时的回调函数:

```
function(responseText, textStatus, XMLHttpRequest){
   //responseText:   请求返回的内容
   //textStatus:   请求状态：success、error、notmodified、timeout 4种
   //XMLHttpRequest:   XMLHttpRequest对象   
});
```

load方法示例:

```javascript
$(function () {
    $("#send").click(function () {
        $("#resText").load("test.html");
        $("#resText").load("test.html .para");   //加载test.html页面中class为para的内容
        $("#resText").load("test.php",function(){
           ... 
        });   //无参数Get方式传递
        $("#resText").load("test.php",{name:"rain",age:"22"},
                          function(){
            ...
        });   //有参数Post方式传递
    });
});
```

##### 8.3 $.get()方法和$.post()方法  传递参数给服务器中的页面

$.get()方法：使用GET方式来进行异步请求，传输的数据有大小限制(一般不大于2KB)，参数跟在URL后面，数据缓存在浏览器中。

$.post()方法：http消息的实体内容发送给web服务器，数据量理论上不受限制，数据不会缓存在浏览器中

`$.get(url [,data] [,callback] [,type])`

url: 请求的HTML页的URL地址

data: 发送至服务器的key/value数据会作为QueryString附加到请求URL中callback: 载入成功时回调函数（只有当Response的返回状态是success才调用该方法） 自动将请求结果和状态传递给该方法：

callback的function(data,textStatus){ data返回的内容可以是xml,json,html等等,  textStatus;   请求状态：success、error、notmodified、timeout等等 };

type: 服务器返回内容的格式，包括xml、html、script、json、text和_default

$.get()方法示例：

```javascript
$(function(){
   $("#send").click(function(){
       $.get("get1.php", {
           username: $("#username").val(),
           content: $("#content").val()
       }, function(data, textStatus){
           $("#resText").html(data);   //将返回的数据添加到页面上
});
```

###### 8.3.1 如返回的数据格式是HTML片段：

直接调用，

```html
element.html(data);  
```

###### 8.3.2 如返回的数据格式是XML文档：

可使用常规的attr()、find()、filter()以及其他方法，

同时返回的数据需添加html代码块

同时，server端的data需将<header>设置为:

```html
<meta content="text/xml; charset=utf-8" />
```

###### 8.3.3 如返回的数据格式是Json文件：

返回的数据添加html代码块，同时type参数设为"json"

###### $.post()方法示例：

```javascript
$(function(){
   $("#send").click(function(){
       $.post("psot1.php", {
           username: $("#username").val(),
           content: $("#content").val()
       }, function(data, textStatus){
           $("#resText").append(data);   //将返回的数据添加到页面上
       });
   });
});
```

##### 8.4 $.getScript()方法和$.getJson()方法：动态加载文件

**动态加载js文件：**

javaScript动态加载js文件的方法：

```javascript
$(document.createElement("script")).attr("src","test.js").appendTo("head");
```

或者

```javascript
$("<script type='text/javascript' src='test.js'/>").appendTo("head");
```

jQuery动态加载js文件的方法示例：

```javascript
$("#send").click(function(){
   $.getScript('test.js'); 
});
```

**动态加载JSON文件的方法示例1：**

```javascript
$("#send").click(function(){
   $.getJSON('test.json',function(data){ // data: 返回的数据
       $('#resText').empty();
       var html = ' ';
       $.each(data, function(commentIndex, comment){
          html += '<div class="comment"><h6>'
           + comment['username'] + ":</h6><p class="para">"
           + comment['content'] + '</p></div>';
       });
       $('#resText').html(html);
   }); 
});
```

**动态加载JSON文件的方法示例2：**

jQuery将自动把URL里的回调函数，”url?callback=?“中的后一个”？“替换为函数名，以执行回调函数

```javascript
$("#send").click(function(){
   $.getJSON('http://url?callback=?',function(data){ // data: 返回的数据
       $.each(data.items, function(i, item){
           $("<img class='para'/>").attr("src", item.media.m).appendTo("#resText");
           if (i == 3){
               return false;
           }
       });
     });
   });
}); 
```

##### 8.5 $.ajax()方法，该方法是jQuery最底层的Ajax实现

结构为：$.ajax(options)，参数以key/vaue形式存在，参数解释：

url: 发送请求的地址

type: 请求方式（POST或GET）

timeout: 设置请求超时时间

data: 发送服务器的数据

**dataType: 预期服务器返回的数据类型**

dataType: (1) xml; (2) html; (3) script; (4) json; (5) jsonp(使用JSONP形式调用函数时，例如myurl?callback=?, jQuery将自动替换后一个“？”为正确的函数名，以执行回调函数)；(6) beforeSend(发送请求前可以修改XMLHttpRequest对象的函数，function(XMLHttpRequest){ this; //调用本次Ajax时传递的options参数})；(7) complete(请求完成后调用的回调函数, function(XMLHttpRequest, testStatus){ this; // 调用本次Ajax时传递的options参数 }); (8) success(请求成功后调用的回调函数，有两个参数 function(data, textStatus){ this; //调用本次Ajax时传递的options参数})； 

(9) error(请求失败时被调用的函数 function(XMLHttpRequest. textStatus, errorThrown) { this; //调用本次Ajax时传递的options参数 })；

(10) global(表示是否触发全局Ajax事件)

$.ajax()方法可代替$.load()、$.get()、$.post()、$.getScript()和 $.getJSON()

##### 8.6序列化元素 param()方法、serialize()方法和serializeArray()方法

param()方法，对一个数组或对象按照key/value进行序列化

```
var obj = {a:1,b:2,c:3};
var k = $.param(obj);   //k="a=1&b=2&c=3"
```

serialize()方法，能够将DOM元素内容序列化为字符串

serializeArray()方法，将DOM元素序列化返回JSON格式的数据

```html
<form id="form1" action="#">
    <p>Name: <input type="text name="username" id="username" /></p>
    <p>Content: <textarea name="content" id="content"></textarea></p>
</form>
```

```javascript
$("send").click(function(){
   $.get("get1.php",$("#form1").serialize(), function(data,textStatus){
      $("#resText").html(data);   //将返回的数据添加到页面上 
   });
});
```

代替：

```javascript
$("send").click(function(){
   $.get("get1.php",{
       username: $("#username").val(),
       content: $("#content").val()
   }, function(data,textStatus){
      $("#resText").html(data);   //将返回的数据添加到页面上 
   });
});
```

##### 8.7 Ajax全局事件

当Ajax请求开始时，会触发ajaxStart()方法的回调函数

当Ajax请求结束时，会触发ajaxStop()方法的回调函数

当Ajax请求完成时，ajaxComplete()

当Ajax请求发送错误时，ajaxError()

当Ajax请求发送前执行，ajaxSend()

当Ajax请求成功时执行，ajaxSuccess()

示例：

```javascript
$("#loading").ajaxStart(function(){
   $(this).show(); 
});
$("#loading").ajaxStop(function(){
   $(this).hide(); 
});
```

Ajax请求不触发全局方法：

```javascript
$.ajaxPrefilter(function(options){
   options.global = true; 
});
```



#### 9.jQuery插件的使用和写法：

##### 9.1 Validation插件使用示例：简化表单验证

html元素的class属性定义验证规则：例如required,email,url,minlength,date,number,digits等。

初始化：

```javascript
$("#commentForm").validate({
         ...      
});
```

自定义rule示例（避免在html 添加class属性）：

```javascript
$("#cusername").rules("add", {   //add rules for an element
    minlength: 2,
    required: true,
    messages: {
        required: "Required input",
        minlength: jQuery.validator.format("Please, at least ...")
    }
});

$("#cusername").rules("remove");   //remove rules for an element
```

自定义验证方式和示例：

jQuery.validator.addMethod(name,method[,message] );

method: 

value(current value of the validated element);

element(the element to be validated);

 params(parameters specified for the method);

```javascript
jQuery.validator.addMethod(   //自定义validation method
    "formula",                //自定义method name
    function (value, element, param) {
        return value == eval(param);
    },
    '请输入正确的数学公式计算结果'
);

$("#cvalcode").rules("add", {   //自定义rule
    "formula":"7+9"             //add param for the method
}); 
```

###### 9.1.1Validation插件使用示例：

```html
<script src="jquery-validation-1.19.1/lib/jquery.js"></script>
<script src="jquery-validation-1.19.1/dist/jquery.validate.js"></script>
<script type="text/javascript">
    $(document).ready(function () {
            $("#commentForm").validate({
                cusername: {
                    required: true,
                    //using the normalizer to trim the value of the element
                    normalizer: function (value) {
                        return $.trim(value);
                    }
                }
            });
        });
</script>
```

```html
<form class="cmxform" id="commentForm" method="get" action="#">
    <fieldset>
        <legend>一个简单的验证带验证提示的评论例子</legend>
        <p>
            <label for="cusername">Name</label><em>*</em>
            <input id="cusername" name="username"
                       size="25" class="required" minlength="2" />
        </p>
        <p>
            <label for="cemail">Email</label><em>*</em>
            <input id="cemail" name="email"
                       size="25" class="required email" />
        </p>
        <p>
            <label for="curl">Website</label><em>&nbsp;</em>
            <input id="curl" name="url"
                       size="25" class="url" value="" />    
        </p>
        <p> 
            <label for="ccomment">Your Comment</label><em>*</em>
            <textarea id="ccomment" name="comment"
                          cols="22" class="required">
            </textarea>
        </p>
        <p>
            <input class="submit" type="submit" value="Submit"/>
        </p>
    </fieldset>
</form>
```

##### 9.2 Form表单插件：将html表单升级为Ajax提交方式

Form有两个核心方法：ajaxForm()和ajaxSubmit(), 和其他一些方法：formToArray(), formSerialize()，fieldSerialize(), fieldValue(), clearForm(), clearFields()和 resetForm()等。

ajaxForm()，将表单升级为Ajax提交方式：

```javascript
$('#myForm').ajaxForm(function(){
    $('#output1').html("提交成功").show();
});
```

ajaxSubmit(), 响应用户的提交表单操作：

```javascript
$('#myForm').submit(function(){
    $(this).ajaxSubmit(function(){
       $('#output1').html("提交成功").show();
    });
    return false;   //阻止表单默认提交
})
```

```javascript
var options = {
  target: '#output1',   //把服务器返回的内容放入id为output1的元素中
    beforeSubmit: showRequest,   //提交前的回调函数
    success: showResponse   //提交后的回调函数
  url: url,   //默认是form的action
  type: type,   //默认是form的method
  dataType: null,   //'xml','script','json'接受服务端返回的类型
  clearForm: true,   //成功提交后，清除表单元素的值
  resetForm: true,   //成功提交后，重置表单元素的值
  timeout: 3000   //限制请求的时间
};
```

```javascript
//beforeSubmit 提交前的回调函数
function showRequest(formData,jqForm,options){
    var queryString = $.param(formData);
    return true;
}
//第一个参数formData 数组对象，$.param()方法把它转化为字符串  //“param=value&param1=value1...”
//第二个参数jqForm 封装了表单的元素，把jqForm转换为DOM对象
//var formElement = jqForm[0];
//var address = formElement.address.value;
//第三个参数options 即options对象
```

```javascript
//success 提交后的回调函数
function showResponse(responseText, statusText, xhr, $form){
    alert('状态：' + statusText + '\n 返回的内容是：\n' + responseText);
}
//第一个参数responseText 携带服务器返回的数据内容，会根据设置的options对象中的dataType属性返回相应格式的内容。1.对于缺省的HTML返回，回调函数的第一个参数是XMLHttpRequest对象的responseText属性。2.当dataType属性设置为xml时，回调函数的第一个参数是XMLHttprequest对象的responseXML属性。3.当dataType属性设置为json时，回调函数的第一个参数是从服务器返回的json数据对象
$('#xmlForm').ajaxForm({
    dataType:'xml',
    success: processXml
});
function processXml(responseXML){
    var name = $('name',responseXML).text();
    var address = #('address', responseXML).text();
    $('#xmlOut').html(name + " " + address);
}
$('#myForm').ajaxForm({
    dataType: 'json', 
    success: processJson
});
function processJson(data){
    $('jsonOut').html(data.name + " " + data.address);
}
```

##### 9.2.1 Form插件验证实例

首先定义validate回调函数，设置beforeSubmit的值：

```javascript
var options = {
  target: '#output1',   //把服务器返回的内容放入id为output1的元素中
    beforeSubmit: validate,   //提交前的回调函数
    success: showResponse   //提交后的回调函数
  url: url,   //默认是form的action
  type: type,   //默认是form的method
  dataType: null,   //'xml','script','json'接受服务端返回的类型
  clearForm: true,   //成功提交后，清除表单元素的值
  resetForm: true,   //成功提交后，重置表单元素的值
  timeout: 3000   //限制请求的时间
};

方式1：利用参数formData
function validate(formData,jqForm,options){
    for(var i=0;i<formData.length;i++){
        if(!formData[i].value){
            alert('用户名，地址不为空');
            return false;
        }
    }
    var queryString = $.param(formData);
    return true;
}
方式2：利用参数jqForm
function validate(formData,jqForm,options){
    var form = jqForm[0];
    if(!form.name.value || !form.address.value){
        alert('用户，地址不为空');
        return false;
    }
    var queryString = $.param(formData);
    return true;
}
方法3：利用fieldValue()方法
function validate(formData,jqForm,oprions){
    var usernameValue = $('input[name=name]').fieldValue();
    var addressValue = $('input[name=address]').fieldValue();
    if(!usernameValue[0] || !addressValue[0]){
        alert('用户，地址不为空');
        return false;
    }
    var queryString = $.param(formData);
    return true;
}
```

##### 9.3 jQuery UI插件sortable()方法运用：

```javascript
$(element.id).sortable();   //可以拖动在列表或框架内的元素排序
$(element.id).sortable('serialize');   //直接获取元素排列顺序
```

##### 9.4jQuery自定义插件

###### 插件种类：

封装对象方法的插件(将对象方法封装起来，用于对通过选择器获取的jQuery对象进行操作), 该方法使用jQuery.fn.extend()方法；

封装全局函数的插件(可以将独立的函数加到jQuery命名空间下)，该方法使用jQuery.extend()方法；

选择器插件，该方法使用jQuery.extend()方法，这两个方法接受一个参数，类型为Object。Object对象的“名/值对”分别代表“函数或方法名”,选择器函数一共接受3个参数:

```javascript
function(a,i,m){
    // ...
}
第一个参数为a,指向的是当前遍历到的DOM元素
第二个参数为i,指的是当前遍历到的DOM元素的索引值，从0开始
第三个参数为m,是一个数组。
以$("div :l(ss(dd))")为例：
m[0]是:l(ss(dd))这部分
m[1]是选择器的引导符，匹配“：”
m[2]是l
m[3]是ss(dd)
m[4]是(dd)
```

###### 自定义插件要点：

文件名推荐命名为jquery.[pluginName].js;

在插件内部，this指向的是当前通过选择器获取的jQuery对象，内部的this指向的是DOM元素；

可以通过this.each遍历所有元素；

所有的方法或函数插件，都以分号结尾，否则压缩可能出现问题；

插件应该返回一个jQuery对象，以保证插件的可链式操作，除非插件需要返回的是一些获取的量；

避免使用$作为jQuery对象的别名，但可以使用闭包来回避；

自定义插件需考虑如下因素：插件灵活性，插件大小，插件性能；

###### 插件中的闭包格式：

```javascript
;(function($){
    $.fn.extend{
        ""+functionName1:function(value){
            //plugin code
        },
        ""+functionName2:function(value){
            //plugin code
        },
    });
})(jQuery);
```

###### 自定义插件-封装对象方法示例：

给这个方法提供一个参数value,如果调用方法的时候传递了value这个参数，就用这个值来设置字体颜色；否则就是获取该匹配元素的字体颜色的值。

```javascript
;(function($){
    $.fn.extend({
       "color":function(value){
           return this.css("color",value);
       } 
    });
})(jQuery);
```

###### 自定义插件-封装对象方法和选择器插件方法示例：

给封装对象方法提供参数options,为该参数options提供选择器插件，

```javascript
;(function($){
    $.fn.extend({
        "alterBgColor":function(options){
            options = $.extend({
                odd:"odd",
                even:"even",
                selected:"selected"
            },options);
        }
    });
})(jQuery);
```

注：匹配元素的对象$(element.id)改写成$(element.id, this),表示在匹配的元素内查找

###### 自定义插件-封装全局函数方法示例：

```javascript
;(function($){
    $.extend({
        ltrim:function(text){
          return (text || "").replace(/^\s+/g,"");  
        },
        rtrim:function(text){
            return (text || "").replace(/\s+$/g,"");
        }
    });
})(jQuery);
```

###### 自定义插件-自定义选择器方法示例：

```javascript
<script type="text/javascript">
    ;(function($){
        $.extend(jQuery.expr[":"],{
           between: function(a,i,m){
               var tmp=m[3].split(",");   //逗号分隔为数组
               return tmp[0]-()<i&&tmp[1]-{};
           }
        });
    })(jQuery);
    //plugin application
    $(function(){
     $("div:between(2,5)").css("background","white");
    })   //此时m[3]值为“2，5”
</script>
```



#### 10.jQuery Mobile的使用

307