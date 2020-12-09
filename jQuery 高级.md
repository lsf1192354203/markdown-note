

# jQuery 高级

### jQuery中的运动

```js
/*
animate()
第一个参数：{}运动的值和属性
第二个参数：时间（）运动的快慢 默认：400
第三个参数：运动形式（swing linear）只有两种--------------时间版运动。
第四个参数：回调函数
*/
/*
stop()默认：只会阻止当前运动,后续运动继续，
stop(true)----阻止后续所有运动
stop(true，true)----可以立即停止到指定的目标点，后续运动阻止。finish()------可以立即停止到所有指定的目标点
*/
//delay()延迟


```
**animate参数**
```js
$('#div1').animate({
			num : "move"
		},{
			duration : 2000,
			easing : 'linear',
			complete : function(){
				//alert(123);
			},
			step : function(a,b){  //可以检测我们定时器的每一次变化
				//console.log(a);
				//console.log(b.pos);   //运动过程中的比例值(0~1)
				$('#div1').html(parseInt(b.pos * 273826678));
			}
		});
```


```js
$('#input1').click(function(){
		
		//$('#div1').animate({width : 300},1000);
		//$('#div1').animate({height : 300},1000);
		//$('#div1').animate({left : 300},1000);
		
		//alert(123);相当于链式操作
		
		$('#div1').animate({width : 300},1000).delay(1000).animate({height : 300},1000);
		
	});
```



*****

### jQuery事件操作

```html
<div id="div1">
    aaaaa
</div>
```

**ev.data  ev.target  ev.type**

```js
//利用0n方法
$("li").on("click",function(){
    this.style.background="red";
})
//利用事件委托 一：省去for循环 二：后续增加的li自动增加点击行为
$("ul").delegate("li","click",function(){
    this.style.background="red";
    $("ul").undelegate();
})
//undelegate()阻止事件委托

//trigger()主动触发--------对自定义事件用的较多
$(function(){
    $("#div1").on("click",function(){
        alert(123);
    });
    $("#div1").trigger("click");//一打开页面就会触发div的click事件；
    $("#div1").on("show",function(){
        alert(123456);
    });
    $("#div1").on("show",function(){
        alert('qqq');
    });
    $("#div1").trigger("show");//123456 qqq
})

//ev.data  ev.target  ev.type
$("#div1").on("click",{name:"hello"},function(ev){
    alert(ev.data.name);//hello
});
$("#div1").on("click",function(ev){
    alert(ev.target);//[object HTMLDivElement]
});
$("#div1").on("click",function(ev){
    alert(ev.type);//click
});
```



+++++

### jQuery的工具方法

##### $下的常用方法------<font color=red>$.type()、$.trim()、$.inArray()、$.proxy()</font>

```js
//以前使用的方法：$().css()、 $().html()、$().val()、$().size()  ------只能给JQ对象用
//$.xxx()   $.yyy()   $.zzz():不仅可以给JQ用，也可以给原生JS用。-------叫做工具方法
$(function(){
    var a = "hello";
    alert(typeof a)//原生判断类型
    //$.type():也是判断类型
    alert($.type(a));
    //区别：$.type()可以明确判断多种类型：eg:string 数组、{} {} null new Date  RegExp 
})

//$.trim()
var str ="  hello  ";
alert('('+str+')');//(  hello  )
//原生js中是string方法,不会改变原始字符串
alert(str.trim())//hello
//$.trim()
alert('('+$.trim(str)+')');//hello
//原生js中string.indexOf（searchvalue,start）------返回某个指定的字符串值在字符串中首次出现的位置
//$.inArray()----类似于indexOf
var arr=['a','b','c']
alert($.inArray('b',arr));//1 -----如果没有就是-1
//proxy():改变this指向的
function show(){
    alert(this)
}
show()//window
$.proxy(show,document)();//document
//////////////////////////////////
function show(n1,n2){
    alert(n1);
    alert(n2);
    alert(this);
}
$.proxy(show,document)(3,4);//document
或者
$.proxy(show,document，3,4)();//document
或者
$.proxy(show,document，3)(4);//document
////////////////////例子
$(document).click(show);
$(document).click($.proxy(show,window,3,4));
//
```

#### jQuery实用工具

$.isFunction()	$.isNumeirc()	$.isArray()	$.isWindow()	 $.isEmptyObject()	$.isPlainObject()

-----

### jQuery的工具方法和ajax

#### $  &jQuery

```js
//$与jQuery是相同的好比一个是大名一个是小名
//防止冲突--------noConflict():
var miaov = $.noConflict();
var $=10;
miaov(function(){
    alert($);
})
```

#### parseJSON

```js
//把字符串解析成json
var str='{"name":"hello"}';
alert($.parseJSON(str).name);
```

#### makeArray()

```js
//类数组转真正数组
window.onload=function(){
    var aDiv=document.getElementByTagName("div");
    $.makeArray(aDiv).push();
}
```

#### $.ajax():json形式的配置参数

```js
/*
url:success
error:contentType
data:type
dataType:cache timeout
*/
$.ajax({
    url:"xxx.php",
    data:'name=hello&age=20',
    type:'POST',
    success:function(data){
        alert(1)
    },
    error:function(data){
        alert(2)
    }
})

$.get('xxx.php?name="leo"',function(){
    
})
$.get('xxx.php',{name:"hello"},function(){
    
})
$.post('xxx.php',function(){
    
})
//getJSON()----支持jsonp的形式：指定？callback=?
$.post('xxx.php?callback=show',function(data){
    
})
show({})
```

<font color=red>注意区别：</font>$.get()与$().get()

____

### jQuery的插件操作

$

​	-$.extend:扩展的是工具方法下的插件形式    $.xxx()  $.yyy()

$.fn：扩展到jQ对象下的插件形式  $().xxx()  $().yyy()

​	-$.fn.extend

```js
//$.trim()
//$.leftTrim()
$.extend({
    leftTrim:function(str){
        return str.replace(/^\s+/,"");
    },
    rightTrim:function(){
        return str.replace(/$\s+/,"");
    },
    aaa:function(){}
})
var str='  hello  ';
alert($.leftTrim(str));
$("#div1").drag();
$.fn.extend(){
    drag:function(){
        //this----调用前面的元素----$("#div1")
        var disX=0;
        var disY=0;
        
        var This=this;
        
        this.mousedown(function(ev){
            
            disX=ev.pageX-$(this).offset().left;
            disY=ev.pageY-$(this).offset().top;
            
            $(document).mousemove(function(ev){
                This.css("left",ev.pageX-disX);
                This.css("top",ev.pageY-disY);
            });
            
            $(document).mouseup(function(ev){
                $(this).off();
            });
            return false;
            
        })
    },
        aaa:function(){
            alert(2)
        }
}

```

