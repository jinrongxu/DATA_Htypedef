在react中修改this
1. bind在constructor，性能最高
2. bind在render中，性能最低，因为调用render的时候才会进行触发
3. 箭头函数，性能与在constructor差不多
写法：
```js
class Example extends React.Component{
    constructor(){
        this.changeCount.bind(this)
    }
    changeCount(){
        
    }
  <!--changeCount=()=>{-->
               
  <!-- }-->
  render(){
    let {count}=this.state
    return <div>
            <div>{count}</div>    
              <button onClick={this.changeCount}>点击</button>
      </div>
  }
}
ReactDOM.render(<Example/>,document.getElementById('box'))
```