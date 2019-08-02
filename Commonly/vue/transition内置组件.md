 [toc]
#### transition内置组件
<transition>元素作为单个元素/组件的过渡效果，<transition>只会把过渡效果应用到其包裹的内容上，而不会额外渲染dom元素，也不会出现在检测过的组件层级中。
###### 用法

```
//简单元素
<transition>
    <div v-if="ok"></div>
</transition>
//动态组件
<transition>
    <components :is="view">
    </components>
</transition>
```

<transition>需要配合css一起使用
进入/离开
###### 进入：
- .v-enter 定义进入过渡开始状态
- .v-enter-to：定义进入过渡结束状态
- .v-enter-active:定义进入过渡生效的状态（从开始到结束的状态）
###### 离开
- .v-leave:定义离开过渡开始状态
- .v-leave-to:定义离开过渡的结束状态
- .v-leave-to-active：定义离开过渡生效时的状态
###### 自定义过渡类名
我们可以通过以下特性来自定义过渡类名：
- enter-class
- enter-active-class
- enter-to-class (2.1.8+)
- leave-class
- leave-active-class
- leave-to-class (2.1.8+)
他们的优先级高于普通的类名，这对于 Vue 的过渡系统和其他第三方 CSS 动画库，如 Animate.css 结合使用十分有用。