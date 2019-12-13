# jQuery操作网页样式示例

## 修改字体大小

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

















































