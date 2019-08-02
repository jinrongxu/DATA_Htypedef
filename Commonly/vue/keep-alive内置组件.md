[toc]
#### keep-alive内置组件
- keep-alive是Vue.js的一个内置组件。
- <keep-alive> 包裹**动态组件**时，==会缓存不活动的组件实例，而不是销毁它们。==
- 它自**身不会渲染一个 DOM 元素**，**也不会出现在父组件链中**。
- 当组件在 <keep-alive> 内被切换，它的** activated **和 **deactivated **这两个生命周期钩子函数将会被对应执行。
- 它提供了include与exclude两个属性，允许组件有条件地进行缓存。

###### 原理
其实就是在created时将需要缓存的VNode节点保存在this.cache中／在render时,如果VNode的name符合在缓存条件（可以用include以及exclude控制），则会从this.cache中取出之前缓存的VNode实例进行渲染。

###### 用法
```
<!-- 基本 -->
<keep-alive>
  <component :is="view"></component>
</keep-alive>
//这里的component组件会被缓存起来。
<!-- 多个条件判断的子组件 -->
<keep-alive>
  <comp-a v-if="a > 1"></comp-a>
  <comp-b v-else></comp-b>
</keep-alive>

<!-- 和 `<transition>` 一起使用 -->
<transition>
  <keep-alive>
    <component :is="view"></component>
  </keep-alive>
</transition>
```
**注意**:<keep-alive> 是用在其一个直属的子组件被开关的情形。如果你在其中有 v-for 则不会工作。如果**有上述的多个条件性的子元素**，<keep-alive> **要求同时只有一个子元素被渲染**。
###### Props

- include - 字符串或正则表达式。只有名称匹配的组件会被缓存。
- exclude - 字符串或正则表达式。任何名称匹配的组件都不会被缓存。
- max - 数字。最多可以缓存多少组件实例。

 include 和 exclude 属性允许组件有条件地缓存。二者都可以用逗号分隔字符串、正则表达式或一个数组来表示：


```
<!-- 逗号分隔字符串 -->
<keep-alive include="a,b">
  <component :is="view"></component>
</keep-alive>

<!-- 正则表达式 (使用 `v-bind`) -->
<keep-alive :include="/a|b/">
  <component :is="view"></component>
</keep-alive>

<!-- 数组 (使用 `v-bind`) -->
<keep-alive :include="['a', 'b']">
  <component :is="view"></component>
</keep-alive>
```

**匹配首先检查组件自身的 name 选项，如果 name 选项不可用，则匹配它的局部注册名称 (父组件 components 选项的键值)。匿名组件不能被匹配。**

max最多可以缓存多少组件实例。一旦这个数字达到了，在新实例被创建之前，已缓存组件中最久没有被访问的实例会被销毁掉。

```
<keep-alive :max="10">
  <component :is="view"></component>
</keep-alive>
```
