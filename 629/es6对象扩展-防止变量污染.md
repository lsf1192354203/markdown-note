### es6对象扩展-防止变量污染

```js
var util = (function (){
					function add(){
						
					}

					function isFunction(){
							
					}

					function isArray(){
							
					}

					return {
						add,
						isFunction,
						isArray
					}

				})();

			util.add();


			var miaov = 10;

			var o = {
				//miaov:miaov
				miaov,
				fn:function(){},
				fn2(){} // 相当于：fn2:function(){}
			}
```

**Object.assign(target,[obj1,obj2,obj3,.....])**

用户合并对象，将源对象的所有可枚举属性，复制到目标对象

```js

```

