

### jQuery -UI

jQUI概念

JQUI是是以jQuery为基础的javascript用户界面代码库。包含用户交互、动画、特效和带主题的可视控件等功能。通常我们也叫做jQUI组件

#### 组件与插件的区别

功能性：组件---功能比较丰富       插件----单一

中心性：组件---以它为主       		插件----以它为辅

统一性：组件---统一性较高       	 插件----多人开发，统一性不太好

### jQuery UI

jqui包含项

* UI核心
* UI交互
* UI控件
* UI特效
* CSS主题
依赖关系
UI特效是独立的
* [菜鸟教程]（https://www.runoob.com）

### UI特效

* [easing函数]（http://www.w3cschool.cc/jqueryui/api-easings.html）

* animate()

* addClass()

* removeClass()

* ### show()  |  hide() |toggle|effect()
```js
//effects特效
/*
blind:百叶窗   bounce：反弹
clip:剪切      drop：降落
explode:爆炸   fade:淡入淡出
fold:折叠      puff:膨胀
pulsate:心跳   scale：缩放
shake:震动     size:尺寸
slide:滑动     transfer：转移
*/
$("#div1").show("fold ",{direction:"left|right|up|down"},1000);
//方向：direction
$("#div1").effect('fold',1000)

```

* #### UI交互

* draggable()

* droppable()

* resizable()

* selectable()

* sortable()

```html
<div id="div1"></div>
```
```js
$(function(){
    $("#div1").draggable();
})
//widget-----返回当前元素的操作
```

* 如何使用
  * 配置参数
    * 初始化时-----$("#div1").draggable({axis:'y'});
  * 方法
    * 初始化后
  * 自定义事件
    * 普通事件之上的封装

```js
$(function(){
    $("#div1").draggable(
        {
            axis:'x',
            create:function(){alert(1)},
            start:function(){alert(2)},
            
        }
    )
})
```

#### UI交互

* 有状态的插件
  * 在初始化后，可获取和设置配置--------$("#div1").draggable('option','axis','x')---------设置
* 统一化的命名方式

```js
$('#sortable').sortable({axis:'x'})
```

* 方法的两种方式
```js
//1.$("#div1").draggable('disable')
//2.$('#div1').draggable('instance').disable()
//a:$('#div1').on('dragstart',function(){alert(2)})//jQuery方法
//b：$("#div1").draggable({axis:'x',create:function(){alert(1)},start:function(){alert(2)} })
/*1种：在配置参数中写；2种：*/
```
* 事件的两种方式
  * create事件的注意事项
* 结合性的交互方案
  * 例如：dgaggable和sortable

### UI控件

```js
$("#div1").accordion({heightStyle:'auto'});
$('input').click(function(){
    var html=$('#div1 div').eq(0).html();
    $('#div1 div').eq(0).append(html);
    $('#div1').accordion('refresh');
})
```

### ui 核心

##### 选择器   ： - ：data（）      -：focusable()    -:tabbable()

```html
<div>    div</div>
<div>    div</div>
<div>    div</div>
<div>    div</div>
<input type='text'>
<input type='text'>
<input type='text'>
<div id='scrollParent' style='height:50px;overflow:auto;'>
    <p >
        测试scrollParent
    </p>
</div>
```

```js
$("div").slice(0,2).data('name','hello');
$('div:data(name)').css('background','red');
$('body').children(':focusable()').css('background','red');
$('body').children$(':tabbable()').css('background','red');
```

##### 方法： 1、disableSelection()     2、enableSelection()  3、focus()    4、scrollParent() 5、jQuery.ui.keyCode

```js
$('div').disableSelection();
$('div').focus(1000)//1000是延迟的效果，二参回调
$('input').focus(1000,function(){
    this.style.background='red';
})
//scrollParent--------有滚动距离的父级
$('p').scrollParent().css('background','red')
//做键盘操作的时候----------jQuery.ui.keyCode
$(document).on('keydown',function(ev){
    if(ev.keyCode==13){//ev.keyCode==$.ui.keyCode.ENTER
        alert('回车')
    }
})

```

##### 实用工具   1、mouse（）     2、position（）

```css
#div1{width:100px;height:100px;background:blue;}
#div2{width:30px;height:30px;background:red;}
```



```html
<div id='div1'>
    <div id='div2'>
        内容
    </div>
</div>
```



```js
//mouse()
/*
内部使用，基于Widget Factory
http://api.jqueryui.com/mouse
继承格式：$.ui.mouse
*/
```

```js
//position()
/*
my
at
of
*/
$('#div2').position(){
    my:'left top',
    at:'top',
    of:'#div1'
}
```

##### Widget Factory

* 编写出具备相同抽象化的插件
* 命名空间
* 继承方法
  * [网址](http://api.jqueryui.com/jQuery.widget)
* 私有和公有
* 实例：编写widget进度条插件
```html
<div id="div1">0%</div>
```

```js
//a:function(){alert('a')}//不带下划线的是公有的方法，（可以在外面找到）
//_a:function(){alert('aa')}//带下划线的是私有的方法，（只能内部使用）
//自定义方法、自定义事件
//$.widget('miaov.testProgressBar',$.ui.mouse,{})//继承 $.ui.mouse 
```

