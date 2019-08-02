下载安装
```
npm install react-router-dom -S
yarn add react-router-dom 
```
路由是组件，渲染真实的组件
引用
```
import {hashRouter，browserRouter ,Route,Switch} from "react-router-dom"//两种hashRouter与browserRouter
//HashRouter必须要把内容包起来
//Route渲染组件用,<Router/>渲染组件
//Switch判断
```
react不是精准匹配

Router渲染方式
- component:react.createElement()
- render:调用实例化完成以后的render必须回调函数，必须实例化，可以穿props
- children:回调函数，必须实例化，不管匹配到都会渲染
```
<HashRouter>
    //该组件不需要注册
    <Route exact path="/" component={Home}/>
    <Route path="/news" component={News}/>
</HashRouter>
//exact 关键字精准匹配，
//就可以跳转对应的页面，不写false，写上true但会
//影响二级路由

//用Switch <Switch></Switch>匹配时根路径写最后
//有二级时，一级写在二级下面可以匹配
```
路由跳转
```
import {Link,NavLink} from "react-router-dom"
//Link跳转路由
<Link to="/news">
//NavLink自动添加,功能比Link多
<div>
    <NavLink to='/tab1'>tab1</NavLink>
    <NavLink to='/tab2'>tab2</NavLink>
    <NavLink to='/tab3'>tab3</NavLink>
</div>
<Route path="/tab1" component={Tab1}></Route>
<Route path="/tab2" component={Tab2}></Route>
<Route path="/tab3" component={Tab3}></Route>
```
路由传参

```
一、params传参
1、在路由配置中以/：的方式评接参数标识
<Route path:"/detail/:id" component='Detail'></Route>
2、在路径后面将参数评接上(/参数)
<Link to='/detail/1'></Link>
3、在被跳转页使用this.props.match.params.xxx(此处为id)   
  接收参数
二、query传参
1、在router文件中配置为正常配置 <Route path="/Child03" component={Child03}/>
2、在跳转时  路径为一个对象{} 其中 pathname为路径  query为一个对象  对象里是携带的参数
3、使用this.props.location.query接收参数
三、state传参
使用this.props.location.state接收参数
<Link to={{pathname:"/detail",state:{name:"zhangsa"}}></Link>
```

重定向Redirect,配合Switch使用
```
   <Switch>
            <Route path="/tab1" component={Tab1}></Route>
            <Route path="/tab2" component={Tab2}></Route>
            <Route path="/tab3" component={Tab3}></Route>
            <Redirect  from="/" to="Tab1"/>//如果不写exact，写在最后
   </Switch>
```