### script标签

```js
@import url("body.css");
div{
    width:20px;
    height:30px;
    
}

```

```js
//1.js
var a=1;
```
```js
//2.js
console.log(a)
a+=1;
```
```js
//3.js
console.log(a)
```

```html
<script src="./1.js"></script>
<script src="./2.js"></script>
```

```html
<!-- defer:在外链js上使用，会在其他的js，dom节点加载完成之后在加载（换言之：延迟加载）-->
<script src="./2.js" defer></script>
<script src="./1.js"></script>
```
```html
<!-- 多个defer: 执行按照先后顺序-->
<script src="./2.js" defer></script>
<script src="./3.js" defer></script>
<script src="./1.js"></script>
```
