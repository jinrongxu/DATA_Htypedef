### redux文档地址

> 文档：https://redux.js.org/
>
> 中文文档：https://www.redux.org.cn/
>
> 只是一个状态存储，可预测，可以用在express，koa，vue，readux

### 安装：

> 通过yarn
>
> ```shell
> yarn add redux
> ```
>
> 通过npm
>
> ```shell
> npm install redux --save
> //或者
> npm i redux -S
> ```
>
> 通过cnpm 
>
> ```shell
> cnpm install redux --save
> ```
>



## 过程

> 1. 组件先创建一个action
> 2. 通过dispatch发送action到store
> 3. store发送state和action到reducer
> 4. reducer处理完数据，返回一个新的state，传给store
> 5. 组件监听到store的变化，更新视图
>
> tips：redux是``单向数据流``