### Vquery

一个小型的jquery库

**学习Vquery具备的知识**

* jquery
* 面向对象
* 常用方法：bindEvent.getByClass

```js
//选择元素
$('#div1')	$(function(){})	$('li')	$(window)

$('#div1').html('hello');
$().html()------>对象
//对象.css();
$()-------->类似函数调用
var arr=[];
arr.push();
arr.sort();
///////////////////////////
function Vquery(){}//构造函数
function $(vArg){return new Vquery();}
function $(vArg){return 对象;}
///////////////////////////
function Vquery(vArg){}//构造函数--传参
function $(vArg){return new Vquery(vArg);}
///////////////////////////对象的方法
Vquery.prototype.css=function(){}
Vquery.prototype.html=function(){
    for(var i=0;i<this.elements.length;i++){
        this.elements[i].innerHTML='aaa';
    }
}

```
<font color=red>面向对象当中，在不同的方法当中，能找到共用的属性和变量，这个变量必须是对象下的属性，因为属性和方法才是共享的，</font>

**getByClass(oParent,sClass)**

```js
function getByClass(oParent,sClass){
    var arr=[];
    var elems=oParent.getElementsByTagName('*')
    
    for(var i=0;i<elems.length;i++){
        if(elems[i].className==sClass){
            arr.push(elems[i]);
        }
    }
}
```

**转数组**

```js
function toArray(elems){
    var arr  =[];
    for(var i=0;i<elems.length;i++){
        arr.push(elems[i]);
    }
    return arr;
}
```



```js
function Vjquery(arg){
    this.elements = [];//选择元素的这样一个集合
    
    switch (typeof arg){
        case 'function'  :
            window.onload=arg;
            break;
        case 'string':
            switch(arg.charAt(0)){
                case '#'://id
                   var oDiv=document.getElementById(arg.substring(1));
                   this.oDiv=document.getElementById(arg.substring(1));
                    this.elements.push(document.getElementById(arg.substring(1)));
                 break;
                case '.'://class
                    
                    this.elements=getByClass(document,arg.substring(1));
                 break;
                default://标签
                    this.elements=toArray(document.getElementsByTagName(arg));
                 break;
            }
            break;
        case 'Object':
            	this.elements.push(arg);
            break;
    }
}
```

**jquery中所有事件都是绑定形式**

```js
function bindEvent(obj,events,fn){
    if(obj.addEventListener){
        obj.addEventListener(events,function(ev){
            if( fn()==false ){
                ev.preventDefault();
                ev.cancelBubble=true;
            }
        },false);
    }
}
```

