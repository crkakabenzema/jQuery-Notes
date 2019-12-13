# jQuery插件的使用和写法

## Validation插件--简化表单验证

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

Validation插件使用示例：

```
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

## Form表单插件--将html表单升级为Ajax提交方式

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

Form插件验证实例

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

## jQuery UI插件

sortable()方法运用

```
$(element.id).sortable();   //可以拖动在列表或框架内的元素排序
$(element.id).sortable('serialize');   //直接获取元素排列顺序
```

## jQuery自定义插件

### 插件种类：

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

### 自定义插件要点：

文件名推荐命名为jquery.[pluginName].js;

在插件内部，this指向的是当前通过选择器获取的jQuery对象，内部的this指向的是DOM元素；

可以通过this.each遍历所有元素；

所有的方法或函数插件，都以分号结尾，否则压缩可能出现问题；

插件应该返回一个jQuery对象，以保证插件的可链式操作，除非插件需要返回的是一些获取的量；

避免使用$作为jQuery对象的别名，但可以使用闭包来回避；

自定义插件需考虑如下因素：插件灵活性，插件大小，插件性能；

插件中的闭包格式：

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

自定义插件-封装对象方法示例：

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

自定义插件-封装对象方法和选择器插件方法示例：

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

自定义插件-封装全局函数方法示例：

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

自定义插件-自定义选择器方法示例：

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

