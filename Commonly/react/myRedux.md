下载

```
yarn add redux
```
定义

```
store/index.js
```
引入

```
//index.js
import {createStore} from "redux";
import reducer from "./reducer"
//redux纯函数，不能写异步函数，只要接受
const store=createStore(reducer)
//const store=createStore(参数)
export default store
```
核心js
```
//reducer.js
//设置state的默认值
const defaultState={
    设置默认值
}
const reducer=(state=defaultState,action)=>{
    switch（action.type）{
        case "传过来的type",
        break;
    }
    return state//有返回值,要有返回值
}
export default reducer;
```
步骤：

1.在点击事件中，创建action；

```
const action={
    type:"ADD",
}
```

2.将action的数据发送到store

```
store.dispatch(action)
```


3.reduce判断里action.type类型

```
//最好少使用if判断
switch（action.type）{
        case "传过来的type",
        break;
    }
```


4.修改传过来的state


```
state不允许直接修改，可能会造成视图的不更新，
可能使redux、store不更新
```
```
可以进行深拷贝JSON.parse(JSON.stringify(state))进行操作
```

5.订阅state变化(store里自带的subscribe)

```
//可以拿到变化
store.subscribe(()=>{
    //定义改变state的函数
    this.stateChange()
})
//修改state数据的函数
stateChange(){
    this.setState({
        ...store.getState()
    })
}
```

```
dispatch：传值action
getState:获取值
subscribe：订阅
```
