### Webpack

**模块打包器**

*牵涉到两种模块和语法*：commonJS(可以理解成nodeJs的模块和语法) 、ES6

**webpack的基本语法和工作流程**

#### CommonJs语法------>webpack.config.js

```js
//引入path模块
const path = require('path');//nodejs内置的模块
module.exports={//导出一个模块--------为甚不用es6语法，因为webpack.config.js 是nodejs来跑的。
    entry://项目的入口文件
    {'./src/app.js'}//相对路径
    output:{//打包后文件放哪里，的配置
    	path:path.resolve(__dirname,'dist'),//绝对路径------这里需要path模块
        //__dirname,代表webpack.config.js所在的目录（根目录）
        filename:'main.js'//打包后的文件名
	}
}

///////////////////下一步 安装开发依赖webpack
//1、初始化package.json文件---因为我们需用npm来管理我们的项目依赖
		npm init -y
//2、安装项目开发的依赖
		npm i -D webpack webpack@^3.5.5
//运行的命令在“script”:里面声明。
		“dev":"webpack"//webpack 命令
		eg:假设webpack.config.js名字换为webpack.config.dev.js的话
		“dev":"webpack --config webpack.config.dev.js"
//3、运行一次打包
		npm run dev
        
```

**Webpack插件： 充当构建共建，创建文件**

```js
//插件  npm i -D html-webpack-plugin
//插件的应用 在webpack.config.js 文件配置
//1、引入html插件
	const htmlWebpackPlugin =require('html-webpack-plugin');
//2、使用：
	const HtmlWebpackPlugin = require('html-webpack-plugin');
   
    const path = require('path');
    module.exports={
        entry:'./src/app.js',
        output:{
            path:path.resolve(__dirname,'dist'),
            filename:'main.js'
        },
        plugins:[
            new HtmlWebpackPlugin()
        ]
    }
//3、再次打包
//4、插件里面配置参数
	new HtmlWebpackPlugin({
        filename:'aac.html',//打包后的html文件名。
        template:'src/index.html'//引用的模板
    })
```

**Webpack Loader：**

* loader就是webpack用来预处理模块的，在一个模块被引入之前，会预先使用loader处理模块的内容

* eg:利用react库

  * ```js
    npm i
    npm i -S react react-dom
    ```

  * 

* npm i -D babel-loader babel-core
* npm i  -D babel-preset-react@6.24.1    -----采用不同的预设处理不同的 内容

**Webpack开发服务器----devServer->专门用来给我们开发调试项目的，从此之后项目跑在服务器上，通过请求来访问我们的项目，同时也给我们的项目模拟一个更加真实的运行环境**

* 先下载一个webPack的devServer的库-------->npm i -D webpack-dev-server@2.8.2

* scripts:{"start":"webpack-dev-server --config webpack.config.js"}-------->先打包，然后在服务器跑打包后的文件

* 运行：npm run start

* 也可以自动打开浏览器，

  * ```js
    //配置
    devServer:{
        open:true,
        port:8090
    }
    ```

    

**引入CSS样式**

```js
//我们的webpack会把一切资源都当做模块
import './main.css';
//webconfig.js内容
module:{
        rules:[
            {
                test:/\.js$/,
                use:[{
                    loader:'babel-loader',
                    options:{
                        presets:['react']
                    }
                }]
            },
            {
                test:/\.css$/,
                use:['style-loader','css-loader']
            }
        ]
    },
 //npm i -D css-loader@0.28.7
 //npm i -D style-loader@0.19.0
 //处理顺序，先处理css-loader ,再处理style-loader       
```

**引入图片---->npm i -D file-loader@1.1.5**

* ```js
  {
    test:/\.jpg$/,
        use:['file-loader']
  }
  ```
**下载：npm i -D url-loader@0.6.2**
* ```js
  //使用url-loader引入图片
  //增强版的file-loader
  {
      	test:/\.(jpg|png|gif|jpeg)$/,
          use:[
              {
                  loader:'url-loader',
                  options:{
                      limit:10000 
                  }
              }
          ]
  },
  ```

**引入字体**

```js
/*
css-loader :处理css文件中出现的url，会自动帮你引入里面要引入的模块
*/
/*
file-loader:
	1.把你的资源移动到输出目录
	2.返回最终引入资源的url
*/
{
    test:/\.(ttf|eot|woff|woff2|svg)$/,
     use:['file-loader']
}
//引用第三方字体
npm i -S font-awesome@4.7.0
```

**模块化**

```js
    test:/\.css$/,
    use:[
        'style-loader',
        {
            loader:'css-loader',
            options:{
                module:true//开启模块化
            }
        }

    ]
import style from './common/style/main.css'
```

```js
//排除模块化，第三方的引用框架如：bootstrap

     		{
                test:/\.css$/,
                use:[
                    'style-loader',
                    {
                        loader:'css-loader',
                        options:{
                            options:{
                            module:true,//开启模块化
                            //localIdentName:'[hash:base64]'默认
                            //localIdentName:'[hash:base64:6]'默认
                            //localIdentName:'[path]-[name]-[local]-[hash:base64:6]'默认
                            localIdentName:'jkl'//更改类的名字
                        	}
                        }
                    }
                    
                ],
                exclude:[
                    path.resolve(__dirname,'node_modules'),
                    path.resolve(__dirname,'src/common')
                ]
            },
            {
                test:/\.css$/,
                use:[
                    'style-loader','css-loader'
                   
                ],
                include:[
                    path.resolve(__dirname,'node_modules'),
                    path.resolve(__dirname,'src/common')
                ]
               
            },
```

**使用less和scss**

```js
//使用scss
npm i -D sass-loader node-sass
npm uninstall sass-loader // 卸载当前版本
 
npm install sass-loader@7.3.1 --save-dev
//使用less
npm i -D less-loader@4.0.5 less@3.0.0-alpha.3
```

**babel **

* 是一款非常强大的javascript编译器，可以将es6转es5,
* babel 运行

```js
npm init -y
npm i -D babel-cli@6.26.0
npm run ./node_modules/.bin/babel src/app.js
/*"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "babel":"node_modules/.bin/babel src/app.js"//如果babel未安装到全局的话
  },
      npm run babel */
```

* babel插件和预设（babel的运行将依赖插件没有了插件，babel将一无是处

  * ```js
    npm i -D babel-plugin-transform-es2015-arrow-functions
    
     "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        
        "babel": "node_modules/.bin/babel src/app.js --plugins transform-es2015-arrow-functions"
      },
    npm i -D babel-plugin-transform-es2015-classes
     "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "babel": "node_modules/.bin/babel src/app.js --plugins=transform-es2015-arrow-functions,transform-es2015-classes"
      },
    ```

  * 解决办法-1---.babelrc（script标签里面的babel：太长）

    * ```js
      babelrc文件内容
      {
          "plugins": [
              "transform-es2015-classes",
              "transform-es2015-arrow-functions"
          ]
      }
       "scripts": {
          "test": "echo \"Error: no test specified\" && exit 1",
          "babel": "node_modules/.bin/babel src/app.js"
        },
      ```

      

  * 解决办法2 、采用预设----》把一些相关的插件打包在一起

    * ```js
      npm i -D babel-preset-es2015
      babelrc文件内容
      {
          "presets": ["es2015"]
      }
      
      ```

    * 输出编译完 的内容

      * ```js
        //-o out/a.js---------将编译的文件输出到哪里
        "scripts": {
            "test": "echo \"Error: no test specified\" && exit 1",
            "babel": "node_modules/.bin/babel src/app.js -o out/a.js"//-o out/a.js
          },
        ```

      * 

* Babel-loader---->babel-loader处理内容其实就是交给babel去处理内容
  * babel-core:其实就是babel运行的核心代码，他就相当于我们写的babel的命令
  * babel是基于插件来运作的，如果想让它编译某些内容，就要安装相应的插件，如果插件很多又可以打包很多插件在一起变成一个预设，
  * 所以：options:{}用来专门配置预设的
  * **Babel**在运行的时候会自动检测一个叫.babelrc的文件
* 同时安装env preset---->npm i -D babel-preset-env  1.6.0
* 处理非标准化的es6语法：eg:   ...      npm i -D babel-plugin-transform-object-rest-spread

```js
{
    test:/\.js$/,
        use:[{
            loader:'babel-loader',
            options:{
                presets:['react','env'],
                plugins:['transform-object-rest-spread']
            }
        }]
},
```

**输出路径处理**

* 一、将index.html文件提出。

```js
output:{
        path:path.resolve(__dirname,'dist'),
        filename:'main.js'
    },
```

```js
output:{
        path:path.resolve(__dirname,'dist/assets'),
        filename:'main.js'
    },
```

```js
plugins:[
        new HtmlWebpackPlugin({
            filename:'../index.html',//可以配置成文件名字和路径信息
            template:'src/index.html'
        })
    ],
```

* 清除打包的目录------->npm i -D clean-webpack-plugin@0.1.17

  * webpack.config.js文件

    * ```js
      const CleanWebpackPlugin=require('clean-webpack-plugin');
      plugins:[
              new HtmlWebpackPlugin({
                  filename:'../index.html',
                  template:'src/index.html'
              }),
              new CleanWebpackPlugin(['dist'])
          ],
      ```

      

* 二、将字体文件分类

  * ```js
    {
        test:/\.(ttf|eot|woff|woff2|svg)$/,
            use:[
                {
                    loader:'file-loader',
                    options:{
                        name:'fonts/[name]_[hash:8].[ext]'//默认编码
                    }
                }
            ]
    }
    ```

    

* 三、将img分类

  * ```js
    {
        test:/\.(jpg|png|gif|jpeg)$/,
            use:[{
                loader:'url-loader',
                options:{
                    limit:10000,
                    name:'img/[name]_[hash:8].[ext]'//默认编码
                }
            }]
    },
    ```

    

* 四、将js分类

  * ```js
    output:{
        path:path.resolve(__dirname,'dist/assets'),
            filename:'js/main.js'
    },
    ```

    

* 五、publicPath

*  ```js
  //webpack.config.js文件里
  output:{
          path:path.resolve(__dirname,'dist/assets'),
          filename:'js/main.js',
          publicPath:'assets/'
      //它其实是个基础路径，他会为我们所有的资源都接上publicpath,所有资源的基础路径，而且一定是‘/'结尾
      },
  ```

* 此时、npm run start 显示异常，页面不见了

* npm run start ----->
  * 运行后资源依然可以打包，但是资源不会打包到我们本地，而是会放到内存里面，
    * 1、所以我们的devserver会到内存找内容，
    * 2、除此之外devserver还会到另外一个地方查找内容，

* * 如果内存找不到资源会到本地localhost:9000查找资源

  * ```js
    devServer:{
            open:true,
            port:9000,
            contentBase:'./src/common',
            publicPath:'/'//服务器打包资源后的输出路径
        }
    ```

  * 

### webpack.config.js

* 文件名对应关系

```js
entry:{
    rawLoader:'./src/rawLoader.js',
    jsonLoader:'./src/jsonLoader.js'
},
output:{
    path:path.resolve(__dirname,'dist'),
    filename:'[name].js'//name 对应的就是上面的rawLoader
}
```

* **raw-loader**:加载文件原始内容
  
* 加载指定文件，并以字符串的形式返回内容
  
* raw.txt---->内容：hello

* rawLoader.js--------->内容

  * ```js
    import content from './raw.txt';
    console.log(content);
    ```

  * 

* **webpack.config.js**

  * ```js
    //配置loader
    module:{
        rules:[
            //每一个规则就是一个对象
            {
                test:/\.txt$/,//当加载的是该类型的文件
                use:['raw-loader']//安装该loader npm i -D raw-loader 
            },
            {
                test:/\.json$/,
                use:['json-loader']
            }
        ]
    }
    ```

  * 

* **json-loader**----->加载json文件

  * 加载只是json数据文件，并以对象（解析后的json数据）的形式返回
  * webpack2.0以后已经内置了json-loader,和对json 后缀的文件的处理，所以不需要下载json-loader与配置
  * 针对非json后缀的，还是需要单独在rules中配置，但是不需要下载json-loader了

  * ```js
    //jsonLoader.js
    import data from './data.json'
    console.log(data)
    //data.json
    {
        "username":"mm",
         "age":30
    }
    ```

    

* **file-loader**--->生成文件到指定目录，并根据配置返回访问路劲（<font color=red>默认生成新文件的名称为源文件的MD5值</font>）

  * npm i -D file-loader

  * ```js
    //fileloader.js
    import img from './1.jpg'
    console.log(img);
    imgElement.src=img;
    ```

  * 

* babel-loader安装：npm i -D babel-loader babel-core babel-preset-env 

* **vue-loader**

  * 加载和转译Vue组件

  * ```js
    npm i -D vue-template-compiler@2.0.0
    ```

  * 

### 插件---->在webpack预处理，打包完成后执行

* 安装压缩插件：npm i -D uglifyjs-webpack-plugin

```js
const UglifyJSPlugin = require('uglifyjs-webpack-plugin')
plugins:[
    new UglifyJSPlugin()
]
```

* ExtractTextPlugin:提取分离成独立的css文件

```js
npm i -D extract-text-webpack-plugin
const ExtractTextPlugin = require('extract-text-webpack-plugin');
module.exports={
    module:{
        rules:[
            {
                test:/\.css$/,
                use:ExtractTextPlugin.extract( {fallback:'style-loader',use:'css-loader'} )
            }
        ]
    },
    plugins:[
        new ExtractTextPlugin('style.css')//style.css是生成后的css文件
    ]
}
```

* providePlugin:自动加载模块，而不必到处import 或require。eg:引入jquery库

```js
const webpack = require ('webpack')
module.exports={
    plugins:[
        new webpack.providePlugin({
            $:'./src/jquery.min',
            jQuery:'jquery'
        })
    ]
}
```

* commonsChunkPlugin:提取chunks之间共享的通用模块

```js
module.exports= {
    plugins:[
        new webpack.optimize.CommonsChunkPlugin({
            name:'verdor'//生成的文件名
        })
    ]
}
```

* 模块热替换---->webpack-dev-server

```js
npm i -D webpack-dev-server
```

