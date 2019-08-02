[toc]
## 生命周期
###### 第一步
创建Vue对象

```
new Vue({
    el:"#app",
    template:"<span>{{grade}}</span>"
    data:{
        grade:"2019"
    }
})
```
###### 第二步
初始化，收集配置项

```
beforeCreate(){
    console.log(this.$el,this.$data,this.grade);
    //undefined,undexfined,undefined
}
```
###### 第三步
把配置项分配到实例上，没有当前挂载的元素（分配配置项到实例上）
```
created() {
        console.log("created")
        console.log(this.$el, this.$data, this.grade)
        //undefined, {__ob__: Observer}, "2019"
}
```
**注意**：
- 在生成dom之前，先确定是否挂载元素 <br>
1. 内部挂载 

```
new Vue({
    el:"#app"
})
```

2. 外部挂载

```
var vm=new Vue();
vm.$mount("#app")
```
- 是否存在模板字符串
- 编译模板，把data里面的数据和模板生成html **（如果有模板字符串，则生成模板字符串中内容，否则生成外部html）**

###### 第四步
生成dom节点（此时还没有生成html到页面上）
```
beforeMount() {
        console.log("beforeMount")
        console.log(this.$el, this.$data, this.grade)
        // <div id=""app><h2>{{grade}}</h2></div>,{__ob__: Observer}, "2019"
}
```

###### 第五步
dom节点生成，模板字符串内容添加到html页面中
```
mounted() {
        console.log("mounted")
        console.log(this.$el, this.$data, this.grade);
        //<span>2019</span></div>,{__ob__: Observer}, "2019"
}
```
**以上五步是将模板字符串的内容生成dom的过程**
###### 更新之前

```
beforeUpdate() {
  console.log("beforeUpdate")
  console.log(this.$el, this.$data, this.grade)       
}
```
###### 数据更新触发

```
updated() {
  console.log("update")
  console.log(this.$el, this.$data, this.grade)
}
```





