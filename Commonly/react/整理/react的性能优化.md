React中可以优化的点

```
1. 在constructor改变this指向代替箭头函数和render内绑定this，避免函数作为props带来不必要的render

2. shouldComponentUpdate，减少不不必要的render

3. PureComponent高性能组件只响应引用数据的深拷贝

4. 使用唯一key优化list diff

5. 合并setState操作，减少虚拟dom对比频率

6. React路由动态加载react-loadable
```