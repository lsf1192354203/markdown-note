### less

* less中的变量

* # [Less用法之——带参数混合](https://www.jianshu.com/p/0ed21e9c1597)

* 定义一个带参数的属性集合:

```les
.border-radius (@radius) {
  border-radius: @radius;
  -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
}
```

调用它

```less
#header {
  .border-radius(4px);
}
.button {
  .border-radius(6px);  
}
```

给参数设置默认值:

```less
.border-radius (@radius: 5px) {
  border-radius: @radius;
  -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
}
```

所以现在如果我们像这样调用它的话:radius的值就会是5px

```less
#header {
  .border-radius;  
}
```

你也可以定义不带参数属性集合,如果你想隐藏这个属性集合，不让它暴露到CSS中去，但是你还想在其他的属性集合中引用，你会发现这个方法非常的好用:

```less
.wrap () {
  text-wrap: wrap;
  white-space: pre-wrap;
  white-space: -moz-pre-wrap;
  word-wrap: break-word;
}
pre { .wrap }
```

输出

```less
pre {
  text-wrap: wrap;
  white-space: pre-wrap;
  white-space: -moz-pre-wrap;
  word-wrap: break-word;
}
```

**@arguments 变量**\

@arguments包含了所有传递进来的参数. 如果你不想单独处理每一个参数的话就可以像这样写:

```less
.box-shadow (@x: 0, @y: 0, @blur: 1px, @color: #000) {
  box-shadow: @arguments;
  -moz-box-shadow: @arguments;
  -webkit-box-shadow: @arguments;
}
.box-shadow(2px, 5px);
```

输出

```less
box-shadow: 2px 5px 1px #000;
  -moz-box-shadow: 2px 5px 1px #000;
  -webkit-box-shadow: 2px 5px 1px #000;
```

