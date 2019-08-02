[toc]
## webpack
### 概念
webpack是JavaScript应用程序的静态模块打包器（模块打包器）==遵循commonjs规范==。
webpack 可以将多种静态资源 js、css、less 转换成一个静态文件，减少了页面的请求。
### 安装

```
npm install webpack -g 
npm install webpack-cli -g 
//全局安装   v.4.0.0版本
```
### webpack配置文件
默认配置文件==webpack.config.js==<br>
当配置文件名并不是webpack.config.js时需要执行命令webpack --config webpack.dev.js
```
//webpack配置文件
module.exports = {
    //入口文件的配置项（不引报错）
    entry: './src/scripts/help_center.js', //以当前位置引入
    //出口文件配置项
    output: {
        path："",//编译后的出口路径
        filename:"",//编译后的文件名
    },
    //加载器
    module:{
        //各种规则
        //js,jsx
        rules:[{
          //正则匹配/\.文件后缀名/
          test:/\.(js|jsx)/,
          //加载器
          loader:"@babel-loader",
          //js文件需要在options中配置项
          options:{//配置项
            //babel-loader@8.0.0版本
            presets:["@babel/preset-env"]
          }
        },{
            //css
            test:/\.css$/,
           //执行顺序是从右向左因此顺序不能改变
           use:["style-loader","css-loader"]
        },{
            //jpg,png,gif
            test:/\.(jpg|png|gif|jpeg)$/,
            use:"url-loader",
            options:{
                limit:字节        
            }
            //url-loader 功能类似于 file-loader
            //但是在文件大小（单位 byte）低于指定的限制时，可以返回一个 DataURL。
            //否则直接返回图片
        },{
           //iconfot存在必须存在css的加载器
           test:/\.(woff|eot|ttf|svg)/,
           loader:"file-loader"
        },{
        //scss
             test:/\.scss$/,
           //执行顺序是从右向左因此顺序不能改变
           use:ExtractWebpackPlugin.extract({
               use:["css-loader","sass-loader"],//执行所需加载器
               fallback:"style-loader"//最后一项加载器
           })
        }]
    },plugins:[
        //抽离css文件
        new ExtractWebpackPlugin("./css/index.css"),
        //清空构建文件
        new cleanWebpackPlugin()
        //快速构建html
        new HtmlWebpackPlugin({
            template:"index.html",
            filename:"app.html",
            title:"首页",//需要在index.html的title标签中设置<title><%=htmlWebpackPlugin.options.title%></title>
            minify: {
                removeAttributeQuotes: true, // 去除引号
                collapseWhitespace: true, //去除空格
                removeComments: true, //去除注释
                removeEmptyAttributes: true //去除空属性
            }
        }),
    ],
    devServer:{
        port:端口号,
        host:"localhost",
        open:true,//自动打开
        inline:true,//自懂更新,
        before(app){//拦截相当于gulp的middleware
            app.get("接口",(req,res,next)=>{
                res.send(数据)
            })
        },
        proxy:{//代理相当于gulp的proxies
            "接口":"地址栏地址"
        }
    },
    resolve:{
        alias:{
            "@":"./src/css",
            "index$":"./scss/index.scss"//$是精确匹配文件
        },
        extensions:[".js",".css",".scss"]//配置后import导入文件时可以省略后缀名
    }
}

```
### 四个核心概念
- 入口（entry）
- 出口（output）
- 加载器（loader）
- 插件（plugins）  
#### entry（入口）
entry：String |Array|Object（三种数据类型，前两种是单入口文件，后一种是多入口文件）

```
//单入口文件 String
module.exports={
    entry:require("path").join(__dirname,"入口文件路径")
}
//单入口文件 Array
module.exports={
    entry:[require("path").join(__dirname,"入口文件路径"),
    require("path").join(__dirname,"入口文件路径")
    ]
    //将多个文件输出成一个文件
}
//多入口文件 Object
module.exports={
    entry:{
    "key1"::require("path").join(__dirname,"入口文件路径"),
    "key2":require("path").join(__dirname,"入口文件路径")
    }
    //两个文件均为入口文件，只不过是运行的方式不同
}
```
#### output（出口）
output默认编译的文件是dist/main.js
```
//改变出口位置
output:{
    path:编译后文件夹
    filename:"[name]-[hash].js"//编译后的文件hash属于缓存
}

```
#### loader（加载器）
编译js
1. 安装

```
npm install babel-loader@8.0.0-beta.0 @babel/core @babel/preset-env webpack

npm install babel-loader babel-core babel-preset-env webpack
```
不同版本的babel-loader所依赖的模块不同<br>
v.8.0.0以上版本所需依赖是@babel/core和@babel/preset-env<br>
v.8.0.0一下版本所需要的依赖是babel-core babel-preset-env
**使用babel通常需要配置.babelrc文件**因此在.babelrc文件中需要设置

```
{
    presets:[
        "@babel/preset-env"或者babe;-preset-env
    ]
}
```
其实在webpack中存在另一种方法设置

```
module:{
    test:/\.(js|jsx)$/
    loader:"babel-loader",
    options:{
        presets:["@babel/preset-env"]
    }
}
```
#### plugins（插件）
1. scss/css抽离
###### 下载插件
```
npm i extract-text-webpack-plugin@next
//extract-text-webpack-plugin必须下载下一个版本4.0.0版本
```
###### 安装插件

```
require("所用插件")
```
###### 使用插件
详细使用在 loader

```
 //使用
  {test:/\.scss$/,
           //执行顺序是从右向左因此顺序不能改变
           use:ExtractWebpackPlugin.extract({
               use:["css-loader","sass-loader"],//执行所需加载器
               fallback:"style-loader"//最后一项加载器
           })
  }
```



###### 调用插件
由于插件可以携带参数/选项，你必须在 webpack 配置中，向 plugins 属性传入 new 实例。
```
//格式
plugins:[
        //抽离css文件
        new ExtractWebpackPlugin("./css/index.css"),
        //清空构建文件
        new cleanWebpackPlugin()
        //快速构建html
        new HtmlWebpackPlugin({
            template:"index.html",
            filename:"app.html",
            title:"首页"//需要在index.html的title标签中设置<title><%=htmlWebpackPlugin.options.title%></title>
        }),
    ]
```
### devServer (起服务)
###### 下载

```
npm i webpack-dev-server
```

执行命令 webpack-dev-server,默认的文件是webpack.config.js
```
devServer:{
        port:端口号,
        host:"localhost",
        open:true,//自动打开
        inline:true,//自懂更新,
        before(app){//拦截相当于gulp的middleware
            app.get("接口",(req,res,next)=>{
                res.send(数据)
            })
        },
        proxy:{//代理相当于gulp的proxies
            "接口":"地址栏地址"
        }
    }
```
