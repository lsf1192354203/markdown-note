### ES6弱引用WeakMap()

```JS
var m = new Map();//强引用
var zm={
    name:"zmouse",
    age:30
};
var reci={
    name:"reci",
    age:20
};
m.set(zm,"miaov1"); 
m.set(reci,"miaov2");

console.log(m); 

zm=null;//垃圾回收机制
console.log(m);
```

```js
var wm = new WeakMap();//弱引用
var zm={
    name:"zmouse",
    age:30
};
var reci={
    name:"reci",
    age:20
};
wm.set(zm,"miaov1"); 
wm.set(reci,"miaov2");
zm=null;
console.log(m); 
```

<font color=red>**弱引用的键名不能以非对象作键名**</font>

```js
wm.set(1,'miaov');
```

<font color=red>**弱引用不可遍历**</font>

```js
for(var v of wm){
    console.log(v);
}
```

