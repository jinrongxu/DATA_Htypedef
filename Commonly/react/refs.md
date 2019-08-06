### ref

> 挂到组件（有状态组件）上的ref表示对组件实例的引用
>
> 挂载到元素上时表示具体的dom元素节点
>
> 不要在render或render之前对Refs进行调用
>
> 不会通过props传递
>
>######  第一种 不建议使用，有可能废弃
>
>字符串形式
>在react元素上定义一个ref等于一个字面量（字符串>>） 
>
>通过组件上的refs对象可以获取---不建议使用
> ```javascript
> class App extends Component {
>   render() {
>     return (
>       <div>
>         登录名：<input ref='name' type="text"/>
>         <br />
>         <button onClick={this.login}>登陆</button>
>       </div>
>     );
>   }
>   login = () => {
>     console.log(this.refs.name.value)
>   };
> ```
>
> ###### 第二种
>
>回调函数（匿名函数）
>通过回调函数（匿名函数）把传入回调函数的dom挂在组件的一个变量上
> ```javascript
> class App extends Component {
>   render() {
>     return (
>       <div>
>         登录名：<input ref={ name => this.name =name} type="text"/>
>         <br />
>         <button onClick={this.login}>登陆</button>
>       </div>
>     );
>   }
>   login = () => {
>     console.log(this.name.value)
>   };
> ```
>
> ###### 第三种
>
> React.createRef()
> ```javascript
> class App extends Component {
>   constructor() {
>     super();
>     this.login = React.createRef();
>   }
>   render() {
>     return (
>       <div>
>         登录名：<input ref={this.name} type="text" />
>         <br />
>         <button onClick={this.login}>登陆</button>
>       </div>
>     );
>   }
>  
>   login = () => {
>     console.log(this.login.current.value);
>     
>   };
> ```

### ref与无状态组件（函数组件）

> **无状态组件是不会被实例化的**,父组件中通过`ref`来获取无状态子组件时，其值为`null`
>
> 法通过`ref`来获取无状态组件实例
>
> ```javascript
> const Fun = ()=>{
>   let funRef = React.createRef()
>   function getRef(){
>     console.log(funRef.current)
>   }
>   return (
>     <div>
>     <p ref={funRef} onClick={getRef}>这是一个函数组件</p>
>   </div>
>   )
> }
> ```
>
>

### findDOMNode

> 得到实际Dom的方法
>
> 引入
>
> ```javascript
> import {findDOMNode} from 'react-dom'
> ```

作用在类组件上获取的是未实例化的组件,
如果想要获取组件对应的dom，通过react-dom中提供的findDOMNode方法来转      **函数组件不可以通过refs获取dom**

```
console.log(this._div.current)//子类组件实例
console.log(findDOMNode(this._div.current))//真实的dom
```
如果组件已经被挂载到 DOM 上，此方法会返回浏览器中相应的原生 DOM 元素。此方法对于从 DOM 中读取值很有用，例如获取表单字段的值或者执行 DOM 检测（performing DOM measurements）**。大多数情况下，你可以绑定一个 ref 到 DOM 节点上，可以完全避免使用 findDOMNode**。


### unmountComponentAtNode

```javascript
import {unmountComponentAtNode} from 'react-dom'
```
从 DOM 中卸载组件，会将其事件处理器（event handlers）和 state 一并清除。如果指定容器上没有对应已挂载的组件，这个函数什么也不会做。如果组件被移除将会返回 true，如果没有组件可被移除将会返回 false。




