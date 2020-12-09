### JavaScript中缓存

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    
    <!-- <script type="text/javascript">
        // 需求：
        // 要实现一个创建缓存的函数：createCache()
        // 1 对缓存进行读取
        // 2 对缓存进行添加
        // 3 对缓存进行修改
        // 4 缓存的数量要控制在某个范围之内
        // 5 每调用一次创建缓存的函数，就会创建一个缓存出来
        //         并且多个缓存之间相互不影响！

        // 配置属性或者配置文件
        var cacheLength = 3;

        // 分析：
        function createCache() {
            var cache = {};
            // 作用：用来记录存储到缓存中key的顺序
            var keyArr = [];
            // 作用：对缓存进行增删改查
            return function(key, value) {
                // 1 先处理参数的个数
                // 如果是一个参数：表示读取
                // 如果是两个参数：表示设置
                //         a. value === undefined
                //         b. arguments.length
                if(value === undefined) {
                    return cache[key];
                }

                // 以下代码来处理设置缓存
                // 1 修改
                // 2 添加
                //         cache[key] === undefined
                //         如果判断为：true， 说明是 添加
                //         否则，就是修改
                if(cache[key] !== undefined) {
                    cache[key] = value;
                } else {
                    // 以下代码来处理添加的逻辑
                    // 1 缓存的长度超过了限制
                    // 2 缓存的长度没有超过限制
                    //         arr.length > 50
                    //     
                    // 如果是先给数据中添加数据，判断的时候，就是：> 限制的数值
                    // 如果是先判断后添加的数据，判断的时候，就是：>= 限制的数值
                    keyArr.push(key);
                    if(keyArr.length > cacheLength) {
                        // 删除，问题：删除哪一条数据
                        // 删除的是：数组中最开始添加进来的数据
                        // 也就是：索引号为：0 的值
                        var deleteKey = keyArr.shift();
                        delete cache[deleteKey];
                    }

                    // 不管删除还是不删除数据，都要往缓存中添加数据
                    cache[key] = value;
                }
            };
        }

        // LVHA    => LV hao
        // :linked
        // :visited
        // :hover
        // :active

        // 调用
        var typeCache = createCache();
        // 添加缓存：
        typeCache("class", ".cls");
        typeCache("id", "#dv");
        typeCache("tag", "div, p");
        typeCache("tag", "span");
        typeCache(":even", "dddd");

        // 读取：
        console.log(typeCache("class"));        // .cls
        console.log(typeCache("id"));        // #dv
        console.log(typeCache("tag"));        // span
        console.log(typeCache(":even"));        // span

        var strCache = createCache();
    </script> -->

    <script type="text/javascript">
        var cacheLength = 3;
        // 优化代码
        function createCache() {
            // 作用：用来记录存储到缓存中key的顺序
            var cache = {},
            // 作用：对缓存进行增删改查
                keyArr = [];

            return function(key, value) {
                if(value === undefined) {
                    return cache[key];
                }

                if(cache[key] === undefined) {
                    // push 方法的返回值：添加数据之后的长度
                    if(keyArr.push(key) > cacheLength) {
                        delete cache[ keyArr.shift() ];
                    }
                }
                cache[key] = value;
            };
        }


        // 调用
        var typeCache = createCache();
        // 添加缓存：
        typeCache("class", ".cls");
        typeCache("id", "#dv");
        typeCache("tag", "div, p");
        typeCache("tag", "span");
        typeCache(":even", "dddd");

        // 读取：
        console.log(typeCache("class"));    // undefined
        console.log(typeCache("id"));        // #dv
        console.log(typeCache("tag"));        // span
        console.log(typeCache(":even"));    // dddd

    </script>
</body>
</html>
```

