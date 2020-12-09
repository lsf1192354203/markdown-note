### Array去重方法

```js
var arr=[{name:"小明",age:12},{name:"晓丽",age:20},{name:"小明",age:30}]
function fn(arr){
    var json={};
    var arrlist=[];
    arr.forEach( (item)=>{
        if(!json[item.name]){
            json[item.name]=true;
            arrlist.push(item);
        }
        return arrlist
    } )
}
```

