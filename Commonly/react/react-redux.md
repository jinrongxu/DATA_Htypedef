下载

```
npm i react-redux
```


引入 index.js

```
import {Provider} from "react-redux"
```


用Provider把<APP/>引起来，这样所有的组件都可以能用store里的值


```
<Provider store={store}>
    <App/>
</Provider>
```
在其他组件里引入connect，包裹住抛出的组件


```
export default connect(mapStateToProps,mapStateToProps)(Home)
```
使用
```
import {connect} from "react-redux";
const mapStateToProps=state=>{
    //state使store里面的state（redux中的）,并且会挂载到props
    return state;
}
const mapDispatchProps=dispatch=>{
    //返回dispatch函数,并且会挂载到props
    方法1(){
        
    },
    方法2(){
        
    }
}

connect中有四个参数
connect(mapStateToProps,mapDispatchProps){
    
}
```


