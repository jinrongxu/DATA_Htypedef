constructor只会执行一次，props的数据放在constructor中，视图不会改变
```js
//在实例的时候会调用一次，必须设置返回值
//应用场景
//state从props获取到，但是我的状态也要和props的属性变化而变化
//获取一个导出的state，从props里来的state，props和state需要同步的场景
static getDerivedStateFromProps(nextProps,prevState){
    //钩子函数
    //静态方法，不能用this.setState()
    if(nextProps.count!==prevState.count){
        //当做一个setState的动作执行
        return {
            
        }
    }
    return null;//初始没有修改返回null
    
}
//解决了操作真是dom发生错误的信息
//render，getSnapshotBeforeUpdate，componentDidUpdate
//生成虚拟dom，并映射中间发生的
getSnapshotBeforeUpdate(){
//必须和componentDidUpdate一起使用
//返回值是componentDidUpate的参数
 return null
}
componentDidUpdate(prevProps,prevState,params){
    //params是getSnapshotBeforeUpdate的返回值
}
```