### Vue

```js
v-bind:title='msg'简写：

v-on:click='fn'简写@
v-model='msg'
v-for='obj'
v-if=''
v-text=''//解决先出现{{}}的问题
v-html=
v-cloak-----------css样式：[v-cloak]{display:none}
v-once//一般显示静态数据
```

**v-for**

```js
//v-for
语法：v-for="value,index in arr"
v-for="value,key,index in object"

Object.keys()
```

**v-if&&v-show**

```js
v-if
//语法：v-if="表达式"    dom节点会移除-----根据表达式的值的真假条件渲染元素和移出元素	
v-show
//语法：v-show="表达式"  dom节点不移除------根据表达式的值的真假条件，切换元素的 CSS 属性 display属性

//初始页面根据条件判断是否要渲染某一块的模板，使用v-if
//频繁的切换模板的显示隐藏，使用v-show

```



Object.assign({},vm.miaov,{  ketang:'新的'})

**删除对象属性**

```js
this.$delete(this.choose,key,'');
```



**对象的响应数据变化**

```js
var vm.miaov=Object.assign( {},vm.miaov,{  ketang:'新的'} );
//vm.$set(vm.miaov,'ketang','新的data')
//Vue.set(vm.miaov,'ketang','新的data')
```

**数组的响应数据变化**

```js
/*
			提供了观察数组的变异方法，使用这些方法将会触发视图更新
			push()、pop()、shift()、unshift()、splice()、sort()、reverse()
			会改变原数组
			*/
			//vm.list.push(1000)

			//不会改变原数组
			//vm.list = vm.list.map(item => item*3)

			// 通过下标改变值不可以
			//vm.list[0] = 'miaov';

			//可以这样使用
			//vm.list.splice(0,1,"miaov");

			// length是不能改变原数组的
			vm.list.length = 1;

```

**可控制Class**

```js
class='{class名字：表达式}'
表达式为true就添加class，为false就忽略
控制style
v-bind:style="{样式名：样式值 }"

vue中的事件
语法：v-on:事件名='事件处理函数'

需要传参
语法：v-on:事件名='事件处理函数(参数)'
```

**事件处理函数对象**

```js
<div @click='test2($event,123)'></div>
//$event,当在模板中给事件的方法传参，需要手动使用$event把事件对象传给方法
```

**Object.defineProperty语法：（obj,prop,description）**

```js
Object.defineProperty(data,'miaov',{
    //数据描述
    value:'ketang'，
    writable:false//不允许改写
    enumerable:false//是否可以枚举
    configurable:false//是否可删除属性
    //访问器描述
    
})
//删除对象属性
delete data.title
/*
可以增加属性，也可以更改已有的属性。
*/
```

**数据劫持包装方法**

```js
var data = {
				title: '新闻',
				miaov:1
			}

			// 数据劫持，转成getter和setter

			observer(data)
			

			function observer(obj){
				Object.keys(obj).forEach((item) => {
					defineReactive(obj,item,obj[item])
				})	
			}

			function defineReactive(obj,key,value){
				Object.defineProperty(obj,key, {
					get(){
						return value;
					},
					set(newValue){
						value = newValue;
						title.innerHTML = newValue ;
					}
				})	
			}

```

**事件修饰符**---方法只有纯粹的数据逻辑，而不是去处理DOM事件细节

<font color=red>@事件名.修饰符.修饰符=‘ ’</font>

语法：v-on:事件名.修饰符=“事件处理函数”

* .stop

* .prevent

* .capture

* .self

* .once

  按键修饰符

  * .enter
  * .tab
  * .delete
  * .esc
  * .space
  * .up
  * .down
  * .left
  * .right



```js
<a @click='fn'></a>
fn(e){
    e.preventDefault();
}
```

**计算属性**

```js
data:{
    list:[2,5,33,22]
}
computed:{
    reverseMesage(){//计算属性挂载在实例上
        return 1;
    },
    isCheckedAll:{
        get(){
            console.log('取值');
            return this.songList.every(function(item){
                return item.checked
            });
        },
        set(newValue){
            console.log('设置值了');
            console.log(newValue);

            this.songList.forEach(item => item.checked = newValue)
         }
    }
    
}
```

