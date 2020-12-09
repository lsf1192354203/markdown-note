### ES6对内置对象的拓展

##### <font color=red>一、字符串新增</font>

###### 判断字符串是否存在某个字符串

```js
var str = "miaovketang";
console.log(str.indexOf("ke"));//ke在字符串中首次出现的下标  5
console.log("zzzz")//-1

```

###### es6判断字符串是否存在某个字符串

```js
//判断是否存在某个字符串
var str ="miaovketang"
console.log(str.includes("zzz"))
//判断是否以某字符串开头
console.log(str.startsWith("miaov"));
//判断是否以某字符串结尾
console.log(str.endsWith("miaov"));
//重复某字符串
var str="miaov |"
str.repeat(3);
console.log(str.startsWith("miaov"));
```

##### es6超级字符串

```js
//es5
var html='<ul><li></li><li></li></ul>'
var html='<ul>'
+'<li></li>'
+'<li></li>'
'</ul>'
console.log(html);
//es6
var html=`
<ul>
<li></li>
<li></li>
</ul>
`
var classStr="yellow";
var html=`<div class="red"></div>`
var html=`<div class='blue'></div>`
var html=`<div class='${classStr}'></div>`
console.log(html);
var n =2;
var m=3;
console.log("n+m="+(n+m))
console.log(`n+m=${n+m}`)
var isRaning =true
console.log(`今天天气是${isRaning?"雨天"："晴天"}`)
//函数执行
functtion fn(){
	return "miaov"
}
console.log(`fn执行结果是：${fn()}`)
```

##### <font color=red>二、字符串新增</font>

```js
var arr = new Array(10,20,30);
console.log(arr)
//es5中数组长度为10
var arr = new Array(10);
console.log(arr)
//es6中的数组
var arr2 =Array.of(10,20,39)
var arr2 =Array.of(10)
console.log(arr2)
//es6中判断数组
console.log(Array.isArray([]))
console.log(Array.isArray({}))

var els = document.all;
var els = document.getElementsByTagName("*");
console.log(Array.isArray(els))
//类数组转为数组
var arrEles=Array.from(els);
//寻找数组当中的某一个或者符合某个标准的一项
var arr=[20,39,35]
arr.find(function(item){
    //console.log(item)
    
})
//寻找数组当中符合某个标准的一项
var res =arr.find(function(item){
    //console.log(item)
    return item>33;
})
console.log(res)
//寻找数组当中符合某个标准的一项下标
var res =arr.findIndex(function(item){
    //console.log(item)
    return item>33;
})
console.log(res)
//返回符合测试条件的第一个数组元素值。如果没有符合条件的则返回undefined

```

#####  <font color=red>三、对象新增（一）</font>

```js
var a=1;
var obj={
    a:a,
    fn:function(){
        console.log("fn")
    }
}
obj.fn();
console.log(obj)

//es6:如果键名和键值是相同的可以简写为a,
var obj={a};
var obj={
    a,//a:a
    fn(){
        console.log("fn")
    }
};
obj.fn();
console.log(obj)
//---------------------------------------
//希望键的键名是一个变量
var attrname="height";
var attobj = {};
var attFn = "fn";
var obj={
    [attrname]:100,
    [attobj]:"hello",
    [attFn](){
        console.log("fn")
    }
}
obj.fn();
console.log(obj)//{height:100}
//-------------------------------------
console.log(1==1)//true
console.log(NaN===NaN)//false
//is方法判断全等
console.log(Object.is(1,1))//true
console.log(Object.is(NaN,NaN))//true
console.log(Object.is({},{}))//false
//-------------------------------------
function move(obj){
    var defaultObj={
        ease:"linear",
    	duration:1000
    }
    //es5:defaultObj和obj结合起来的一个新的对象
    var para={
        ease:obj.ease || defaultObj.ease,
        duration:obj.duration || defaultObj.duration
    }
    console.log(para);//easeIn ,2000
    //es6中合并方法：越往后写的会保留下来，会修改传进来的第一个参数
    Object.assign(obj,defaultObj)//把defaultObj往obj上融合
    console.log(obj)
    
    Object.assign(obj,defaultObj，{a:1})
     console.log(obj)
	var para2 ={}；
	Object.assign(para2，obj,defaultObj，{a:1})
     console.log(para2)
}
move({
    ease:"easeIn",
    duration:2000
})
```

<font color=blue>对象是不支持以对象作为key的</font>

#####  <font color=red>三、对象新增（二）</font>

```js
var obj = {
    a:1,
    b:2
}
for(var attr of obj){
    console.log(attr)
}
//-----------------
console.log(Object.keys(obj))//把这个对象上面可以遍历的键名列到一个数组当中，并将数组返回
console.log(Object.values(obj))
console.log(Object.entries(obj))//二维数组（键名，键值）
for(var attr of Object.keys(obj)){
    console.log(attr)
}
for(var attr of Object.entries(obj)){
    console.log(attr)
}
for(var [key,val] of Object.entries(obj)){
    console.log([key,val])
}
//obj is not iterable
```

###### <font color=blue>扩展运算符</font>(由一个整体打散成参数的形式)

```js
var obj={
    a:1,
    b:2
}
var res ={
    ...obj//把后面的参数全部打散
    aa:1,
    bb:3,
    c:4
}
console.log(res)
//------------------
var arr=[1,3,4,5,6]
console.log(arr)
console.log(...arr)//1,3,4,5,6
console.log(1,3,4,5,6)
//-------------------
var arr=[1,3,4,5,6]
consle.log(Math.max(...arr))
console.log(Math.max(3,22,21,5))
//数组去重----------------------
var arr =[a,b,c,3,a,b,c];
var res = new Set(arr)
var arr2=Array.from(res)
//-----
var arr =[a,b,c,3,a,b,c];
var res =[ ...new Set(arr)]
console.log(res)
```

#### <font color=red>函数新增</font>

###### 默认参数设置

```js
//es5:参数默认值设置
function add(a,b){
    var _b=b || 100;
    return a+_b;
}
console.log(add(10))
console.log(add(10,5))
console.log(add(10,0))//异常
//修改
var _b = b===undefined?100:b;
//------------------------
//es6:参数默认值设置
function add(a,b=100){
    return a+_b;
}
```

###### 剩余参数设置

```js
//-----------
//arguments是你传入实参的集合
function fn(){
   console.log(arguments)
}
fn(10,5,10,5)
//---------------------
function fn(){
   console.log(a,arguments)
}
fn(10,5,10,5)
//-----------
//打印除了a以外剩余的参数
function fn(a,...rest){
   console.log(a,rest)
}
```
###### 箭头函数

```js
var add = (a,b) =>{return a+b}
//相等于
var add = (a,b)=>a+b//若返回的是一条语句可以简写
var add = (a,b) =>({miaov:3})//如果返回的是一个对象要加一个（）
//{}当作是函数体
var add = (a,b) =>{
    miaov:for(var i=0;i<10;i++){//miaov 是语句标签
        console.log(i)
        if(i==3){
            break miaov;
        }
    }
}
//只有一个参数时
var add = (a)=>a*100
//变体，有一个参数可以省略小括号
var add = a =>a*100
//变体，有0个参数时小括号不能省
var add = （）=>a*100
console.log(add(2))
```

**筛选数组元素**

filter函数要做的就是把你回调函数当中返回为true的结果当中的那一项，把它给拼起来，收集起来，并且组成一个新的数组返回，用res 接收返回值

```js
var arr = [1,28,30,55,85];
var res = arr.filter(function(item){
    return item>20
})
console.log(res)

//es6变体

var res =arr.filter( item=>item>20 )
```

**<font color=red>箭头函数注意事项</font>**

```js
//this指向
var fn =()=>{
    console.log(this)
}
//当你这个函数创建的时候，你当前环境下的this
fn();//window
document.onclick=fn;//window
//------------------
fn.bind({a:1})//无效修改this指向
//------------
var fn =()=>{
    console.log(arguments)//箭头函数没有arguments;
}
//---------
//若真想得到实参集合
var fn =(...r)=>{
    console.log(r)
}
fn(1,2,3)
//箭头函数不能通过new来调用
```



