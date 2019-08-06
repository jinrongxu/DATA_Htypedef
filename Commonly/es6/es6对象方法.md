# es6方法
## Object.assign({}, obj1, obj2); 合并对象
返回第一个参数 默认修改第一个参数<br/>
==只能合并可枚举属性==可枚举是指可以进行遍历

```
let obj1 = {
    name: 'zs',
    age: 12,
    sex: 'man'
}
let obj2 = {
    name: 'ww',
    age: 20,
    class: '1610'
}
function extend (obj, ...arg) {
    arg.forEach(function (file) {
        for (let i in file) {
            obj[i] = file[i];
        }
    })
    return obj;
}
let obj = extend({}, obj1, obj2);
console.log(obj);
let objs = Object.assign({}, obj1, obj2);
console.log(objs);
```


##  Object.getOwnPropertyDescriptor(obj, 属性名, [配置项]);<br>(获取)
获取当前对象的属性的描述对象

返回值为对象

```
let obj = {
        name: 'zs',
        age: 12
    }
let o = Object.getOwnPropertyDescriptor(obj, 'name')
console.log(o);
```
##  Object.defineProperty(obj, 属性名, [配置项]);
**(用于给对象里只加键值对，或替换键值对)**
- 定义属性<br>

①数据属性
```
let obj = {
        name: 'zs'
    }
Object.defineProperty(obj, 'age', {
    value: 12,
    configurable: true, // 默认false，是否可配置是否能操作
    enumerable: true, // 默认为false，是否可枚举
    writable: true // 默认false，是否可编辑
})
obj.age = 22;
console.log(obj)
console.log(Object.keys(obj)) // 打印不出来的为不可枚举属性
```
②访问器属性
```
var str;
Object.defineProperty(obj, 'aa', {
    get () { 
    // 当使用该键值对时函数被触发，可以在函数里设置属性值，如不设置为undefined
        return str//4>返回设置的值
    },
    set(val) { //2>通过set的方法把b=55;
    // 当设置该变量时函数触发
    str=val//3>把val赋给新变量
        console.log(val);
    }
})
obj.b=55//1>先设置
```

==**数据属性与访问器属性不能共存**==
###### Object.keys(obj);//键名
###### Object.values(obj);//键值
###### Object.entries(obj);//键名+键值
返回值是一数组的形式。
这三个返回的也是一个遍历器对象，可以使用for of 进行遍历
######   Object.is(v1, v2) 比较两个值是否完全相等

```
NaN === NaN // false
```
 NaN和任何数据类型都不想等包括自身

```
Object.is(NaN, NaN) // true
```

