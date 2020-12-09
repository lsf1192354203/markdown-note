## 改变this指向函数

##### 改变函数this指向三个方法：bind/call /apply

* 三个方法的相同点：

  > 目标函数被调用时，改变this的指向为指定的值
  >
  > 三个方法都是函数的方法，挂载在Function.prototype上

* 不同点：

  > 目标函数调用call和apply后，会直接执行
  >
  > 目标函数调用bind后，不会立即执行，而是返回一个新的函数，调用新函数才会执行目标函数

```js
function fn(...arg){
      console.log(this);
      console.log(arg);
    }
var newFn=fn.bind([1.2,3,4,5],1,3,5,6);
newFn();
fn.prototype.miaov=function(){
    console.log("miaov")
}
//当做构造函数来使用

var f =new newFunc();
console.log(f)
//---------------
Function.prototype.customBind=function(thisArg,...arg){
    let self=this;//目标函数
    console.log(self);
    return function(arg2){//返回的新函数
        self.apply(thisArg,[...arg,...arg2])
    }
}
//let newFn=fn.bind([1.2,3,4,5],1,3,5,6);
let newFn2 = fn.customBind([1.2,3,4,5],1,3,5,6);
console.log("---------------------------")
newFn2(3,4,5,6);
```

