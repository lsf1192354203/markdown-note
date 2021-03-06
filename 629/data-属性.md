### data-*属性

下面就详细介绍四种方法获取`data-*`属性的值

```
<li id="getId" data-id="122" data-vice-id="11">获取id</li>
```

需要获取的就是`data-id` 和 `dtat-vice-id`的值

------

一：getAttribute()方法

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
const getId = document.getElementById('getId');
// //getAttribute()取值属性
console.log(getId.getAttribute("data-id"));//122
console.log(getId.getAttribute("data-vice-id"));//11
// //setAttribute()赋值属性
getId.setAttribute("data-id","48");
console.log(getId.getAttribute("data-id"));//48
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

二：dataset()方法

 

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
//data-前缀属性可以在JS中通过dataset取值，更加方便
console.log(getId.dataset.id);//112
//data-vice-id连接取值使用驼峰命名法取值 
console.log(getId.dataset.viceId);//11

//赋值
getId.dataset.id = "113";//113
getId.dataset.viceId--;//10

//新增data属性
getId.dataset.id2 = "100";//100

//删除，设置成null，或者delete
getId.dataset.id2 = null;//null
delete getId.dataset.id2;//undefind
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

三：jquery data()方法

```
var id = $("#getId").data("id"); //122
var viceId = $("#getId").data("vice-id"); //11
//赋值
$("#getId").data("id","100");//100
```

 

jquery data 是一种缓存机制

用法如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
data()方法

//HTML代码 <div id="myDiv" data-appid="123" data-myname="lsxj" data-app-id="456" data-my-name="secondname"></div>

//获取属性
var appid = $("#myDiv").data("appid"); //123
var app-id = $("#myDiv").data("app-id"); //456

//属性赋值 $("#myDiv").data("appid","666");

//最终HTML代码 <div id="myDiv" data-appid="123" data-myname="lsxj" data-app-id="456" data-my-name="secondname"></div>

需要注意的是，data()的值进行修改并不会影响到DOM元素上的data-*属性的改变。data()的本质其实是将一个 “cache” 附加到了对象上，并使用了一个特殊的属性名称。

所以上述代码中，虽然对div进行了data()赋值操作，但HTML代码中div的data-appid的值仍然为123，因为data()只是修改了缓存的那个值，此时进行$('#myDiv').data("appid")的操作，输出的结果为666.
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

四：jquery attr()方法

```
var id = $("#getId").attr("data-id"); //122
var viceId = $("#getId").attr("data-vice-id"); //11
//赋值
$("#getId").attr("data-id","100");//100
```

