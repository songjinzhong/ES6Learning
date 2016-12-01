## 块级作用域

** let 代替 var**

let 完全可以代替 var 且没有副作用，let 是块级作用域，

** 全局常量和线程安全**

const 作为常量，优先考虑，好处多多。一可以提醒阅读程序的人，这个值是常量，二是可以避免后面犯错误。

## 字符串

静态字符串一律使用单引号或反引号，不使用双引号。动态字符串使用反引号。

## 解构赋词

使用数组成员对变量赋值时，优先使用解构赋值。

## 对象

单行定义的对象，最后一个成员不以逗号结尾。多行定义的对象，最后一个成员以逗号结尾。

对象尽量静态化，一旦定义，就不得随意添加新的属性。如果添加属性不可避免，要使用Object.assign方法。

如果对象的属性名是动态的，可以在创造对象的时候，使用属性表达式定义：

```
// bad
const obj = {
  id: 5,
  name: 'San Francisco',
};
obj[getKey('enabled')] = true;

// good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
};
```

## 数组

使用 ... 来拷贝数组

Array.from 可以将类数组对象转换成数组。

## 函数

箭头函数 

## Map 结构

如果使用 key value ，建议使用 Map，有良好的遍历机制。

## Class

Class 替代 ES5 繁琐的 prototype 操作等。

## 模块

使用 import 取代 require，

## ESLint

ESLint 是一个语法规则和代码测试等检测工具。