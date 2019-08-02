###### react
react是开源前端JavaScript库，用于构建用户界面，尤其是单页应用程序。它用于处理网页和移动应用程序的视图层。
###### 什么是 Pure Components?
React.PureComponent 与 React.Component 完全相同，**只是它为你处理了 shouldComponentUpdate() 方法**。当属性或状态发生变化时，PureComponent 将对属性和状态进行**浅比较**。另一方面，一般的组件不会将当前的属性和状态与新的属性和状态进行比较。因此，在默认情况下，每当调用 shouldComponentUpdate 时，默认返回 true，所以组件都将重新渲染。
###### react组件实例
组件实例是react组件类的实例化对象，它通常管理内部状态，吃力生命周期函数。我们无需直接创建组件实例，React会负责创建它，**ReactDOM.render方法返回的结果就是组件实例**
###### redux中间件

中间件提供第三方插件的模式，自定义拦截 action -> reducer 的过程。变为 action -> middlewares -> reducer 。这种机制可以让我们改变数据流，实现如异步 action ，action 过滤，日志输出，异常报告等功能。

常见的中间件：

- redux-logger：提供日志输出
- 
- redux-thunk：处理异步操作
- 
- redux-promise：处理异步操作，actionCreator的返回值是promise

###### redux有什么缺点

1.一个组件所需要的数据，必须由父组件传过来，而不能像flux中直接从store取。

2.当一个组件相关数据更新时，即使父组件不需要用到这个组件，父组件还是会重新render，可能会有效率影响，或者需要写复杂的shouldComponentUpdate进行判断。

###### react生命周期
一、初始化阶段：

getDefaultProps:**获取实例的默认属性**

getInitialState:**获取每个实例的初始化状态**

componentWillMount：**组件即将被装载、渲染到页面上**
（渲染前调用）

render:**组件在这里生成虚拟的DOM节点**

componentDidMount:**组件真正在被装载之后**
（第一次渲染后调用）

二、运行中状态：

componentWillReceiveProps:**组件将要接收到属性的时候调用**
（在组件接收到一个新的props时被调用。这个方法在第一次渲染时不会被调用。）

shouldComponentUpdate:**组件接受到新属性或者新状态的时候（可以返回false，接收数据后不更新，阻止render调用，后面的函数不会被继续执行了）**
（返回一个布尔值。在组件接收到新的props或state时被调用）

componentWillUpdate:**组件即将更新不能修改属性和状态**
（在组件接收到新的props或state，但还没有render时被调用）

render:**组件重新描绘**

componentDidUpdate:**组件已经更新**（在组件完成更新后立即调用。在初始化时不会被调用）

三、销毁阶段：

componentWillUnmount:**组件即将销毁**
（在组件从DOM中移除的时候立刻被调用）

###### react性能优化是哪个周期函数？

shouldComponentUpdate 这个方法用来**判断是否需要调用render方法重新描绘dom**。因为**dom的描绘非常消耗性能**，如果我们能在shouldComponentUpdate方法中能够写出更优化的dom diff算法，可以极大的提高性能。
###### 为什么虚拟dom会提高性能?

虚拟dom**相当于在js和真实dom中间加了一个缓**存，利用dom diff算法**避免了没有必要的dom操作**，从而提高性能。
###### react性能优化方案

（1）重写shouldComponentUpdate来避免不必要的dom操作。

（2）使用 production 版本的react.js。

（3）使用key来帮助React识别列表中所有子组件的最小变化。