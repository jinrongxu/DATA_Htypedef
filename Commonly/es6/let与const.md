### let 与 const
let和const是es6的两个声明标识符。
[toc]
### const 
1. 不能对变量重赋值
2. 产生块级作用域

```
const a ="a"
if(true){
    const a="aa"
    console.log(a);
    //不会出现任何问题
}
```

3. 不会变量提升
4. 不能在声明时不赋值
```
var a; // √
let a; // √
const a; // ×  Missing initializer in const declaration
```
5. 不能重复声明同一个变量
```
const str = 'a';
var str = 'b'; //  Identifier 'str' has already been declared
```

6. 暂时性死区

```
6.暂时性死区
str = 'hello';
const str = 'world';
// str is not defined;
```
### let
1. 能对变量重赋值
2. 产生块级作用域

```
for (let i = 0; i < 5; i++) {
    setTimeout(() => {
        console.log(i);
    }, 0);
}
// es5模拟块级作用域
for (var i = 0; i < 5; i++) {
    (function (i) {
        setTimeout(() => {
            console.log(i);
        }, 0);
    })(i)
}
```

3. 不会变量的提升

```
let i = 2;
function fn () {
    console.log(i);
```

4. 能在声明时不赋值
5. 在同一作用域下不能重复声明同一个变量

```
let a = 2;
{
    var a = 3;
}
console.log(a);
for (let i = 0; i < 5; i++) {
    let i = 10;
    console.log(i); // 5个10
    {
        let i = 20;
        console.log(i); // 5个20
    }
}
let i = 30;
console.log(i); // 30
```

6. 暂时性死区

```
i = 1;
let i = 3;
// ReferenceError: i is not defined
```


