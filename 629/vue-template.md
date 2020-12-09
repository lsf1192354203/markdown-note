### vue-template

```html
<div id="demo">
    <span>miaov</span>
</div>
<script type="x-template" id="temp">
<div>hello</div>
</script>
var obj={name:"xiaoming",age:22}
var vm = new Vue({
el:"#demo",
data:obj,
template:"#temp"
})
```
**createElement:(标签名，子元素)**

```html

<div id="demo">
    <span>miaov</span>
</div>
<script>
    var obj={name:"xiaoming",age:22}
	var vm = new Vue({
    el:"#demo",
    data:obj,
    render(createElement){
        return createElement(
        	"ul",[
                createElement("li",1),
                createElement("li",2),
                createElement("li",3),
            ]
        )
    }
})
</script>
```

**createElement:(标签名，【数据对象】，子元素)**

```html
<div id="demo">
    <span>miaov</span>
</div>
<script>
    var obj={name:"xiaoming",age:22}
	var vm = new Vue({
    el:"#demo",
    data:obj,
    render(createElement){
        return createElement(
        	"ul",
            /*{
               class:{} ,//绑定class,和v-bind:class一样的API
               style:{} ,//绑定样式,和v-bind:style一样的API
               attrs:{},//添加行间属性
               domProps:{},//DOM元素属性
                on:{}//绑定事件
                
                nativeOn:{},//监听原生事件
            	directives:{},//自定义指令
        		scopedSlots:{},//slot作用域
        		slot:{},//定义slot名称
        		key："key",//给原生添加唯一标识
        		ref:"ref"//引用信息
            },*/
            {
                class:{bg:true},
                style:{fontSize:"50px"},
                attrs:{
                    abc:"miaov"
                },
                domProps:{
                    innerHTML:"<li>我是html</html>"//元素对象的属性
                }
                
            },
            [
                createElement("li",1),
                createElement("li",2),
                createElement("li",3),
            ]
        )
    }
})
</script>
```

