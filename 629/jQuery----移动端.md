### jQuery----移动端

**事件扩展**

<font color=red>foucus事件----和blur事件</font>

```js
//focus与blur不支持冒泡
//focusin()与focusout支持冒泡
//one 事件只能触发一次。或者用off（）；
```

**阻止默认行为拖拽**

```js
$('#div').mousedown(function(){
    return false;
})
```



**touchstart**------------------>originalEvent.changedTouches

**获取原生event**

* originalEvent---------原生event对象
* changedTouches

```js
$('#div1').on('touchstart',function(ev){
		
		alert(ev.originalEvent.changedTouches);
		alert(ev.originalEvent.changedTouches)
		
		
	});
```

**zoomIn**

```js
$('#img1').on('zoomIn',function(){  //缩小
		
		$(this).css('width',200);
		
	});
	
	$('#img1').on('zoomOut',function(){  //放大
		
		$(this).css('width',700);
		
	});
	
	$('#img1').on('DOMMouseScroll',function(ev){
		
		if(ev.originalEvent.detail > 0){
			$(this).trigger('zoomIn');
		}
		else{
			$(this).trigger('zoomOut');
		}
		
	});
```

**自定义事件**--------在原有的事件的基础上进行了二次封装，它真正的其实还是调用我们系统事件

滚轮监听事件---------鼠标滚轮可以触发他《**DOMMouseScroll**》

**关于鼠标滚轮的属性**---------》ev.detail

鼠标滚动缩放

```js
$('#img1').on('zoomIn',function(){  //缩小
		
		$(this).css('width',200);
		
	});
	
	$('#img1').on('zoomOut',function(){  //放大
		
		$(this).css('width',700);
		
	});

$('#img1').on('DOMMouseScroll',function(ev){
		
		if(ev.originalEvent.detail > 0){
			$(this).trigger('zoomIn');
		}
		else{
			$(this).trigger('zoomOut');
		}
		
	});
```

**triggerhandler**-----不会获取焦点，不会触发默认的事件行为，相当于自定义事件

**trigger**------会自动获取焦点-----主动触发事件的默认行为

#### ev.stopPropagation 与ev.stopImmediatePropagation的区别

 ev.stopPropagation ------------------只会阻止父级

ev.stopImmediatePropagation-----------不仅阻止父级，还阻止自身

**ready()**

```js
$('img').load(function(){
    alert($('img').width())
})
```

**数据缓存**

* 缓存大量数据用data()
* 自定义属性用attr（）

```js
//data();----------类似于attr
$('#div1').data('name','hello')
/*
{name:hello}
设置缓存数据-----并不是真正往元素身上添加
把数据存到了一个大的集合中：作用，通过间接方式可找到。防止内存泄漏
*/
$('#div1').attr('name','hello')//属性：属性值，往元素本身上添加属性，自带属性
alert($('#div1').attr('name'))
//prop()
```

**prop与attr区别**

attr：通过原生的setAttribute()添加的，获取通过getAttribute方式

prop：通过. 或者[]的方式------------oDiv[index]=i;

```js
//全选
aInput[0].onclick= function(){
    for(var i=0;i<aInput.length;i++){
        aInput[i].checked=true;
    }
}

var bBtn=true;
$('input[type=button]').click(function(){
    if(bBtn){
       $('input[type=checkbox]').attr('checked',true) 
    }else{
       $('input[type=checkbox]').attr('checked',false)
    }
    
    bBtn=!bBtn;
})

$('input[type=button]').click(function(){
    if(bBtn){
       $('input[type=checkbox]').prop('checked',true) 
    }else{
       $('input[type=checkbox]').prop('checked',false)
    }
    
    bBtn=!bBtn;
})
```

**removeAttr() / removeProp() / removeData()**

**回调函数**

```js
$('div').addClass(function(i,oldClass){//i代表索引，oldClass代表旧的类名
    console.log(i);
    console.log(oldClass);
    return 'box'+(i+1);
})
```

**支持回调形式的设置**

```js
addClass()
html()
val()
```

**JQ中的回调对象**

```js
$.Callbacks()
var cb=$.Callbacks();//统一管理对象
//有以下几个方法
cb.add(a)//将a添加到集合
cb.add(b)
cb.fire()//触发这个集合
cb.add(c)//不会触发，执行有一定的顺序
cb.fire()
cb.remove(a)//删除集合里a

```

**JQ中的回调对象Callbacks()的四大参数**

* once
* memory
* unique
* stopOnFalse
* 延迟$.deferred对象

```js
var cb=$.Callbacks('once');
cb.add(a)
cb.add(b)
cb.fire()
var cb=$.Callbacks('memory');
cb.add(c)
var cb=$.Callbacks('unique');
cb.add(a)
cb.add(a)
cb.fire()
var cb=$.Callbacks('stopOnFalse');
function a(){
    alert('a')
    return false;
}
cb.add(a)
cb.add(b)
cb.fire()
var cb=$.Callbacks('once memory');

```

**jQ当中的延迟对象------（也是一种工具方法）**来操作异步的，（定时器、ajax）

```js
setTimeout(function(){
    alert(1)
},1000)
alert(2)//结果  2   1
//如果想先执行1 后执行2 
var cb= $.Callbacks();
setTimeout(function(){
    alert(1);
    cb.fire()
},100)
cb.add(function(){
    alert(2)
})
alert(3)
```

**$.Deferred()**

```js
var dfd= $.Deferred();
setTimeout(function(){
    alert(1);
    dfd.resolve()
},100)
dfd.done(function(){
    alert(2)
})
```

* 状态-----------resolve()    done()            reject()    fail()

```js
$.ajax('xx.php').done(function(){}).fail(function(){})
```

```js
var bBtn=true;
$('input').click(function(){
    if(bBtn){
        bBtn=false;
        setTimeout(function(){
            alert(1)
        },2000)
    }else{
        alert(1);
    }
})
//改进。
var dfd=$.Deferred()
$('input').click(function(){
    setTimeout(function(){
        dfd.resolve(a)//状态会保持住
    },2000)
    dfd.done(a)    
    
})
function a (){
    alert(1);
}

```

**ajax中的应用----When**

```js
$.ajax('xx.php').done(function(){})
$.ajax('yy.php').done(function(){})
//当xx.php和yy.php 都执行完了
$.when( $.ajax('xx.php') ,$.ajax('yy.php') ).done(function(){});
```

**JQ的源码架构**

<font color=red>函数也是对象，函数下面也可以带方法</font>

