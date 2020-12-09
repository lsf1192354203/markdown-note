### 元素getLeft

```js
function getLeft(obj){
    var oLeft=0;
    while(obj.offsetParent){
        oLeft+=obj.offsetLeft;
        obj=obj.offsetParent;
    }
    return oLeft;
}
```

```js
function getOffsetL(obj)
{ 
	var iLeft=0; 
	while(obj)
	{
		iLeft+=obj.offsetLeft;
		obj=obj.offsetParent;	
	} 
	return iLeft; 
} 
```

