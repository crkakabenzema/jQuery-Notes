# jQuery与Ajax的应用

Ajax的核心是XMLHttpRequest对象，通过它来完成异步请求、接受响应及执行回调。

##  JavaScript的Ajax应用示例

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

## load()方法获取server的静态数据文件

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

## $.get()方法和$.post()方法  传递参数给服务器中的页面

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

### 如返回的数据格式是HTML片段：

直接调用，

```html
element.html(data);  
```

### 如返回的数据格式是XML文档：

可使用常规的attr()、find()、filter()以及其他方法，

同时返回的数据需添加html代码块

同时，server端的data需将<header>设置为:

```html
<meta content="text/xml; charset=utf-8" />
```

### 如返回的数据格式是Json文件：

返回的数据添加html代码块，同时type参数设为"json"

$.post()方法示例：

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

###  $.getScript()方法和$.getJson()方法：动态加载文件

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

###  $.ajax()方法--jQuery最底层的Ajax实现

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

序列化元素 param()方法、serialize()方法和serializeArray()方法

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

### Ajax全局事件

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

