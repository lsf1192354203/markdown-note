### Es6 新的数据结构Map

<font color=red>Map结构依然可以保存键值对</font>，键和值可以任何数据类型：可以是字符串和对象

###### new Map()

```js
var m = new Map([ ['name','miaov'],['grade','2'] ]);
console.log(m.size);
m.set("family","nuannuan");
var broth ={name:"yuyu"},
m.set(broth,1);
var res = m.delete(broth);
console.log(m,res);
```

##### Map结构的属性size

##### Map结构的方法get()

##### Map结构的方法set()

##### Map结构的方法delete()

##### Map结构的方法has()
##### Map结构的方法clear()
##### Map结构的方法forEach(item,key,map)
```js
m.forEach(function(item,key,map){
	console.log(key,value);
})
```
##### Map结构的方法keys()
```js
var res= m.keys();
console.log(res.next());
```
##### Map结构的方法values()
```js
var res= m.values();
console.log(res.next());
```
##### Map结构的方法entries()
```js
var res= m.entries();
console.log(res.next());
```

##### <font color=red>疑问</font>

```js
m.set({},2);
m.set({},22);
console.log(m)
```

#### 遍历接口 MapIterator

```js
var res = m.entries();
console.log(res);//MapIterator;
var arr =[10,30,50];
console.log( arr[Symbol.iterator]);//f values() {[native code]}
```

###### <font color=red>查看一种数据有没有遍历接口</font>Symbol.iterator

```js
var k = arr.keys();
console.log(k.next());//{value:0,done:false}
```

```js
//模仿keys方法
//var k = arr.keys();
var k = i(arr);
console.log(k.next());

function i(obj){
    var index =-1;
    return {
        next:function(){
            index ++;
            return index<obj.length ? {
                value:index,
                done:false
            } : {
                value:undefined,
                done:true
            }
        }
    }
}
```

<font color=red>有遍历接口可以使用for(of)</font>

```js
for(var attr of arr){
    console.log(attr)
}//遍历当前数据结构的每一项
//不同于for in 是他的下标或者key属性名字
```

<font color=blue>**for....in**</font>

```js
//for...in 对数组或对象的循环、迭代操作
let names= ["tom","Jerry"];
for(let i in names){
    console.log(names[i])
}//Tom,Jerry
let obj ={
    a:"one",
    b:"two",
    c:"three"
}//a,b,c
/*判断对象是否是数组、对象的元素/属性------
	格式：（变量 in 对象）
	当‘对象’是数组时：“变量”指的是数组的“索引”；
	当“对象”为对象时：“变量”指的是对象的“属性”
*/
let arrs=["a","b","c"];
console.log("b" in arrs)//false
console.log(2 in arrs)//true

let obj ={
    a:"one",
    b:"two",
    c:"three"
}
console.log(2 in obj)//false;
console.log("b" in obj)//true;


```



<font color=red>拥有遍历接口的有几类：数组，类数组，set/map</font>