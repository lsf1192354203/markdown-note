### jq高级

##### 一、基础方法扩充

* get（）：下标和length属性
```js
$(function(){
	$("#div1").get(0).innerHTML//$("li").get()就相当于原生的一组li
})
```
* outerWidth（）：针对隐藏元素和参数true
```js 
//原生js offsetWidth:是获取不到隐藏元素的值的
alert($("#div1").get(0).offsetWidth);
alert($("#div1").outerWidth());
```

* text():合体的特例
```js 
$("div").text();//只会获取所有一组标签的文本内容，不会读取标签元素
```
* remove():detach()
```js 
//原生js:removeChild移除节点
$("div").click(function(){
alert("123")
})
var remChild= $("div").remove();//删除的返回值就是删除的节点元素
$("body").append(remChild);//页面上面虽然添加了删除的元素，但是点击事件没了
var remChild= $("div").detach()
//detach():与remove（）的区别就是：保留了删除的事件；
$("div").text();//只会获取所有一组标签的文本内容，不会读取标签元素
```
* $():$(document).ready()
```js 
//原生window.onload=function(){}//等页面加载完了在加载
$(function(){
//等DOM加载完成就可以了，性能要好
})
```
## DOMContentLoaded

### <font color=red>jQuery 的DOM操作</font>

```html
<body class="cont">
    <div id="box cont">
        <div id="div1 cont">
            内容一一一
        </div>
    </div>
</body>
```



```js
//parents():获取当前元素的所有祖先节点，参数就是筛选功能
$("#div1").parents('body').css("background","red");//父级body
//closest():获取最近的指定的祖先节点（包括当前元素自身）必须要写筛选的参数，只能找到一个元素
$("#div1").closest(".cont").css("background","red");
//siblings:获取所有的兄弟节点----（不含本身），可以写参数筛选。
//nextAll():下面所有的兄弟节点
//prevAll():上面所有的兄弟节点
//nextUntil():截止-----prevUntil() ----parentsUntil();
$("span").nextUntil('h2').css("background","red");
/*
clone():克隆节点-----可以接受参数  clone（true），作用是可以复制操作行为
appendTo append 都是剪切操作
*/
$("div").clone().appendTo($('span'));

```

```html
<span>2</span>
<span>2</span>
<span>2</span>
```

```js
/*
wrap()、单个包装
wrapAll()、整体包装
wrapInner()、内部包装
unwrap()删除包装，（删除父级，不包括body）
*/
$("span").wrap("<div>");//每个span都被一个div包裹
```
```html
<span>2</span>
<div>div</div>
<ul>
    <li>22</li>
    <li>22</li>
    <li>22</li>
    <li>22</li>
</ul>
```

```js
/*
add() slice（arg1,arg2）------一参是起始位置 二参是：结束位置（不包含）
*/
var elem = $("div");
var elem2 =elem.add("span");
elem.css("color","red");
elem2.css("background","blue");

$("li").slice(1,4).css("background","blue");//选取的意思
```

```js
//serialize() serializeArray()------数据串联化
/*
<form>
<input type ="text" name="a" value="1">
<input type ="text" name="b" value="2">
<input type ="text" name="c" value="3">
</form
*/
$("form").serialize();//string:a=1&b=2&c=3;
$("form").serializeArray();//Array:每一项是json
/*
[
{name:"a",value:"1"},
{name:"b",value:"2"},
{name:"c",value:"3"}
]
*/
```

