### Es6的解构赋值

```js
var obj={
    name:"kemo",
    age:28
}
var {naem,age}=obj;
console.log(name,age);
//如果声明之后赋值
var name ="";
({name}=obj);
//重命名------键名和变量名不一样
var {name：str}=obj;
console.log(str)
//配置默认值
var {c=200}=obj;
console.log(c)
//var {gender:g="male"}=obj;
console.log(g);
//数组解构赋值
var arr = "miaov".split("");
console.log(arr)
var [f,s,t,d]=arr;
console.log(f,s,t,d);
//var [f,,t]=arr;
console.log(f,t);
var [a ="123456",b,c]=arr;
console.log(a,b,c);
//剩余模式
var [a,b,c,...r]=arr;
console.log(a,b,c,r);
```

