### Vue教程（三）vue-cli 构建Vue项目后的打包和发布<https://www.jianshu.com/p/faec2866c9dd>

##### [vue-cli创建项打包后打开页面为空白的问题解决](https://www.cnblogs.com/facefront/p/10954799.html)

<font color=red>****

**最后总结一下：../dist   ./dist   /dist  dist**

**../dist:相当于在__dirname父目录下执行 CD dist**

**./dist:相当于在__dirname目录下执行 CD dist**

**/dist：和_dirname无关，在根目录执行 cd dist**

**dist:和_dirname无关，直接 CD dist的目录**</font>



**<font color=red>assetsPublicPath</font>**属性作用是指定编译发布的根目录，‘/'指的是项目的根目录 ，'./'指的是当前目录。



#### vue-cli 3.0版本没有webpack的配置

##### https://cli.vuejs.org/zh/config/#vue-config-js 【vue-cli配置】

需要手动创建一个vue.config.js



**registerServiceWorker**帮助做缓存

http server 模块-------------安装 npm i http-server  -g

快速开启一个服务在浏览器访问

```js
new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')
render:function(createElement){
    return createElement(App);
}
//createElement 函数是用来生成 HTML DOM 元素的，也就是上文中的 generate HTML structures，也就是 Hyperscript，这样作者才把 createElement 简写成 h。h是 Vue.js 里面的 createElement 函数，这个函数的作用就是生成一个 VNode节点，render 函数得到这个 VNode 节点之后，返回给 Vue.js 的 mount 函数，渲染成真实 DOM 节点，并挂载到根节点上
```

Vue.config.productionTip = false;生产环境配置的开启

vue组件：

 * 引入组件

 * 注册组件

 * 使用组件

 * ```js
   import App from ./app; //引入组件
   new Vue({
       el:"#app",
       template:'<App/>',//使用组件
       components:{App:App}//注册组件
   })
   ```

	* app.vue 以.vue结尾的。单文件组件（一个文件就是一个组件），**组件包含三个部分：**<template>模板</template>、<script>交互</script>、<style>样式</style>