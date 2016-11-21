## 数组解构赋值

```javascript
var a = 1;
var b = 2;
var c = 3;
// es6
var [a, b, c] = [1, 2, 3];
```

只要等号两边的模式相同，就会进行模式匹配。解构不成功，就会 underfined，`var [bar, foo] = [1];` foo 为 underfined。但匹配一部分可以成功，比如 `let [a, [b], d] = [1, [2, 3], 4];`。

## 运行指定默认值

```javascript
var [foo = true] = [];
foo // true

[x, y = 'b'] = ['a']; // x='a', y='b'
[x, y = 'b'] = ['a', undefined]; // x='a', y='b'
//必须是 underfined才行，比如
var [x = 1] = [null];
x // null
var [x = 1] = [underfined];
x // 1
```

## 对象的解构赋值 

```
var { bar, foo } = { foo: "aaa", bar: "bbb" };
foo // "aaa"
bar // "bbb"

var { baz } = { foo: "aaa", bar: "bbb" };
baz // undefined
```

不同是：没有顺序，但要同名才行。

另外，这样子赋值的是后者，而不是前者：

```
var { foo: baz } = { foo: "aaa", bar: "bbb" };
baz // "aaa"
foo // error: foo is not defined
```

## 字符串的解构

## 数值和布尔值

## 函数参数解构

```
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3

[[1, 2], [3, 4]].map(([a, b]) => a + b);
// [ 3, 7 ]
```

## 用途（重点在这）

变量交换

`[x, y] = [y, x]`

返回多个值，感觉这个和 python 返回 ， 很像

```
// 返回一个数组

function example() {
  return [1, 2, 3];
}
var [a, b, c] = example();
```

函数参数定义，**提取 json**；

```
var jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
};

let { id, status, data: number } = jsonData;

console.log(id, status, number);
// 42, "OK", [867, 5309]
```

函数的默认值，再也不用 `option.name = option.name || 'songjz'`，

```
jQuery.ajax = function (url, {
  async = true,
  beforeSend = function () {},
  cache = true,
  complete = function () {},
  crossDomain = false,
  global = true,
  // ... more config
}) {
  // ... do stuff
};
```

