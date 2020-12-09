### react-router-dom 路由

##### react-router-dom 路由使用与核心源码解析

##### <https://gitchat.csdn.net/activity/5cf736f8f4cc8d19d1f81b4f?utm_source=so>

###  1、路由配置

##### 路由配置属性主要有 *path* 、*name* 、*component*

* path:组件相对路径
* name:组件路径别名
* component：组件地址

##### 路由配置中，路径匹配属性*exact*、*strict*

* exact:精准匹配，类型为布尔值，默认为true，false时表示普通匹配
```js
<Route  path="/"       name="index" component={Index}/>
<Route  path="/login"  name="detail" component={Login}/>
```

* strict:严格匹配，类型为布尔值，默认为false，为true时表示普通匹配

```js
<Route strict = {true}  path="/login"  name="index" component={Login1}/>
<Route strict = {true} path="/login/"  name="detail" component={Login2}/>
```

**综上所述**要想严格匹配，就需要将 exact 和 strict 都设为 true。
###  2、路由跳转
#### 路由跳转有两种方式：
* Link或者NavLink形式，实质是通过a标签链接跳转。<font color=red>区别：后者可以切换时改变样子，**用法如下:**</font>

  

![alt 文章目录](C:\Users\Administrator\Desktop\markdown\react-router-dom.jpg)

### 主要组件

React Router中的组件主要分为3类：

* 路由器，例如<BrouserRouter><HashRouter>

* 路由匹配器，例如<Route>和<Switch>

* 导航，例如<Link>,<NavLink>和<Redirect>

在Web应用程序中使用的所有组件都应从react-router-dom导入