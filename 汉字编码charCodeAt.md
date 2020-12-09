### 汉字编码charCodeAt

```js
var str = "妙"；
//str通过实例调用了charCodeAt()方法
console.log(str.charCodeAt(0))//22937   ---字符串编码
//String---通过构造函数调用fromCharCode()方法，这种是静态方法
console.log(String.fromCharCode(22937))//反向由编码得到字符串

```



