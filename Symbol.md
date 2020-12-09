### Symbol

新增独一无二的Symbol,每次调用Symbol时都会创建一个新的独一无二的值

##### Symbol 作为对象键名的使用

```js
var s = Symbol();
console.log(typeof s)//Symbol
//Symbol标志
var s = Symbol("a");
//以Symbol为键值的的键名对
var obj = {
    a:1
}
var a = Symbol("a");
obj[ a ]="sa";
console.log(obj)
console.log(obj[ a ])
//避免键名的重复
for(var attr in obj){
    console.log(obj[attr]);
}
//以Symbol为键名的不会被遍历到
//解决方法
Object.getOwnPropertySymbols(obj)//以Symbol为key的键名
```

##### Symbol 作为数据类型的使用（typeof）

```js
var s=Symbol("a");
console.log(s+1)//报错
console.log(s+"a")//报错
console.log(!!)//true
```

#### Symbol 主要用在对象内部

