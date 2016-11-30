在 ES6 之前，异步编程的方法，大概又一下几类：

1. 回掉函数
2. 时间监听
3. 发布／订阅
4. Promise 对象

## 基本概念

**异步**的基本概念，**回掉函数**的概念，**Promise**的概念，

## Generator

Generator 事携程在 ES6 的基本实现，在需要暂停的地方，都用 Generator 的 yield 来实现，

```
function* gen(x){
  var y = yield x + 2;
  return y;
}

var g = gen(1);
g.next() // { value: 3, done: false }
g.next() // { value: undefined, done: true }
```

## Generator函数的数据交换和错误处理 

可以通过 next() 函数设置值进行数据交换，也能够进行错误处理，比如

```
function* gen(x){
  try {
    var y = yield x + 2;
  } catch (e){
    console.log(e);
  }
  return y;
}

var g = gen(1);
g.next();
g.throw('出错了');
// 出错了
```

**Thunk**函数

编译器的"传名调用"实现，往往是将参数放到一个临时函数之中，再将这个临时函数传入函数体。这个临时函数就叫做Thunk函数。

```
function f(m){
  return m * 2;
}

f(x + 5);

// 等同于

var thunk = function () {
  return x + 5;
};

function f(thunk){
  return thunk() * 2;
}
```

JavaScript语言是传值调用，它的Thunk函数含义有所不同。在JavaScript语言中，Thunk函数替换的不是表达式，而是多参数函数，将其替换成单参数的版本，且只接受回调函数作为参数。

## co模块 貌似经常见到的样子

比如，有一个Generator函数，用于依次读取两个文件。

```
var gen = function* (){
  var f1 = yield readFile('/etc/fstab');
  var f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```

co模块可以让你不用编写Generator函数的执行器。

```
var co = require('co');
co(gen);
```

上面代码中，Generator函数只要传入co函数，就会自动执行。co函数返回一个Promise对象，因此可以用then方法添加回调函数。

```
co(gen).then(function (){
  console.log('Generator 函数执行完成');
});
```

## async函数 

async函数就是Generator函数的语法糖。

async函数就是将Generator函数的星号（*）替换成async，将yield替换成await，仅此而已。

async函数对 Generator 函数的改进，体现在以下四点。

1. 内置执行器；
2. 更好的语义；
3. 更广的适用性；
4. 返回值是 Primise。

