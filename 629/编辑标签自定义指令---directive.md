### 编辑标签自定义指令---directive

**自定义指令**

update:被绑定元素所在的模板更新时调用

钩子函数中参数：

el:指令所绑定的元素，可以用来直接操作DOM

binding:一个对象

value:指令的绑定值

```js
var vm = new Vue({//这里面的参数都在选项对象
    el:"#app",
    data:{
        
    },
    methods:{
        
    },
    directives:{
        "focus":{
            update(el,binding)//里面两个参数（指令绑定的元素，）
            console.log(el,binding);//name:指令名，value：表达式的值
        }
    }
})
```

```html
<input v-focus="curtask===task"/>//里面内容是表达式
在自定义指令中如何获取表达式的值？
利用update函数会触发，每次双击
```

**将数据存储到本地存储**

```js
//存取localStorage中的数据
var store = {
    save(key,value){
        //localStorage.setItem(key,value);
        localStorage.setItem(key,JSON.stringify(value));
    },
    fetch(key){
       return JSON.parse(localStorage.getItem(key))||[] ;
    }
}
var list = store.fetch("miaov");
```

**监控属性watch**

```js
watch:{
    list:function(){
        //监控list这个属性，当这个属性对应的值发生变化就会执行函数
        store.save("miaov",this.list);
    },
    
}
```

```js
watch:{
    list:{
        handler:function(){
            //监控list这个属性，当这个属性对应的值发生变化就会执行函数
            store.save("miaov",this.list);
        },
        deep:true//能监控到ischecked属性
     }
}
```

