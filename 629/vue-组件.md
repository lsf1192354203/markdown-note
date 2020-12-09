### 组件

组成：一、样式结构 二、行为逻辑 三、数据

单文件组件

```vu
<template>
	<p>{{greeting}}</p>
</template>

<script>
module.exports = {
	data:function(){
		return {
		greeting:"hello"
		}
	}
}
</script>

<style>
	p{color:red;}
</style>

```

**一 、全局注册**

**二、局部注册**

遇到受限制的元素如：select、ul，变通使用特殊属性is来扩展HTML标签功能

<tr is="custom-select"></tr>

**Vue组件的API来自三部分**

* props参数   传递数据给组件
* slot 定制模板    外部模板混合子组件模板
* event自定义事件   监控子组件交互状态

```js
1/传入的数据结构
	[
    {
        title:xxx,
        children[
        {
        title:xxx,
        children:[]
    }
        ]
    }
]
2/设置的props:
data 数据结构  默认为[]

3/定制模板
	不可定制

4、监控状态变化：
	事件名on-select-change  点击树节点触发
```

**动态组件**

多个组件可以使用同一个挂载点，动态地在它们之间切换，使用<component>元素，使用is特性进行动态绑定

```vue
Vue.component("custom1",{
	template:`<div>
        我是第一个组件
</div>`
})
```

**keep-alive**

可以使用keep-alive把切出去的组件保留在内存中，这样可以保留他的状态避免重新渲染

