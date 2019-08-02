在开发react单页面应用时，我们会遇到一个问题，那就是打包后的js文件特别巨大，首屏加载会特别缓慢。这个时候我们应该讲代码进行分割，按需加载，将js 拆分成若干个chunk.js,用到就加载，react-loadable就可以很好地解决这个问题。
安装

```
yarn add react-loadable
```
假设现在项目中有个 home页面组件
src/pages/home/index.js

```
import React, { Component } from 'react'
class Home extends Component {
    render(){
        return (
            <div>这个是home页面</div>
        )
    }
}



export default Home
```

在没有使用react-loadable之前，在我们的route.js里面是直接import Home这个组件的
router.js

```
import React, { Fragment } from 'react'
import { BrowserRouter, Route } from 'react-router-dom'

import Home from '@pages/home'

const Routes = () => (
    <BrowserRouter>
        <Route path="/home" component={Home}/>
    </BrowserRouter>
);

export default Routes
```


运行项目后我们可以看chrome的network记录


可以看到1.chunk.js是687k

现在我们来添加react-loadable
在home文件下新建一个loadable.js文件
src/pages/home/loadable.js

```
import React from 'react';
import Loadable from 'react-loadable';

//通用的过场组件
const loadingComponent =()=>{
    return (
        <div>loading</div>
    ) 
}


export default Loadable({
    loader:import('./index.js'),
    loading:loadingComponent
});
```


然后再router里面调用

```
import React, { Fragment } from 'react'
import { BrowserRouter, Route } from 'react-router-dom'

import Home from '@pages/home/loadable'

const Routes = () => (
    <BrowserRouter>
        <Route path="/home" component={Home}/>
    </BrowserRouter>
);

export default Routes
```

