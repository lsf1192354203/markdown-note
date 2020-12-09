### **vue动态绑定class的几种方式**

```css
:class="{ 'active': isActive }"
```

```js
第一种（用逗号隔开）
:class="{ 'active': isActive, 'sort': isSort }"
第二种（放在data里面）
//也可以把后面绑定的对象写在一个变量放在data里面，可以变成下面这样
:class="classObject"
data() {
  return {
    classObject:{ active: true, sort:false }
  }
}
第三种（使用computed属性）
:class="classObject"
data() {
  return {
    isActive: true,
    isSort: false
  }
},
computed: {
  classObject: function () {
    return {
      active: this.isActive,
      sort:this.isSort
    }
  }
}
```

**数组形式**

```js
:class="[isActive,isSort]"
data() {
  return{
    isActive:'active',
    isSort:'sort'
  }
}
```

**数组与三元运算符结合方式**

```js
:class="[isActive?'active':'']"
或者
:class="[isActive==1?'active':'']"
或者
:class="[isActive==index?'active':'']"
或者
:class="[isActive==index?'active':'otherActiveClass']"
```

**动态绑定style**

```js
<div class="control-panel">
      <span class=open :style="{'backgroundImage': 'url(' + (this.offline ? offlineIcon1 : isOpened == 1 ? openedIcon1 : closedIcon1) + ')'}" @click="toggle(1)">开窗帘</span>
      <span class=pause :style="{'backgroundImage': 'url(' + (this.offline ? offlineIcon2 : isOpened == 2 ? openedIcon2 : closedIcon2) + ')'}" @click="toggle(2)">暂停</span>
      <span class=close :style="{'backgroundImage': 'url(' + (this.offline ? offlineIcon3 : isOpened == 3 ? openedIcon3 : closedIcon3) + ')'}" @click="toggle(3)">关窗帘</span>
    </div>
```

```js
<span @click="togle">
    <img :src=" this.isTrue ? srcs : nosrc" alt="">
</span>
 
export default{
    data(){
        return{
            isTrue:false,
            srcs:require('../images/icon-up@2x.png'),
            nosrc:require('../images/icon-down@2x.png')
        }
    },
    methods:{
        togle(){
            this.isTrue = !this.isTrue
        }
    }
}
```

