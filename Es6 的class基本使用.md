class People{
    constructor(name,age){
        this.name=name;
        this.age=age;
    }
    say(){console.log("I say")}
    eat(){console.log("I eat")}
    static isHuman(obj){
        //console.log("isHuman")
        return obj instanceof People;
    }
}Es6 的class基本使用

##### Es5创建对象

```js
function Person(name,age){
    this.name=name;
    this.age=age;
    this.say=function(){
        console.log('会说话。。。')
    }
}
var p1=new Person("小明",20);
console.log(p1);
```

```js
function Person(name,age){
    this.name=name;
    this.age=age;
}
Person.prototype.say=function(){
    console.log("会说话")
}
var p1=new Person("小明",20);
p1.say();
console.log(p1.say());
```

##### Es6创建对象

```js
class Person{
    constructor(){
        this.name=name;
    	this.age=age;
    }
    //原型上面的方法
    say(){
        console.log('我会say'+this.name)
    }
}
var p1=new Person("小明",20);
console.log(p1);
console.log(typeof Person);
console.log(Person.prototype);
p1.say();
```

<font color=red>**class 注意事项**</font>

```js
//遍历原型上面的方法
//Object.keys(obj)一个表示给定对象的所有可枚举属性的字符串数组
 console.log(Object.keys(Person.prototype));//结果[]，说明是不可枚举的
class Student{};
var s = new Student();
```

<font color=red>**class 静态方法和继承**</font>

```js
//静态方法的创建
class People{
    constructor(name,age){
        this.name=name;
        this.age=age;
    }
    say(){console.log("I say")}
    eat(){console.log("I eat")}
    static isHuman(obj){
        //console.log("isHuman")
        return obj instanceof People;
    }
}
var p1 = new People("kemo",23);
console.log(People.isHuman(1));
console.log(People.isHuman(p1));
//静态属性
People.staticProps ="miaov";
console.log(People.staticProps)


```

<font color=red>**class 继承**</font>

```js
class People{
    constructor(name,age){
        this.name=name;
        this.age=age;
    }
    say(){console.log("I say")}
    eat(){console.log("I eat")}
    static isHuman(obj){
        //console.log("isHuman")
        return obj instanceof People;
    }
}
//coder 继承
class Coder extends People{
    constructor(name,age,money){
        super(name,age);
        this.money=money;
    }
}
var c1 = new Coder('zm',30,300);
console.log(c1);
c1.say();
//子类也能调用父类的静态方法
```

