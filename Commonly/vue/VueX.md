1.下载 安装

```
npm install vuex
```
什么是vuex

vuex是一个专为vue.js应用程序开发的状态管理模式。

主要应用于vue中**管理数据状态**的一个库。通过创建一个**集中的数据存储**，供程序中所有的组件访问

2.新建store.js

```
- 引入vue
- 引入vuex
- 注册Vue.use(Vuex)
- new Vuex.Store({//仓库的方法（是一个仓库，包含着vue应用的状态）
    state:{
       //状态，把需要多个组件之间共享的状态，可以理解为vue里的data 
    }
    mutations:{
        //方法的第一个参数是state，当然也有第二个参数。
        //第二个参数是通过从commit触发时传过来的参数
        //没有第三个参数，如需传多个复杂的数据，
        //可以放到一个对象里面通过第二个参数传过来
        方法1(state){},
        方法2(state){},
    },
    getters:{
        //在state中数据的基础上，获取新数据，类似于computed ,接受getter作为第二个参数
        //和计算属性一样，getter的返回会根据它的依赖被缓存起来，
        //只有当它的依赖发生了改变才会重新计算和
    },
    actions:{
        //异步操作
        方法(content){
            
        }
    }
  })
- 抛出实例
```
3.挂载
在main.js引用，挂载到Vue实例上，程序中的所有组件才能使用仓库中的状态


怎么在视图或者组件里获取store里面的共享状态

```
this.$store.state.属性名
```


修改Vuex的state的状态的唯一方法是提交mutation(mutation里面必须是同步函数)

```
提交mutation，在组件、视图里面通过
this.$store.commit("方法名")
```
mapState 
作用：是把写在vuex.store.state中的数据，慧姐映射到计算属性中
在计算属性里面

```
<span>{{count}}</span>
computed：{
    ...mapState(["count","arr"]), //数组里面的名字要与store中定义的一样
    countCom(){
        
    }
}
```
注意：如果计算属性还有其他函数，用逗号隔开
mapState是一个函数，这里就是调用这个函数

