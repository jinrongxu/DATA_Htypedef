# module
模块功能主要由两个命令构成：export和import
- export命令是用于规定模块的对外接口
- import命令用于输入其他模块提供的功能。
- 
## export
一个模块就是**一个独立的文**件。该文件内部的所有变量，**外部无法获取**。如果你希望外部**能够读取模块内部**的某个变量，就必须**使用export关键字输出该变量**。

```
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;
//上面代码一个是js文件
//将其视为一个模块里面用export命令对外部输出了三个变量。
```
export的写法，除了像上面这样，还有另外一种。
```
// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export {firstName, lastName, year};
```
export命令除了输出变量，还可以输出函数或类（class）。

```
export function multiply(x, y) {
  return x * y;
};
export class Fn{
    constructor(){}
}
//抛出默认
export default class{}
```
通常情况下，export输出的变量就是本来的名字，但是可以使用as关键字重命名。


```
function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```

上面代码使用as关键字，重命名了函数v1和v2的对外接口。重命名后，v2可以用不同的名字输出两次

需要特别注意的是，**export命令规定的是对外的接口**，必须与模块内部的变量**建立一一对应关系**。

```
// 报错
export 1;

// 报错
var m = 1;
export m;
```
上面两种写法都会报错，因为没有提供对外的接口。第一种写法直接输出 1，第二种写法通过变量m，还是直接输出 1。1只是一个值，不是接口。正确的写法是下面这样。
```
// 写法一
export var m = 1;

// 写法二
var m = 1;
export {m};

// 写法三
var n = 1;
export {n as m};
```
上面三种写法都是正确的，规定了对外的接口m。**其他脚本可以通过这个接口，取到值1**。它们的实质是，在接口名与模块内部变量之间，**建立了一一对应的关系。**<br>
==export命令可以出现在模块的任何位置，只要处于模块顶层就可以==。如果==处于块级作用域内==，就会**报错**。这是因为处于条件代码块之中，就没法做静态优化了，违背了 ES6 模块的设计初衷。

function foo() {
  export default 'bar' // SyntaxError
}
foo()
上面代码中，export语句放在函数之中，结果报错。
## import
使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。

```
import {firstName, lastName, year} from './profile.js';

function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```
