大括号

`"\u{20BB7}"`

codePointAt 处理双字，返回四字节处理的字符

String.fromCodePoint 处理 32 为 UTF-16 字符

## 字符串的遍历

```
for (let codePoint of 'foo') {
  console.log(codePoint)
}
// "f"
// "o"
// "o"
```

这真的是非常方便

## includes(), startsWith(), endsWith() 

之前字符串只有一个函数 `indexOf` 方法，用来判断是否含有子串并返回位置，

1. includes() 表示是否含有子串，返回布尔；
2. startsWith() 表示以子串开头；
3. endWith() 表示以子串结尾。

第二个参数表示开始位置，而 startsWith() 第二个位置表示到为止。`'Hello world'.endsWith('Hello', 5) // true`。

## repeat()

重复 n 次，`'x'.repeat(3) // "xxx"` 表示字符串相乘，这和 python 的 `'he' * 3` 很像。

## padStart()，padEnd() 

用来补全字符串，感觉用途不是很。。。

```
'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'

'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
```

## 模板字符串

用反引号来表示模板字符串，比如

```
var name = 'hello world';
//模板用法
var str = `my name is ${name}.`;
// 以前用法
var str = 'my name is ' + name + '.';
```

`${}` 还能调用函数，

## 模板编译

我去，ES6 这以后没模板什么事了。

```
var template = `
<ul>
  <% for(var i=0; i < data.supplies.length; i++) { %>
    <li><%= data.supplies[i] %></li>
  <% } %>
</ul>
`;
```

## 标签模板 

放在函数后面，表示该函数调用该模板，`alert\`hello\``