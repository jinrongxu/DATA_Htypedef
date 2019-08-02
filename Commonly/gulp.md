[toc]
# gulp
gulp是==前端开发==过程中一种基于流的代码构建工具，是==自动化项目==的构建利器。插件机制非常强大<br/>
流-->输入和输出<br>
### 自动化构建
自动化构建是将==源代码==利用工具==自动转换==成用户可以使用的目标的过程。==目标'在这里指的是js,css,html的集合==。
###### 自动化构建的优点
1.减少每一个文件的容量大小。<br>


```
HTML：站在结构的层面<br>
CSS：压缩<br>
Js：压缩<br>
图片：无损压缩<br>
```
2.尽量减少http请求

```
具体来说，就是合并。
Css文件，可以合并的就合并。
Js文件，可以合并的都合并。 
背景图片，合并，使用雪碧图 sprite。
前景图片，滚动加载、延迟加载。
```
### gulp

gulp是基于==Node.js==的自动任务运行器。可以==自动完成html、image、css和js==等文件的==检测、检查、合并、压缩、格式化==等，并==监听文件==在改动后重复指定的这些步骤。
##### gulp的优点
1.易于使用<br>
2.构建快速<br>
3.插件高质<br>
4.易于学习<br>
5.插件机制强大
##### gulp的安装

```
//本地安装
npm install gulp --save-dev//开发依赖包
//全局安装
npm install gulp -g
```
##### 下载插件

```
npm install gulp-sass gulp-uglify--sav-deve//多个插件同时下载
npm install gulp-less --save-dev//下载一个
在package.json 中写下插件，npm i直接下载插件
```
##### gulp的使用

```
//注册任务,用来定义一个gulp任务
gulp.task("任务名",function(){
     //逻辑具体任务
});
//任务名是一个字符串，执行的任务是一个回调函数（回调函数是一个函数作为另一个函数的参数）

//读文件，指定需要执行任务的文件
gulp.src("目标文件路径")

//输出文件
gulp.dest("输出的文件路径")

//管道
gulp.pipe()

//监听文件变更
gulp.task("任务名",function(){
    gulp.watch("监听文件目录",gulp.series("任务名","任务名"...)
})

//设置执行任务顺序(相当于同步)
gulp.series("任务名","任务名"...)

//设置执行任务顺序(相当于异步)
gulp.parallel("任务名","任务名"...)

//注册多个任务
gulp.task("任务名",gulp.series(""任务名","任务名"..."))
```

查找规则| 说明
---|---
* | 查找所有的文件
**| 匹配的0个或多个文件夹
{} <br> {jpg,png,gif}|匹配多个文件，或多个属性
！|非
####  gulp的常用插件

插件名 | 功能
---|---
gulp-concat | 合并文件(js/css)
gulp-rename | 文件重命名
gulp-webserver |开启服务（自动打开浏览器，自动刷新）
gulp-imagemin|图片压缩
gulp-rev|生成生成文件后缀


###### css方法

插件名 | 功能
---|---
gulp.sass | 编译sass
gulp.less | 编译less
gulp-clean-css|压缩css
gulp-autoprefixer|自动添加浏览器前缀

###### js方法

插件名 | 功能
---|---
gulp-babel|es6——>es5<br> (babel-core,babel-preset-env依赖)
gulp-uglify | 压缩js文件，不支持es6
row 2 col 1 | row 2 col 2


###### html方法

插件名 | 功能
---|---
gulp-htmlmin | 压缩html

###### gulpfile.js
```
//引入模块
var gulp = require('gulp');

//注册转换less的任务
gulp.task('less',function(){
    return gulp.src('src/less/*.less')
    .pipe(less()) //使用less对象进行编译
    .pipe(gulp.dest('src/css'))编译的的结果保存到目录
})

//注册转换sass的任务
gulp.task('sass',function(){
    return gulp.src("src/scss/*.scss")
    .pipe(sass()) //进行编译
    //自动处理浏览器前缀 
    .pipe(autoprefixer({
        browsers: ['last 2 versions', 'Android >= 4.0'], //浏览器版本
        cascade: true, //是否美化属性值 默认：true 
        remove:true //是否去掉不必要的前缀 默认：true 
    }))
    .pipe(gulp.dest('dist/'))
})

//注册合并压缩js的任务
gulp.task('js',function(){
    return gulp.src("src/js/**/*.js") //找到目标原文件，将数据读取到gulp的内存中
    .pipe(concat('build.js'))//合并临时文件
    .pipe(gulp.dest('dist/js/'))//输出文件到本地路径
    .pipe(uglify())//压缩文件
    .pipe(rename('build.min.js'))//重命名第一种情况
    .pipe(rename({suffix:'.min'})) //重命名第二种情况;suffix:后缀名
    .pipe(gulp.dest("dist/js/"))
})

//注册压缩html的任务
gulp.task('htmlMin', () => {
    //removeComments: true,//清除HTML注释
    //collapseWhitespace: true,//压缩HTML
    return gulp.src('index.html')
      .pipe(htmlmin({collapseWhitespace: true,removeComments: true,}))
      .pipe(gulp.dest('dist/'));
});

//开启服务
gulp.task('server',function(){
    return gulp.src('src')
    .pipe(webserver({
        port:9090, //端口号
        open:true, //自动浏览器
        livereload:true, //自动打开刷新
        proxies:[  //代理
            { source:'/api/find',target:'http://localhost:3000/api/find'}
        ]   
    }))
})

//开发坏境（串联）
gulp.task('dev',gulp.series('任务名','任务名'))

//线上环境（并联）
gulp.task('build',gulp.parallel('任务名','任务名'))
```











