# vue
**vue是一个渐进式框架，轻量，易于上手**<br>
vue是MVVM的一个框架
- M(数据)
- v(视图)
- VM(数据双向绑定)

[toc]
### 引入
```
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

```
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```
### 使用
vue 是一个构造函数的，需要实例化<br>
**{{}}最好放在双标签内**
```
<p>{{flag}}</p>

var vm=new Vue({
        el:"#app",   //el上的是挂载元素,把Vue实例挂载在app上
                     //一般情况下一个页面只有一个实例，因此使用id选择器
        template:``,//模板字符串，会替换挂载元素
        data:{      //数据是一个对象,配置项的名字不可以随意修改
                   //获取data里的数据vm.数据名
         flag:flag 
        },methods:{
            方法名(){//this指当前的实例
                具体方法
            }
        }
})
```
### 指令 v-

指令 | 说明
---|---
v-text       |**只能解析文本**，解析出来的文本作为标签的内容，不能解析html标签
v-html | **解析标签**
v-show="true" | 控制元素的显示
v-show="false"|控制元素的隐藏
v-on:事件名称|绑定事件 **可以简写为@事件名称**
v-bind:属性|绑定动态事件 **可以简写为:属性**
v-for|循环
v-model|实现双向绑定，一般用于表单元素
v-cloak|元素上直到关联实例编译结束
v-pre|会跳过这个元素和子元素的编译（不编译了）{{}}
v-if|根据表达式的值真假渲染元素
v-else|不需要表达式(必须使用v-if或v-else-if)
v-else-if|判断条件(必须使用v-if或v-else-if)

###### **v-text**

```
<p v-text="msg"></p>--><span>12345</span>//不可以加载标签
new Vue({
       el: "#app",
       data: {
        msg: "<span>12345</span>"
   }
})
```

###### **v-html**

```
<p v-html="msg"></p>-->12345
new Vue({
     el: "#app",
     data: {
     msg: "<span>12345</span>"
  }
})
```
###### **v-on：事件名称**

事件 | 说明
---|---
@click | 点击事件
@click.prevent | 阻止默认事件
@click.stop|阻止冒泡事件
@click.captrue|捕获阶段触发的
@click.stop|阻止冒泡
@click.self|只触发自身事件（父级也需要设置self）
@click.once|只触发一次，下一次会继续触发事件
@click.left|鼠标左键触发
@click.right|鼠标右键触发
@click.middle|鼠标中键触发
@keyup.enter/@keyup.13|键盘按下键值为13或者enter时会执行

###### v-bind：属性

```
属性名="变量名"//按字符串解析
:属性名="变量名"//按变量解析
```
###### v-for

```
<ul v-for="(item,index,key) in list">
       <li>
          <span>{{item.name}}</span>
          <span>{{item.age}}</span>
      </li>
 </ul>
 const vm = new Vue({
        el: "#app",
        data: {
          list: [
          {name: "zs",age: 12}, 
          {name: "ls",age: 15}, 
          {name: "ww",age: 18},
          {name: "zl",age: 20}
          ]
   }
})
```
**遍历对象(value,key,index)**
：key="唯一标识"
- value-->每一项的value值
- key -->每一项的key
- index-->下标

**遍历数组(item,index,key)**
- item-->数组里得每一项
- index -->下标
- key-->无

**遍历数字(item,index,key)**

- item-->数组里得每一项
- index -->下标
- key-->无
###### v-model

```
<input type="text" v-model="val">
<p>{{val}}</p>

//原生
<input type="text" @input="val=$event.target.value">
<p>{{val}}</p>
```
###### v-cloak
在css样式里需要编译

```
<style>
[v-cloak] { display: none }le
</style>
```
在实例的元素中

```
<div id="app" v-cloak></app>
```












