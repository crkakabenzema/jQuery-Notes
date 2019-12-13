# jQuery对表单、表格的操作及应用

## 表单组成部分

表单标签：包含处理表单数据的服务端程序URL和数据提交到服务器的方法；

表单域：包含文本框、密码框、单选复选框等；

表单按钮：包含提交按钮、复位按钮和一般按钮

## 表单应用

jQuery通过attr()访问对象的属性

### 单行文本框应用示例：

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

### 多行文本框应用示例：

文本框高度属性：height; 文本框滚动条属性：scrollTop；

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

### 复选框应用示例：

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

### 下拉框应用示例：

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

### 表单验证示例：

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

### 表格高亮和展开/关闭示例：

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

### 表格内容筛选示例：

```javascript
$("#confirm").click(function () {
    $("table tbody tr").hide()
        .filter(":contains('" + ($("#filterName").val()) + "')").show();
}); 
```

### 网页选项卡示例：

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


