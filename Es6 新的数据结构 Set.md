#### Es6 新的数据结构 Set

```js
var s =new (["a","b","c"])
console.log(s.size)
//不会重复添加
s.add(1).add(2).add(1)
console.log(s)
s.add(NaN).add(NaN)
console.log(NaN===NaN)//false

```

**<font color=red>不会重复添加</font>**

###### set.add()

###### set.delete()

```js
var s.delete("b")
//返回值 var res =s.delete("b")//true
//返回值 var res =s.delete("z")//false
```



###### set.has()

```js
console.log(s.has("a"));//返回true
```



###### set.clear()

```js
s.clear()
console.log(s)
```

遍历set结构

```js
s.forEach(function(item,index,set){
    console.log(item,index,set)
})
```

其他的遍历方式

```js
//keys()
var keys = s.keys()
console.log(keys.next())
console.log(keys.next())
console.log(keys.next())
console.log(keys.next())
//values()
var values = s.values()
console.log(values.next())
console.log(values.next())
console.log(values.next())
console.log(values.next())
//entries()
var entries= s.entries()
console.log(entries.next())
console.log(entries.next())
console.log(entries.next())
console.log(entries.next())
```

