# jQuery中的事件和动画

## jQuery中的事件

自定义事件见5.1.7

### 加载DOM

```javascript
$().ready(function(){
   //编写代码
})
```

### 事件绑定

```javascript
element.bind(eventType,event.data,function);
element.bind(eventType, function).bind(eventType,function);
```

eventType: blur, focus, load, resize, scroll, unload, click, dbclick, mousedown, mouseup, mousemove, mouseover, mouseout, mouseenter, mouseleave, change, select, submit, keydown, keypress, keyup和error等

### 事件触发

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

### 事件触发示例：

hover()方法

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

### 移除事件

```javascript
element.unbind(event.type, function);   //解除绑定
```

```javascript
element.one(event.type, function);   //只触发一次
```

### 事件命空间

可为eventType添加命名空间eventType.namespace, 之后解绑定时可直接使用

```
element.unbind(".namespace")；
```

当只触发不包含在命名空间中的eventType时，可以使用

element.trigger("eventType!");   //作用是匹配所有不包含在命名空间的方法

### 事件冒泡

多层元素内嵌时，触发事件将按照DOM的层次结构由内向外响应。

event.stopPropagation()将阻止事件的冒泡

### 事件对象的属性

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

