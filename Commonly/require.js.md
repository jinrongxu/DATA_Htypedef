[toc]
### require
为什么使用require.js
- 首先一个页面如果在加载多个js文件的时候，浏览器会停止网页渲染，加载文件越多，网页失去响应的时间就会越长；
- ==其次，由于js文件之间存在依赖关系==，==因此必须严格保证加载顺序==，当依赖关系很复杂的时候，代码的编写和维护都会变得困难。

require.js 优点
- 异步加载js模块，防止阻塞页面，避免网页失去响应；
- 有效的管理模块之前的依赖，便于代码的编写和维护。<br>
**requireJS 是什么**
-  require.js是一个JavaScript 模块加载器；采用AMD规范，它非常适合在浏览器中使用
- require.js 是一个js文件，直接使用script标签链接就可以。
node.js服务器 ——> common.js ——>同步加载

### 使用
1、官网下载新版本，引入页面加载。
http://www.requirejs.cn/
```
<script src="js/require.js" defer async="true" ></script>
```
==注：async属性异步加载。IE9不支持async，所以把defer也写上。==
2、加载require.js以后，下一步加载自己代码，也就是入口，可以叫主模块。(data-main)
```
<script src="js/require.js" data-main="js/main.js"></script>

<!DOCTYPE html>
<body>
    <script>
       require(['./src/index.js']);
    </script>
    <p>index.html</p>
    //入口文件 require.js 在加载的时候会检查data-main 属性:
    <script src="./src/require.js" data-main="./src/index.js"></script>
</body>
</html>
```
### 语法
require([模块1，模块2，…],function(){}) //引入模块

- 第一个参数：Array 依赖的模块，即使只有一个模块也必须写成数组，不能省略 （路径相对页面去查找）

==注：1>模块是用路径引入的，路径相对于页面（index.html）所在的位置查找==

- 第二个参数：function 回调函数功能

require.config 配置模块
- 第一种：逐一指定路径。
```
require.config({
    paths:{ 
        //起别名
        "jquery":"相对于页面查找的路径",
        "swiper":"相对于页面查找的路径",
        ...
    }
})
```
- 第二种：改变基目录（baseUrl）。

```
require.config({
    baseUrl: "./src/js/lib",
    paths:{
        //起别名
        "jquery":"jquery.min",
        "swiper":"swiper.min",
        ...
    }
})
```
==注意：文件不需要带后缀名.js，require.js会自动追加后缀。==

### AMD模块的写法
- require.js加载的模块必须采用AMD规范；
- 使用define()函数来定义模块。

1. 如果一个模块不依赖其他模块，那么可以直接定义在define()函数之中。
```
// math.js
define(function(){
    var add = function (x,y){
        return x+y;
    };
    return {
        add: add
    };
);
```

加载方法如下：
```
// main.js
require(['math'], function (math){
    alert(math.add(1,1));
});
```

### 加载非规范的模块
require.config()接受一个配置对象，这个对象除了有前面说过的paths属性之外，还有一个shim属性，专门用来配置不兼容的模块。每个模块要定义

（1）exports值（输出的变量名），表明这个模块外部调用时的名称；<br>
（2）deps数组，表明该模块的依赖性。
```
require.config({
	paths:{
		'mui': './libs/mui.min',
		'dtpicker':'./libs/mui.dtpicker'
	},
	shim: {
        "picker": { //picker在mui执行完成之后再执行
            deps: ['mui'],  //deps数组，表明该模块的依赖性
        },
		 "dtpicker": { //picker在mui执行完成之后再执行
		    deps: ['mui'], //deps数组，表明该模块的依赖性
		},
    }
})
```


http-server搭建简易服务器 (Anywhere)
安装

```
npm install –g http-server

http-server -o 默认起的端口是：8080

http-server -p 9090 (设置指定端口号)
```


hs 是node模块http-server的简写命令，用于启动http服务器
-p 9090是设置端口的意思
-o 在默认浏览器里打开网址