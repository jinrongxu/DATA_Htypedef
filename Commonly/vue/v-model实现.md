mvvm的双向绑定，最突出的v-model

v-model不只用于input框，组件也可以使用，并且可以更改数据



```js
//父组件
<template>
<Child v-model='ipt'></Child>
</template>
<script>

export default{
    props:['value'],
    data(){
        return{
            
        }
    }
}
</script>

```

```js
//子组件
<template>
    <button @click="changeIpt">修改</button>
</template>
<script>
export default{
    props:['value'],
    data(){
        return{
            
        }
    }
}
</script>
```