React通过this.state来访问state，通过this.setState()方法来更新state。当this.setState()方法被调用的时候，React会重新调用render方法来重新渲染UI
```html
<div id="box"></div>
```
合成事件
```js
 <script src="https://unpkg.com/react@16/umd/react.production.min.js" crossorigin></script>
 <script src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js" crossorigin></script>
 <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
class Example extends React.Component{
            state={
                count:1
            }
            changeCount=()=>{
                //直属作用域的 setState 会先进行合并 执行一次，只打印一次
                this.setState({
                    count:this.state.count+1
                })
                console.log(this.state.count,'one');//1
                setTimeout(() => {
                    //同步函数
                    this.setState({
                    count:this.state.count+1
                    })
                    console.log(this.state.count,'two')//3
                    this.setState({
                    count:this.state.count+1
                    })
                    console.log(this.state.count,'two')//4
                }, 100);
                this.setState({
                    count:this.state.count+1
                })
                console.log(this.state.count,'three')//1
            }
            render(){
                let {count}=this.state
                console.log('render');
                //除实例期外render会打印三次，分别是1后（异步），3,4之前（同步）
                return <div>
                    <div>{count}</div>    
                    <button onClick={this.changeCount}>点击</button>
                </div>
            }
        }
        ReactDOM.render(<Example/>,document.getElementById('box'))
```

获取dom添加点击事件

```js
  class Example extends React.Component{
            state={
                count:1
            }
            changeCount(){
                //setState是同步函数
                this.setState({
                    count:this.state.count+1
                })
                console.log(this.state.count,'one')//2
                setTimeout(() => {
                    //同步函数
                    this.setState({
                    count:this.state.count+1
                    })
                    console.log(this.state.count,'two')//4
                    this.setState({
                    count:this.state.count+1
                    })
                    console.log(this.state.count,'two')//5
                }, 100);
                this.setState({
                    count:this.state.count+1
                })
                console.log(this.state.count,'three')//3
            }
            render(){
                let {count}=this.state
                console.log('render')//会在打印结果之前打印，setState是同步函数
                return <div>
                    <div>{count}</div>    
                    <button ref='btn'>点击</button>
                </div>
            }
            componentDidMount(){
                this.refs.btn.addEventListener('click',this.changeCount.bind(this))
            }
        }
        ReactDOM.render(<Example/>,document.getElementById('box'))
```