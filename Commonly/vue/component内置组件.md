# component内置组件
## component
- Props：

1. is - string | ComponentDefinition | ComponentConstructor
1. inline-template - boolean
- 用法：

渲染一个“元组件”为动态组件。依 is 的值，来决定哪个组件被渲染。


```
<!-- 动态组件由 vm 实例的属性值 `componentId` 控制 -->
<component :is="componentId"></component>

<!-- 也能够渲染注册过的组件或 prop 传入的组件 -->
<component :is="$options.components.child"></component>
```

## 动态组件
**有的时候，在不同组件之间进行动态切换是非常有用的比如在一个多标签的界面里**：

```
<!-- 组件会在 `currentTabComponent` 改变时改变 -->
<component v-bind:is="currentTabComponent"></component>
```

在上述示例中，currentTabComponent 可以包括
- **已注册组件的名字**
- **一个组件的选项对象**

你可以在这里查阅并体验完整的代码，或在这个版本了解绑定组件选项对象，而不是已注册组件名的示例。

到目前为止，关于动态组件你需要了解的大概就这些了，如果你阅读完本页内容并掌握了它的内容，我们会推荐你再回来把**动态和异步组件**读完。

## 解析 DOM 模板时的注意事项
有些 HTML 元素，诸如**ul、ol、table** 和 **select**，对于哪些元素可以出现在其内部是有严格限制的。而有些元素，诸如 **li、tr** 和 **option**，只能出现在其它某些特定的元素内部。

这会导致我们使用这些有约束条件的元素时遇到一些问题。例如：
```
<table>
  <blog-post-row></blog-post-row>
</table>
```

这个自定义组件 **<blog-post-row>** 会被作为无效的内容提升到外部，并导致最终渲染结果出错。幸好这个特殊的 **is** 特性给了我们一个变通的办法：
```
<table>
  <tr is="blog-post-row"></tr>
</table>
```
需要注意的是如果我们从以下来源使用模板的话，这条限制是不存在的：

字符串 (例如：template: '...')
单文件组件 (.vue)

```
<script type="text/x-template">
```
到这里，你需要了解的解析 DOM 模板时的注意事项——实际上也是 Vue 的全部必要内容，大概就是这些了.