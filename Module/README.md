ES6 之前有两种模块化加载的方式，分别是 CommonJS 和 AMD，前者用于服务器，后者用于浏览器。

## 严格模式

会自动加上严格模式，关于严格模式下有哪些不同：

1. 变量必须声明后再使用
2. 函数的参数不能有同名属性，否则报错
3. 不能使用with语句
4. 不能对只读属性赋值，否则报错
5. 不能使用前缀0表示八进制数，否则报错
6. 不能删除不可删除的属性，否则报错
7. 不能删除变量delete prop，会报错，只能删除属性delete global[prop]
8. eval不会在它的外层作用域引入变量
9. eval和arguments不能被重新赋值
10. arguments不会自动反映函数参数的变化
11. 不能使用arguments.callee
12. 不能使用arguments.caller
13. 禁止this指向全局对象
14. 不能使用fn.caller和fn.arguments获取函数调用的堆栈
15. 增加了保留字（比如protected、static和interface）

## export 

模块由两个 import 和 export 两个命令组成，表示引入其他模块的函数和函数输出给其他模块使用。

export 不仅可以输出变量，还可输出函数。

一般的 export 命令如下：

```
//'./profile'
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export {firstName, lastName, year};
```

## import

```
import {firstName, lastName, year} from './profile';

function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```

import 效果会提升到头部执行，和变量的提前申明很像。

## export default 

为模块指定默认输出，

```
// export-default.js
export default function () {
  console.log('foo');
}
//main.js
import customName from './export-default';
customName(); // 'foo'
```

export 命令后不使用大括号。

```
// 输出
export default function crc32() {
  // ...
}
// 输入
import crc32 from 'crc32';

// 输出
export function crc32() {
  // ...
};
// 输入
import {crc32} from 'crc32';
```

## 模块的继承

```
//circle.js
export * from 'circle';
export var e = 2.71828182846;
export default function(x) {
  return Math.exp(x);
}
```

继承的意思就是表示 circle.js 函数会先输出 circle.js 函数的输出，在接着 export 后面的内容。export \* 会丢弃默认 default 方法。

