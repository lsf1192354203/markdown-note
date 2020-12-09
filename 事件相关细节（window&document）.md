## <font color=blue>事件相关细节&</font>位置操作

### Window与Document对象

```js
$(function(){
      $(document).click(function(event) {
        alert($(window).scrollTop());
        //window：它是一个顶层对象，即浏览器窗口，window对象表示浏览器中打开的窗口。
        /*
        当浏览器载入HTML文档，它就会成为Document对象
        document指页面。document是window的一个子对象。
        document对象是HTML文档的根节点，
        Document对象使我们可以从脚本中对html页面中的所有元素进行访问。
        */
        //document对象是window对象的一部分，
        /*
        用户不能改变document.location(因为这是当前显示文档的位置)。
        但是可以改变window.location（用其他文档取代当前文档）
        window.location本身也是一个对象，
        而document.loaction不是对象
        */
      });
    })
```

#### 编写弹窗

```html
<body>
    <input type="button" value="点击">
    <div id="login"style="position:absolute;width:300px;height:300px;top:50px;">
        <input type="text" value="用户名">
        <input type="password" value="密码">
        <span id="close">X</span>
    </div>
</body>
```



```js
//创建元素
$("<div>")
//选择元素
$("div")
$(function(){
    var oDiv=$("<div>");//var oDiv=$("<div>html-div</div>")
    $("body").append(oDiv);
})
```

##### width属性

```js
alert( $('div').width() );  //width
	
alert( $('div').innerWidth() );  //width + padding

alert( $('div').outerWidth() );  //width + padding + border

alert( $('div').outerWidth(true) );  //width + padding + border + margin
```

### 事件相关细节

```js
$("div").click(function(ev){
    //ev:event对象相当于原生的 ev=ev||window.event;
    //ev.pageX(相对于文档):clientX(相对于可视区)  即：ev.pageX=clientX+滚动条距离
    //ev.which:keyCode---键盘的键值
    //ev.preventDefault()://阻止默认事件
    //ev.stopPropagation();//阻止冒泡的操作
    return false;//阻止默认事件+阻止冒泡的操作
    //on类似于one，区别是只触发一次
    $("div").one("click",function(){
        alert(123);
    })
})
```

### 位置操作.offset().left/position().left

```js
//原生的offsetLeft 是针对父级或最近有相对定位元素的距离：（position:relative）
//jq:$("#div2").offset().left;//获取的是距离屏幕的左距离。
//$("#div2").position().left;//将div2看做一个有定位的元素了，他这个定位也是到有定位的父级，margin不包含在内，（到有定位的父级的left值,把当前元素转为类似定位的形式）
//若Div2：position：absolute；left：25px ,则：$("#div2").position().left的值为25；
```

### offsetParent

```html
<body>
    <div id="div1">
        <div id="div2"</div>
    </div>
</body>
```



```js
//parent():获取父级-------同原生的parentNode
//offsetParent():获取有定位的父级  ------同原生的offsetParent
$(function(){
    $("#div2").parent().css("background","blue");//div1有无定位都是div2的parent。
    /*
    如果div1有定位则是div1背景色为蓝色
    如果div1无定位仍然是div1背景色为蓝色
    */
    $("#div2").offsetParent().css("background","red");
    /*
    如果div1有定位则是div1背景色为红色
    如果div1无定位则是body背景色为红色
    */
})
```

### val()&size()&each()

```js
$("input").val();//取值
$("input").val('aaa');//设置值
$("li").size()//像length
//原生的for循环加强版-------each()
$("li").each( function(i,elem){//一参：下标索引  二参：每个元素
    $(elem).html(i);
} )
```

