### 1. includes(), startsWith(), endsWith()
- includes()：==返回布尔值==，表示是否找到了参数字符串。
- startsWith()：==返回布尔值==，表示参数字符串是否在原字符串的头部。
- endsWith()：==返回布尔值==，表示参数字符串是否在原字符串的尾部。

```
let s = 'Hello world!';
s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true
```

这三个方法都支持第二个参数，表示开始搜索的位置。

```
let s = 'Hello world!';
s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
```

2. repeat()
==repeat方法返回一个新字符==串，表示将原字符串重复n次。

```
'x'.repeat(3) // "xxx"
'hello'.repeat(2) // "hellohello"
'na'.repeat(0) // ""
```

参数==如果是小数，会被取整==。

```
'na'.repeat(2.9) // "nana"
```

如果repeat的参数是==负数或者Infinity==，==会报错==。

```
'na'.repeat(Infinity)
// RangeError
'na'.repeat(-1)
// RangeError
```

但是，如果参数是 ==0 到-1 之间的小数==，则等同于 ==0==。<br>这是因为会先进行取整运算。<br>
==0 到-1 之间的小数==，取整以后等于==-0==，==repeat视同为 0。==

```
'na'.repeat(-0.9) // ""
```

==参数NaN等同于 0。==

```
'na'.repeat(NaN) // ""
```

==如果repeat的参数是字符串，则会先转换成数字==。

```
'na'.repeat('na') // ""
'na'.repeat('3') // "nanana"
```

3. padStart()，padEnd()<br/>
如果某个字符串不够指定长度，会在头部或尾部补全。padStart()用于头部补全，padEnd()用于尾部补全。
padStart()和padEnd()一共接受两个参数，第一个参数是字符串补全生效的最大长度，第二个参数是用来补全的字符串。

```
'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'

'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
```

如果用来补全的字符串与原字符串，两者的长度之和超过了最大长度，则会截去超出位数的补全字符串。

```
'abc'.padStart(10, '0123456789')
// '0123456abc'
```

如果省略第二个参数，默认使用空格补全长度。

```
'x'.padStart(4) // '   x'
'x'.padEnd(4) // 'x   '
```

padStart()的常见用途是为数值补全指定位数。下面代码生成 10 位的数值字符串。

```
'1'.padStart(10, '0') // "0000000001"
'12'.padStart(10, '0') // "0000000012"
'123456'.padStart(10, '0') // "0000123456"
```

另一个用途是提示字符串格式。

```
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```

4. 模板字符串
模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。
