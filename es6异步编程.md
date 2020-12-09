### es6异步编程

##### js异步简介

```js
/*
异步：
js:单线程
把一些耗时的事情通过新开线程的方式来实现
我们把这些任务称为：异步任务。
*/
```



##### 同步与异步

##### Promise基本使用

```js
/*Promise----js提供的内置对象
构造函数，通过Promise来构建一个异步任务处理对象
*/
new Promise((res,rej)=>{
    //要执行的异步任务
})
var a=1;
setTimeout(()=>{
    a=10;
},2000)//它是个异步任务，不会占用主线程
console.log(a);

//----------------------
new Promise(()=>{
    setTimeout( ()=>{
        a=10;
    },2000 );
}).then( ()=>{
    //then方法就是Promise处理完任务以后继续执行的任务
	console.log(a)
} )
//---------------------------
/*
Promise状态：
	-resolve()函数：更改Promise对象为成功状态
	-reject()函数：更改Promise对象为失败状态
*/
let p1 =new Promise(()=>{
    setTimeout( ()=>{
        a=10;
        resolve();
    },2000 );
});
p1.then( ()=>{
    //then方法就是Promise处理完任务以后继续执行的任务
	console.log(a)
},()=>{
    console.log("失败了")
} )
/*
then方法：
任务后续处理函数，一般情况下某个Promise任务完成功还是失败的后续任务
	.then(onFulfilled/onResolved,onRejected)
*/
/*
Promise值：
	resolve,reject这两个函数是可以传入参数的，传入的参数将被传递给then函数进行使用
*/
new Promise(()=>{
    setTimeout( ()=>{
        var a=10;
        //resolve(a);
        reject('出错了')
    },2000 );
}).then( (v)=>{
    //then方法就是Promise处理完任务以后继续执行的任务
	console.log(v)
}，err=>{
        console.log(err)
} )
```



##### Promise任务链-----（存在问题中途退出难）

```js
new Promise( (resolve,reject)=>{
    //有异步任务
    resolve();
    
} ).then(
    ()=>{
        console.log("resolve",1);
    },
    ()=>{
        console.log("reject",1);
    }
).then(
	()=>{
        console.log("resolve",2);
    },
    ()=>{
        console.log("reject",2);
    }
)
/*
Promise Chain
then函数执行后会返回一个新的Promise对象
	-如果then没有传入处理函数，那么会返回一个继承了上一个处理状态的Promise对象
		new Promise((resolve,reject)=>{
			//resolve();
			reject();
		}).then(/()=>{//两个//间代码注释
            return new Promise((resolve,reject)=>{
                //resolve();
                reject();
            })
		}/).then(()=>{console.log(1)},()=>{console.log(2)})
	-如果then传入了处理函数，那么默认返回一个fulfilled/resolved状态的Promise对象
	new Promise((resolve,reject)=>{
			//resolve();
			reject();
		}).then(
		()=>{
			console.log(1)
		},
		()=>{
			console.log(2)
		}
		).then(()=>{console.log(3)},()=>{console.log(4)})
	-如果then传入了处理函数，通过处理函数显示的return了一个新的Promise，那么返回这个显示的Promise对象
	new Promise((resolve,reject)=>{
			
			reject();
		}).then(
		()=>{
			console.log(1)
		},
		()=>{
			console.log(2)
			return new Promise((resolve,reject)=>{
		
			reject();
		  })
		}
		).then(()=>{console.log(3)},()=>{console.log(4)})
*/

//--------------catch()执行以后也会返回一个Promise对象
 
```



##### Promise其他方法与Async-await

##### <font color=red> Promise.all</font>

```js
let p1=new Promise( (resolve,reject)=>{
    setTimeout(()=>{
         console.log(1)
        resolve(10);
        
    },2000);
} )
let p2=new Promise( (resolve,reject)=>{
    setTimeout(()=>{
         console.log(2)
        resolve(100);
        
    },2000);
})
//等上面两个promise完成后再执行

Promise.all([p1,p2]).then(()=>{
    console.log(3)
})
Promise.all([p1,p2]).then(arr=>{
    console.log(3,arr)//1,2,3,[10,20]
})
```
##### <font color=red> Promise.race</font>
```js
let p1=new Promise( (resolve,reject)=>{
    setTimeout(()=>{
         console.log(1)
        resolve(10);
        
    },2000);
} )
let p2=new Promise( (resolve,reject)=>{
    setTimeout(()=>{
         console.log(2)
        resolve(100);
        
    },2000);
})
//等上面两个promise完成后再执行

Promise.race([p1,p2]).then(()=>{
    console.log(3)
})
Promise.race([p1,p2]).then(arr=>{
    console.log(3,arr)//1,2,3,[10,20]
})
```
##### Promis.resolve(),reject()
```js
Promise.resolve().then(()=>{
console.log(1)
},()=>{
console.log(2)
})
Promise.reject().then(()=>{
console.log(1)
},()=>{
console.log(2)
})
//------------
Promise.resolve(1).then(v=>{
    console.log(v)
})//1
//------------------
Promise.resolve(new Promise((resolve,reject)=>{
    reject("错误")
})).then(v=>{
    console.log(v)
},err=>{
    console.log(err)
})
//----------
//Promise.resolve(value)、Promise.resolve(promise)---->直接返回promise参数的Promise对象
/*Promise.resolve(thenable)
返回thenable对象
thenable:一个包含then方法的对象
*/
Promise.resolve({
    then(){
        console.log("then");
        return Promise.resolve("miaov")
    }
}).then(v=>{
    console.log(v)
})
```

##### 最终异步解决方案

```js
//await能拿到执行后的结果，await后跟异步函数
async function fn(){
 var v=  await new Promise( (resolve,reject)=>{
        setTimeout(()=>{
            var a=10;
            resolve(10);
        },2000);
    } );
    console.log(v)
}
//以上简化
async function fn(){
    var v = await getValue(10);
    console.log(v);
    //return;如果想阻止后续代码执行
    var w=await getValue(20);
    console.log(w);
    try{
        var y=await getValue(200);
        console.log(y);
    }catch(e){
        console.log(e);//使用try、、catch捕获已有的错误
    }
}

function getValue(val){
    return new Promise( (resolve,reject)=>{
        setTimeout(()=>{
            var a=10;
            if(val<100){
                resolve(val*10);
            }else{
                reject("传入的值太大了");
            }
            //resolve(10);
        },2000);
    } );
}

fn();
```

