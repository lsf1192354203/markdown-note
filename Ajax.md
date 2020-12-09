

### Ajax

<font color='red'>**安装服务器工具：Wampserver集成环境**</font>：[网址](www.php100.com)

把我们做的文件放到指定目录下

注意：迅雷、下载软件尽量关闭。

**概念**

异步的JavaScript和XML：用javascript异步形式去操作XML

作用：数据交互（可以请求也可以发送数据）--------把数据发送给asp,再从asp处理后获取数据

<font color=red>通过ajax：也就是js当中的一个内置的ajax对象</font>

status：服务器状态码，http状态码

**responseText:是字符串**

**原理**：

```js
var oBtn=document.getElementById('btn');

oBtn.click=function(){
    //打开浏览器
    /*
    1、创建一个ajax对象------XMLHttpRequest
    */
    var xhr = new XMLHttpRequest() || new ActiveXObject('Microsoft.XMLHTTP');
    if(window.XMLHttpRequest)
    //在地址栏输入地址
    xhr.open('get','1.txt',true);
    //提交
    xhr.send();
    //等待服务器返回内容
    xhr.onreadystatechange=function(){
        if(xhr.readyState==4 && xhr.status==200){
            alert(xhr.responseText);
        }
    }
    
    //try ...catch 捕获异常
    try{//代码尝试执行这个块中的内容，如果有错误，则会执行catch{}，并会传入错误信息参数
       var xhr = new XMLHttpRequest()
    }catch(e){
       var xhr = new ActiveObject('Microsoft.XMLHTTP');
    }
    
}
```

**表单**

* action:数据提交的地址--------默认是当前页面
* method:数据提交的方式------默认是get方式
  * 1.get--------url长度限制的原因，我们不要通过get方式传递过多的数据-----传递的是字符串类型的
  * 2.post------理论上无限制-----key传文本或二进制
  * enctype:提交的数据格式-----默认数据格式application/x-www-form-urlencoded

```html
<form action='a.php' method='get' enctype='application/x-www-form-urlencoded'>
    <input type="text" name='username'/>
    <input type='submit' value='提交'
</form>
```
**get**

```js
<?php
header('content-type:text/html;charset="utf-8"');
error_reporting(0);
$username=$_GET['username'];
echo '你的名字是:{$username}';
```

**post**

```js
<?php
header('content-type:text/html;charset="utf-8"');
error_reporting(0);
$username=$_POST['username'];
echo '你的名字是:{$username}';
```

**REQUEST**-----get与post提交过来的数据都可以接收

**解决get地址缓存问题+乱码**

* 1、缓存：在url？后面连接一个随机数，时间戳
* 2、乱码 编码encodeURI

```js
xhr.open('get','2.get.php?username=leo&'+new Date().getTime(),true);
xhr.open('get','2.get.php?username=刘伟&'+new Date().getTime(),true);//中文乱码
xhr.open('get','2.get.php?username='+encodeURI('刘伟')+'&'+new Date().getTime(),true);
xhr.open('get','2.get.php?username=leo&t='+new Date().getTime(),true);
```

**Post方式传递**

* 数据放在send()里面作为参数传递
* 告诉后端发送过去的文档是什么类型的-----声明发送的数据编码类型
```js
xhr.setRequestHeader('content-type','application/x-www-form-urlencoded');
xhr.send('username=leo&age=30');
```

<font color=red>**以上是传递过程中存在的问题**</font>

****

<font color=red>**以下是获取到内容以后存在的问题**</font>

```php
$arr1 = array('leo','momo');
$arr2= array('username'=>'leo','age'=>32);
echo json_encode($arr2);
//字符串转成对应的json,json 转成对应的字符串
/*
JSON对象不一定所有浏览器都支持----json2.js引入
	[son.org]
	两个方法 ：1 stringify:可以把一个对象转成对应的字符串
			 2 parse:可以字符串转成对应对象
	
*/
var arr=[1,2,3];
alert(JSON.stringify(arr));
var s1='[100,20,30]';
var a1 = JSON.parse(s1);
```

**获取cookie**

```js
function getCookie(key){
    var arr1=document.cookie.split(';');
    for(var i=0;i<arr1.length;i++){
        var arr2=arr1[i].split('=');
        if(arr2[0]==key){
            return arr2[1];
        }
    }
}
```

### JSONP

**跨域的问题**

* 域：域名
* 跨域请求（访问）：一个域名下的文件请求另外一个域名下的资源，就产生了跨域

### 跨域的解决

1、本机代理   2、flash    3、script tag

* Jsonp:json with padding
  * 1、script标签
  * 2、用script标签加载资源是没有跨域问题的-----认识的不是文件标识而是文件内容
  * 在资源加载进来之前定义好一个函数，这个函数接收一个参数（data），函数利用这个参数做一些事情
  * 然后需要的时候通过script标签加载对应远程文件资源，当远程的文件资源被加载进来的时候，就会去执行我们前面定义好的函数，并且把数据当做这个函数的参数传入进去
* img/link/script----------可以加载外部资源

 ```js
//2.txt
fn([1.2,3,5]);
//1.php
$arr2=['aa','bb'];
 ```

```html
<script>
    function fn(data){
        alert(data)
    }
</script>
<script>
var oUl1 = document.getElementById('ul1');
    var html = '';
    for (var i=0; i<data.length; i++) {
        html += '<li>'+data[i]+'</li>';
    }
    oUl1.innerHTML = html;
</script>
<script src='2.txt'></script>
```

```js
oBtn.onclick=function(){
    var oScript=document.createElement('script');
    oScript.src='2.txt';
    document.body.appendChild(oScript);
}
```

```js
oBtn1.onclick = function() {
    var oScript = document.createElement('script');
    oScript.src = 'getData.php?callback=fn1';
    document.body.appendChild(oScript);

}
```

```php
<?php
$t = isset($_GET['t']) ? $_GET['t'] : 'num';
$callback = isset($_GET['callback']) ? $_GET['callback'] : 'fn1';

$arr1 = array('111111','22222222','33333333','4444444','555555555555555555555');
$arr2 = array('aaaaaaaaaaaa','bbbbbbbb','cccccccccccc','ddddddddd','eeeeeeeeeeee');

if ($t == 'num') {
	$data = json_encode($arr1);
} else {
	$data = json_encode($arr2);
}

echo $callback.'('.$data.');';
```

