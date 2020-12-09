### 数组方法

退出markdown区块用两个回车

```js
let arr=[1,2,3,4,5,6];
arr.slice(1,2).slice(1,2);
//不同于下面
arr.slice(1,2);
```

> 当一个Promise完成或者失败，返回函数将被异步调用。具体的返回值依据以下规则返回：  
>
> * 如果then中的回调函数没有返回值
> * 如果then函数中返回值有一个

```js
;(function(){
    let status ={
        pending:0,
        fulfilled:1,
        rejected:2
    }
    class CustomerPromise{
        constructor(executor){
            this._status = status.pending;
            this.resolvedArr=[];
            this.rejectedArr=[];
            this._handler(executor);
            //executor();
        }
        //_区分是私有的方法，外面无法调用
        //接收外部传入的函数，调用外部传入的函数
        _handler(executor){//executor就是（resolve，reject）=>{}这个函数
            let done=false;
            executor( (val)=>{
                //把状态变成成功的函数
                //console.log(val)
                if(done)return;
                done=true;
                console.log(value)
                this._resolve(val)
            }，(err)=>{
                //把状态变成失败的函数
                if(done)return;
                done=true;
                console.log(err)
                this._reject(err)
            } )
            
        }
        _resolve(){
           //把状态改为成功
            this._status = status.fulfilled;
        }
        _reject(){
            //把状态改为失败
            this._status = status.reject;
        }
        then(resolvedFunc,rejectedFunc){//收集注册的成功状态或失败状态要执行的函数
            
        }
    }
    window.CustomePromise = CustomePromise;
})();
```

```js
new CustomerPromise( (resolve,reject)=>{
    resolve("success")
} )
```

