### 探索Promise源码

#### 介绍

<font color=red>Promise</font>是<font color=red>JavaScript</font>异步编程的一种流行解决方案，掌握<font color=red>Promise</font>的使用是我们不可或缺的一项基本技能。但是要想熟练掌握并深入的理解它，还是必须要知道它的实现原理的。这节课就是从具体使用角度出发，使用原生手写方式一步一步的带你实现<font color=red>Promise</font>库，而且不仅仅只是包含了<font color=red>Promise</font>目前通用的功能，还有<font color=red>Promise</font>的一些新的特性和未来即将支持的特性的介绍与实现

#### 知识要点

- Promise类
- Promise状态
- Promise.#resolve方法
- Promise.#reject方法
- Promise.then方法
- Promise.catch方法
- Promise.finally方法
- Promise.resolve方法
- Promise.reject方法
- Promise.all方法
- Promise.race方法
- Promise.allSettled方法

### Promise类

Promise的构造函数必须接受一个函数参数（也就是需要执行异步任务的函数，该函数将在传入以后立即调用，并传入Promise对象下的两个方法resolve和reject
### Promise状态
每一个Promise对象存在以下三种状态：
- Pending:进行中，Promise对象的初始状态
- Fulfilled：已成功
- Rejected：已失败
```js
class KPromise{
	static PENDING="PENDING";
	static FULFILLED="FULFILLED";
	static RESOLVED="RESOLVED";
	static REJECTED="REJECTED";
	constructor(handler){
		if(typeof handle !=== "function") throw
		new Error("Promise resolver undefined is not a function")
		//new TypeError
		this.resolvedQueue=[];
		this.rejectedQueue=[];
		this.status=KPromise.PENDING;
		handler(this._resolve.bind(this),this._reject.bind(this));
	}
	
	_resolve(){
		if(this.status!=== KPromise.PENDING) return;
		console.log("_resolve");
		this.status=KPromise.RESOLVED;
		let handler;
		while(handler = this.resolvedQueue.shift())
		{
			handler();
		}
	}
	
	_reject(){
	if(this.status!=== KPromise.PENDING) return;
		this.status=KPromise.REJECTED;
		let handler;
		while(handler = this.rejectedQueue.shift())
		{
			handler();
		}
	}
	then(resolvedHandler,rejectedHandler){
		this.resolvedQueue.push(resolvedHandler);
		this.rejectedQueue.push(rejectedHandler)
	}
}

```

### 微任务 ---postMessage

```js
window.addEventListener("message",_=>{
    if(this.status!=== KPromise.PENDING) return;
		console.log("_resolve");
		this.status=KPromise.RESOLVED;
		let handler;
		while(handler = this.resolvedQueue.shift())
		{
			handler();
		}
});
window.postMessage("")
```

