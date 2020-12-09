### 深度详解EcmaScript6

#### 使用模块

###### commonjs amd cmd es6

```js
//尽可能将js标签放到body标签内部的最下面，不影响页面内容的渲染的情况下，让他尽早的去执行
//<img></img>
//<script></script>
```

![alt 页面script运行流程](C:\Users\Administrator\Desktop\markdown\script.jpg)

```html
<script src="./a.js" defer> </script>

```

+ 普通js加载

     - type="application/javascript"

          - 默认省略

          - 默认同步加载  
      - 同步加载的问题
  - 使用异步加载
      + defer(延迟)
          - 在外链js标签上使用
          - 等待DOM结构加载完成，嵌套脚本执行完成再执行
          - 多个defer之间可以确保加载顺序
  + es6模块化使用
      - 使用type="module"
      - 服务器环境下使用
      - 默认是异步加载（默认的份儿）
  + <font color=red>注意事项</font>
      - 代码运行在模块作用域
          - 模块作用域和全局作用域
      - 默认开启严格模式 “use strict”
      - 顶层的this指向undefined
      - 一个模块被加载多次则执行一次

  - 语法：
      - export(导出)
          - [export](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/export)
          - [import](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/import)
      - 模块导出的是对原来值的引用
          - 不可以直接在导入模块后修改值
          - 可以通过被导入模块提供的方法修改，被导入模块内部的值
          - 所有导入的内容都是引用关系
- 数组的解构赋值
     - 按顺序结构

     - 不完全解构

     - 解构不成功

     - 默认值

     - 剩余值

- 对象解构赋值
  
#### 导入与导出

```js
//export.js
export var m="momo",kill="会唱歌"
export default 999;
```



```js
//import.js
import * as all from "./a.js"
console.log(all.m+all.kill+all.default)
```

---------

```js
function fn(){
    return{
        add:function(){},
        get a(){
            
        }
    }
}
obj.a
```



#### 模块化语法

#### ES6结构赋值



