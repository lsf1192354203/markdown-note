### Es6 中的promise

```js
//es5回调地狱
function send(url,callback){
    //var xhr =.....
    //....
    callback()
}
send("/url1",()=>{
    send("/url2",()=>{
		send("/url3",()=>{
			send("/url4",()=>{

            })
        })
    })
})
//异步编程
//es6:promise
var p = new Promise( ()=>{} );//创建的时候（）里面一定要放一个函数
var p = new Promise( ()=>{console.log("实例化。。。")} );//内部函数会立即执行

console.log(p);//Promise {pending}  [PromiseStatus]:"pending"  [PromiseValue]:undefined

//准备
//成功
var p = new Promise( (resolve,reject)=>{console.log("实例化。。。");resolve()} );
//失败
var p = new Promise( (resolve,reject)=>{console.log("实例化。。。");reject()} );
//只能进入一个状态
var p = new Promise( ()=>{return resolve()；console.log("ddgjkd")} );//return 阻止后续代码执行
//then()
var p = new Promise( (resolve,reject)=>{
    console.log("实例化。。。");
    return resolve("成功")；
    
} );
p.then( (data)=>{
    console.log("then:",data)
} )

```



### promise执行顺序和实例方法

```js
console.log(1)//宏任务
setTimeout( ()=>{
    console.log(3)
} )//把里面的函数执行推到下一轮的执行任务当中
setTimeout( ()=>{
    console.log(4)
} )//宏任务
var p = new Promise( (res,rej)=>{
    console.log(5)
    res()
} )//宏任务
p.then( ()=>{//微任务
    console.log(6)
} )
console.log(2)//宏任务
//输出结果：1、5、2、6、3、4
//---------------------------
//then方法、实例方法
```

```js
var p = new Promise( (res,rej)=>{
    res("成功")
} )
p.then( (data)=>{
    console.log(data)
} )
//then方法可以接收两个参数，p.then（成功回调，失败回调）
p.then( (data)=>{
    console.log(data)
},()=>{
    console.log("失败")
} )
//一般情况只会传一个，如果只想捕捉失败的话用catch()
var p = new Promise( (res,rej)=>{
    rej("失败")
} )
p.catch( ()=>{
    console.log("失败")
} )
//如果进入成功状态catch 就不会继续走了
//catch 就是then的另外一种变体
//then执行完后有一个返回值
var p2 =p.then( (data)=>{
    console.log(data)
} )
console.log(p2)//又返回一个新的promise对象
//简写
p
.then( (data)=>{
    console.log(data)
} )
.then( ()=>{
    console.log("then")
} )
//p2和p不相等



```

```js
//then方法执行后会返回一个新的promise对象，但是这个promise其实有两个东西：状态和状态值
/*内部的状态是根据then方法里面的箭头函数的返回值来的，
如果没有返回值，相当于返回undefined,状态是true,但是内部的值是undefined
如果返回的是一个promise：那么p2就相当于内部返回的promise，内部promise是成功，p2状态就是成功
内部promise是失败，p2状态就是失败，其最终目的是调用方便*/
var p= new Promise( (res,rej)=>{
    res("success")
} )
var p2 = p.then( ()=>{
    return new Promise( (res,rej)=>{
        rej()
    } )
} )
p2.then( data=>{
    console.log("p2 then:",data)
    return new Promise ( (res,rej)=>{
        rej()
    } )
} )
.then()

```

**cathch方法**

```js
//捕捉到错误
var  p = new Promise( (res,rej)=>{
    res("success")
} )
p.then( ()=>{
    console.log(1)
    a
} )
.then( ()=>{
    console.log(2)
} )
.then( ()=>{
    console.log(3)
} )
.catch( (err)=>{
    console.log(err)
} )
.finally( ()=>{
    console.log("finishi")
} )
```

**Promise静态方法**

```js
var p = new Promise( (res,rej)=>{
    res()
} )
p
.then( ()=>{console.log(1)} )
//.then( ()=>{return new Promise( (res,rej)=>{res()} )} )
.then( ()=>{return Promise.resolve()} )//静态方法
.then( ()=>{console.log(2)} )
//-----------------
p
.then( ()=>{console.log(1)} )
//.then( ()=>{return new Promise( (res,rej)=>{res(200)} )} )
.then( ()=>{return Promise.resolve(200)} )//静态方法
.then( (data)=>{console.log(data)} )
//------------------------
p
.then( ()=>{console.log(1)} )
//.then( ()=>{return new Promise( (res,rej)=>{res(200)} )} )
.then( ()=>{return Promise.reject("失败！")} )//静态方法
.then( (data)=>{console.log(data)} )
.catch( (err)=>{console.log(err)} )
//-------------------------
var p1=new Promise( (res,rej)=>{
    setTimeout( ()=>{
        res("a")
    } ,1000)
} )

var p2=new Promise( (res,rej)=>{
    setTimeout( ()=>{
        res("b")
    } ,1500)
} )
var p3=new Promise( (res,rej)=>{
    setTimeout( ()=>{
        res("c")
    } ,500)
} )
//两个静态方法：all，race
var p=Promise.all( [p1,p2,p3] )
var p=Promise.race( [p1,p2,p3] )//赛跑
console.log(p)
p.then( data=>console.log(data) )//[a,b,c] 同时执行完后的结果
```

**Promise改写运动**

```js
//之前妙味运动函数
function move ( obj,attr,target,duration,callback){
    var b = parseInt(getComputedStyle(obj)[attr]);
    var c = target-b;
    var d = duration;
    var temp = new Date().getTime();
    var timer = setInterval( function(){
        var t = new Date().getTime()-temp;
        if(t>=d){
            clearInterval(timer);
            t=d;
        }
        var v =c/d*t+b;
        obj.style[attr]=v+"px";
        if(t===d){
            typeof callback === "function" && callback();
        }
    },20 )
}
//-----------------------------
var box = document.getElementById('box')
move(box,"width",200,500);
move( box,"width",200,500,()=>{
    move( box ,"height",300,500,()=>{
        move( box ,"left",300,500,()=>{
            move(box,"top",200,500)
        })
    })
})

```

<font color=red>promise改写运动</font>

```js
function movePromise( obj,attr,target,duration){
    return new Promise( (res,rej)=>{
        var b = parseInt(getComputedStyle(obj)[attr]);
        var c = target-b;
        var d = duration;
        var temp = new Date().getTime();
        var timer = setInterval( function(){
            var t = new Date().getTime()-temp;
            if(t>=d){
                clearInterval(timer);
                t=d;
            }
            var v =c/d*t+b;
            obj.style[attr]=v+"px";
            if(t===d){
                res();
            }
        },20 )
    } )
    
}
movePromise(box,"width",200,500)
.then( ()=>movePromise(box,"height",200,500) )
.then( ()=>movePromise(box,"left",200,500) )
.then( ()=>movePromise(box,"top",200,500) )
.then( ()=>console.log("done") )
```

