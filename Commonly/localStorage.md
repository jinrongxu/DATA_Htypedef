# H5- localStorage 笔记
[toc]
## 在客户端存储数据
#### **cookie**  
- 但是 cookie 不适合大量数据的存储，因为它们由每个对服务器的请求来传递，这使得 cookie 速度很慢而且效率也不高。
- 
==HTML5 提供了两种在客户端存储数据的新机制==
#### **localStorage** 
- localStorage 存储的数据没有时间限制。只要浏览器不清楚数据，它储存的数据一直存在
####  **sessionStorage** 
- sessionStorage 方法针对一个 会话窗口进行数据存储。当用户关闭浏览器窗口后，数据会被删除。

## localStorage基本语法
HTML5 使用 JavaScript 来存储和访问数据。可以通过调用Window.sessionStorage和Window.localStorage属性创建一个Storage对象的实例。

- Storage 对象以简单的键值得形式来储存数据，键值都是以字符串的形式进行储存，如果一个值是数字，它将被转为字符串。

####  **localStorage本地方法**

header 1 | header 2
---|---
添加键值对 | localStorage.setItem(key,value);
获取键值对 | localStorage.getItem(key);
删除键值对 |  localStorage.removeItem(key);// 删除数据数据时使用单个参数；
清除所有键值对| localStorage.clear();// 清空数据数据时不需要参数；
获取localStorage的键名 |  localStorage.key;
获取localStorage中保存的键值对的数量 | localStorage.length;


#### **localStorage 的巧用**
- 对用户访问页面的次数进行计数：
```
<script type="text/javascript">
if (localStorage.pagecount)
  {
  localStorage.pagecount=Number(localStorage.pagecount) +1;
  }
else
  {
  localStorage.pagecount=1;
  }
</script>
```
- 用户每次刷新页面都会触发localStorage，触发localStorage后都会给 localStorage.pagecount的值增加增加一，以此来达到统计访问量的目的。

- 用户在当前 session 中访问页面的次数进行计数时，将上面代码中的localStorage换成sessionStorage即可。

### 自己扩展：真实项目中使用的第三方插件
对于数据多维的储存，使用Storage插件会更加方便，比较常用有Storage.js、store.js等插件。

store.js 插件：

该插件小巧，简介，兼容性很强，可实现大多数日常的应用
