## 函数参数的默认值

这个和 python 差不多了，很有用。

```
function log(x, y = 'World') {
  console.log(x, y);
}

log('Hello') // Hello World
log('Hello', 'China') // Hello China
log('Hello', '') // Hello
```

**与解构复制配合使用**

```
function foo({x, y = 5}) {
  console.log(x, y);
}

foo({}) // undefined, 5
foo({x: 1}) // 1, 5
foo({x: 1, y: 2}) // 1, 2
foo() // TypeError: Cannot read property 'x' of undefined
```

**参数位置**

```
function f(x, y = 5, z) {
  return [x, y, z];
}

f() // [undefined, 5, undefined]
f(1) // [1, 5, undefined]
f(1, ,2) // 报错
f(1, undefined, 2) // [1, 5, 2]
```

当参数位置不是末尾的时候，必须手动输入参数 underfined，否则。。还有 null 无法得到效果，比如

```
function foo(x = 5, y = 6) {
  console.log(x, y);
}

foo(undefined, null)
// 5 null
```

**length** 将异常

```
(function (a = 0, b, c) {}).length // 0
(function (a, b = 1, c) {}).length // 1
```

**作用域**

```
var x = 1;

function f(x, y = x) {
  console.log(y);
}

f(2) // 2

let x = 1;

function f(y = x) {
  let x = 2;
  console.log(y);
}

f() // 1
```

调用函数时，如果 x 没有生成，则全局，如果 x 已经生成，则生成的那个 x。

**闭包**

```
let foo = 'outer';

function bar(func = x => foo) {
  let foo = 'inner';
  console.log(func()); // outer
}

bar();
```

## 应用

此处不可省去参数，可以写一个函数专门用来抛错，如果此处省略参数就抛错。

```
function throwIfMissing() {
  throw new Error('Missing parameter');
}

function foo(mustBeProvided = throwIfMissing()) {
  return mustBeProvided;
}

foo()
// Error: Missing parameter
```

## reset 参数

reset 不是关键字，是形如 `function(...values){}`,比如一个任意参数的求和，

```
function add(...values){
  let sum = 0;
  for(var v of values){
    sum+=v;
  }
  return sum;
}
```

需要注意，reset 后不能有其他参数，必须是最后一个参数，length 值不包括 reset 在内。

## 扩展运算符

... 表示将一个数组拆分，`console.log(1, ...[2, 3, 4], 5)`

**数组合并的新写法**

```
//es5
// ES5
[1, 2].concat(more)
// ES6
[1, 2, ...more]
```

结构赋值结合，函数的返回值，

**字符串**

```
[...'hello']
// [ "h", "e", "l", "l", "o" ]
```

将字符串转换成数组，非常好用，和 `Array.from('hello')` 可以一战。

## 函数内部可以设定严格模式

## 函数支持 name 属性

```
function foo() {}
foo.name // "foo"
(new Function).name // "anonymous"
```

## 箭头函数 

好吧，，不多介绍了，用的比较多

**注意点**

1. this 是定义时所在的对象，而不是使用时所在的对象。
2. 不可以构造，不能用 new；
3. 不能用 arguments，可用 reset；
4. 不能使用 yield；

关于第一点，实在定义时，而不是使用时的对象

```
var handler = {
  id: '123456',

  init: function() {
    document.addEventListener('click',
      event => this.doSomething(event.type), false);
  },

  doSomething: function(type) {
    console.log('Handling ' + type  + ' for ' + this.id);
  }
};
```

this指向的固定化，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。正是因为它没有this，所以也就不能用作构造函数。

## 绑定 this

用 `::` 来绑定对象，左边导航对象右边是函数。

```
foo::bar;
// 等同于
bar.bind(foo);

foo::bar(...arguments);
// 等同于
bar.apply(foo, arguments);

const hasOwnProperty = Object.prototype.hasOwnProperty;
function hasOwn(obj, key) {
  return obj::hasOwnProperty(key);
}
```

## 尾调用优化 

## 尾递归 

## 递归函数的改写 

## 函数参数的尾逗号 

