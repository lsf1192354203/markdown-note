### Php知识

字符串连接符<font color=red>**.**</font>

```php
<?php
    $newsTitle = 'title1';
	$newsTitle2 = 'news';
echo $newsTitle.$newsTitle2;
```

* var_dump-------输出数据类型和对应的值
* trim()----------去除收尾空格
* strlen($newsTitle2)----------获取字符串长度（只能是字节），不能正确处理汉字
* mb_strlen($newsTitle3)-----------获取字符串长度
* 复合数据类型：1、Array 2、Object
* null resource特殊数据类型
* print_r 简洁的输出数组格式
* isset()
##### 数组

```php
<?php
    $newsList =array();
	$news =[];
var_dump($newsList);
//添加数据
$newsData = array('news1','news2','news3')
var_dump($newsData);
//修改键值,key 要唯一，key的数据类型（数字、字符串）
//key对应的值：类型可以为：string int array boolean float
$newsList3 = array(
	0=>'new0',
    1=>'new1',
    2=>'new2',
    3=>'new3',
)
    echo '<br>'
    print_r($newsList3)//简洁的输出数组
//为数组添加元素：
    $newsList3[]='new4';
	$newsList3[11]='new5';
//修改元素的值
	$newsList3[11]='new5-5';
//删除数组的元素unset---(unset是销毁变量)
	unset($newsList3[11])//
//获取元素的值
	$newsList3[11]
//遍历数组----1/不需要key值     2、需要key值
     foreach($newsList3 as $value){
         echo '<br>'.$value
     }
	  foreach($newsList3 as $key =>$value){
          echo '<br>'.$key .'=>'.$value
      }

```

**二维数组**

```php	
<?php
    $news = array('05-17','news1','miaov.com');
	print_r($news)
    echo $news[0];
	$news2 = array(
        'time'=>'05-17',
        'title'=>'new1',
        'link'=>'miaov.com',
	)
    $newsList = array(
    	array(
            'time'=>'05-17',
            'title'=>'new1',
            'link'=>'miaov.com',
            'isNew'=>'yes'
        ),
        array(
            'time'=>'05-18',
            'title'=>'new1',
            'link'=>'miaov.com',
        ),
        array(
            'time'=>'05-19',
            'title'=>'new1',
            'link'=>'miaov.com',
        ),
    )
        print_r($newsList);
	//添加新闻
	$newsList[] = array(
    	array(
            'time'=>'05-17',
            'title'=>'new1',
            'link'=>'miaov.com',
        )
    )
    //修改数组数据
    $newsList[0]['isNew']='yes'
```

**定义常量**---通常大写，合法的常量名以字母或下划线开始，后面跟任何字母、数字或下划线，常量值必须是标量数据类型数据或NULL

```php	
//define(name,value,[false/true])
define('USERNAME','root');
var_dump(defined('USERNAME'));//检查常量是否定义,用define：true表明已定义

$user= 'root';
var_dump(isset($user));//检查变量是否定义：用isset($变量名)；true表明已定义
```

**<font color='red'>运算符</font>**

```php
=  赋值运算符
-	减法
+	加法
*	乘法
/	除法
%  取余
```

#### 自动类型转换规则

* 布尔类型参与运算时：true转整数1，false转整数0

* Null参与算术运算时，被转换成整数0；

```php
echo 1+true
echo "<br>"
echo 1+1.0
var_dump(1+1.0)
echo '2017miaov'+1;
var_dump(true&&true);
var_dump(''&&true)
```

* 浮点数和整数算术运算，整数转浮点再运算

* 参与算术运算的字符串，只有以数字开头的字符串才会被认作数字可转，否则被转0

* 字符串连接运算时，整数、浮点数转字符串再运算
* 逻辑运算时：
  * 空字符串‘ ’，字符串‘0’，整数0，浮点数0.0，NULL以及空数组将被转换成布尔型FALSE
  * 其他的数据将被转换成布尔型TRUE

#### 检查数据类型

* is_bool
* is_string
* is_int
* is_integer
* is_long
* is_double
* is_float
* is_real
* is_numeric
* is_scalar
* is_array
* is_object
* is_recource

```php
//字符串转int类型
//方法一：
$str = '2017miaov';
var_dump($str);
$int1=(int)$str;
var_dump($int1);
//方法二：
$int2= intval($str);
var_dump($int2)
//方法三：
var_dump(settype($str,'int')); 
var_dump($str)
```

#### 流程控制语句

* 条件控制结构(if   、switch)
* 循环结构 (while  、do ...while、for)
* 程序跳转和终止语句(break、continue、exit/die)

```php
<?php
    $status =2;
if($status == 0){
    echo "请先登录"；
}elseif($status ==2){
    echo "已被禁言"
}else{
    echo "欢迎登录";
    
 switch(exp){
     case val1:
         语句块1;
         break;
     case val2:
         语句块2;
         break;
     default:
         语句块n;
 }
    
  while(exp){语句块}
  do{语句块}while(exp)
      
  for(exp1;条件表达式2；表达式3){语句块}
    //for
    for($i=0;$i<10;$i++){
        echo $i.'<br>';
    }
    //while
    $i=0;
    while($i<10){
        echo $i.'<br>';
        $i++;
    }
    //do...while
    $i=0;
    do{
       echo $i.'<br>';
        $i++; 
    }while($i<11)
```

**break:**结束foreach、for、while 、do-while或者switch结构的执行

**continue:**在循环结构里，用于跳出本次循环中剩余的代码并开始执行下一次循环

**exit/die:**输出一个消息并退出当前脚本

#### 定义函数

```php
function 函数名（$param1,$param2,...$param=默认值){
    函数体
    return 返回值；
}
 函数名（$param1,$param2,...$param=默认值)
     
 function calculator($num1,$num2,$op){
     if(!is_numeric($num1) || !is_numeric($num2)){
         echo '数值不符合要求！'
     }else{
         switch ($op){
             case '+':
                 echo $num1+$num2;
                 break;
             case '-':
                 echo $num1-$num2;
                 break;
             case '*':
                 echo $num1*$num2;
                 break;
              case '/':
                 if($num2 == 0){
                     echo '除数不能为0'；
                     break;
                 }
                 echo $num1/$num2;
                 break;
             default:
                 echo '未知运算符'
         }
     }
 }
//如果需要返回值就用return， 就不用break了。
calculator(10,2,'/');
$rest =calculator(10,2,'/');
if($rest ===false){
    echo '出错了';
}else{
    echo $rest;
}
//改写return
function calculator($num1,$num2,$op){
     if(!is_numeric($num1) || !is_numeric($num2)){
         //echo '数值不符合要求！'
         return ['code'=>1,'msg'=>'数值不符合要求']
     }else{
         switch ($op){
             case '+':
                 return ['code'=>0,'result'=>$num1+$num2]
                
             case '-':
                 return ['code'=>0,'result'=>$num1-$num2]
                
             case '*':
                 return ['code'=>0,'result'=>$num1*$num2]
                 
              case '/':
                 if($num2 == 0){
                     return ['code'=>1,'msg'=>'除数不能为0'];
                 }
                return ['code'=>0,'result'=>$num1/$num2]
                
             default:
                  return ['code'=>1,'msg'=>'未知运算符']
         }
     }
 }

calculator(10,2,'/');
$rest =calculator(10,2,'/');
if($rest['code'] != 0){
    echo $rest['msg'];
}else{
    echo $rest['result'];
}
```

#### 类

```php
class 类名{//大驼峰命名
}
class Comment{
    private $username;
    public $content;
    public function setUsername($username){
        $this->username=$username;
    }
    public function getUsername($username){
        return $this->username;
    }
}
class CommentBook{
    const FilePath='commentBook.txt';
    public function getCommentList(){
        return unserialize(file_get_contents(self::FilePath));
    }
    public function write($commentData){
        $commentList = $this->getCommentList();
    }
}
$commentBook = new CommentBook();
echo $commentBook::FilePath;//访问类常量
```

* 定义类变量
  * public $var1
  * protected $var2
  * private   $var3
  * const 常量名称 = 值

* 定义类方法（类的函数）非静态
  * public function 函数名1（）{.....}
  * protected function 函数名2（）{.....}
  * private function 函数名3（）{.....}
  * function 函数名4（）{.....}

* 类内获取类变量（非静态）
  * $this->变量名称

* 类内获取类常量
  * self::常量名称

* 类内调用类方法（非静态）
  * $this->函数名（....)

#### 对象

```php
$comment = new Comment();
var_dump($comment);
$comment->username='miaov';
echo $comment->username;

//设置数据
$comment->setUsername('miaov');
echo $comment->getUsername();

//设置数据
$comment->set('username','miaov');
echo $comment->get('username')
```

**set方法**

```php	
class Comment{
    private $username;
    public $content;
    public function setUsername($username){
        $this->username=$username;
    }
    public function getUsername($username){
        return $this->username;
    }
    public function set($name,$value){//非public属性，通用设置获取方法（private $username）
        $this->$name=$value;
    }
    public function get($name){
        return $this->$name;
    }
}
```

#### 魔术方法

```php
public function __set()set($name,$value){
    $this->$name=$value;
}
public function __get($name){
    return $this->$name;
}
//应用
$comment = new Comment();
$comment->username='miaov';
echo $comment->username;
```

#### 定义类属性（静态）

```php
class 类名{
    public static $变量1；
    protected static $变量1；
    private static $变量1；
    static $变量1；
}
//实例
class Tools{
    public static $titleSuffix='miaov';
    public $test ='test';
    
    public function parseTitle($title){
        self::parseTitle2('title')//**类内调用类方法（静态）**self::函数名（...)
        return $title.'-'.self::$titleSuffix;//在类内调用静态属性
        
    }
    public static function parseTitle2($title){//静态方法不能调用非静态属性，因为非静态属性需要实例化，需要放到对象里，静态的方法也不能调用非静态的方法
        $this->test;//会报错
        $this->parseTitle（）;//会报错
        return $title.'-'.self::$titleSuffix;//在类内调用静态属性
    }
}
//类外获取类属性（静态）
//类名：：$变量名称
Tools::$titleSuffix;
Tools::parseTitle2('vip')
```

**调用静态属性  ：self::$变量名称**

**静态方法不能调用非静态属性，因为非静态属性需要实例化，需要放到对象里**

**，静态的方法也不能调用非静态的方法**

**类内调用类方法（静态）**self::函数名（...)

**类外调用类方法**类名：：函数名（...)

<font color=red>能够拿起来就用的就用静态方法。工具类方法都用静态方法来实现</font>

#### 构造方法--用来完成类初始化的工作

```php
//如果需要用来完成初始化工作就需要显式声明构造函数
function __construct(){
    //初始化工作
    //可以传参，设置默认参数值，使用类的属性或方法函数
}
//实例
class Page{
    public $page;
    public $totalPage;
    public $link;
    
    public function __construct($totalPage,$link,$page=1){
        $this->page=$page;
        $this->totalPage=$totalPage;
        $this->link=$link;
    }
}
$pager =new Page(10,'http://miaov.com');
print_r($pager);
```

#### 析造方法

-----对象在内存中被销毁前自动调用

```php
function __destruct(){
    //对象销毁前的工作，不能传递任何参数。
}
```

#### 继承extends

* 子类只能继承一个父类
* 子类继承父类所有公有和受保护的属性和方法
* 除非子类覆盖了父类的方法，被继承的方法都会保留其原有的功能

```php
//实例
class BaseClass{
    public $user;
    public function error(){
        echo "404<br>";
    }
    public function __construct(){
        echo "验证登录";
    }
}
class SubClass extends BaseClass{
    public function __construct(){
        //子类使用父类的构造函数
        parent::__construct();
        echo "验证权限";
    }
    public function test(){
        $this->user;
        $this->error();
    }
    
    public function error(){
        echo 'error'
    }
}
//构造方法 的继承

$subClass = new SubClass();//如果子类没有构造函数继承父类构造函数，子类有构造函数引用子类构造函数

```

**面向对象是以对象为中心，事务流程抽象化，对象是一些属性和有权对这些属性进行操作的方法的封装体，面向对象的思想去编程或解决问题：**



* 有哪些对象
* 对象有哪些属性和方法
* 如何调用这些属性和方法

**面向过程的思想开发过，是以事件为中心的编程思想，也就是安装事务的流程步骤编程**

php文件的引用方式：

* include require
* include_once require_once

