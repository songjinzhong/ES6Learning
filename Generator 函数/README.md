## 简介 

ES6 提供的异步解决方案，Fenerator 函数是一个状态机，封装了多个内部状态，它有两个关键字，一个是在在 function 关键字前面有 * 标记，第二个是用 yield 来定义不同的内部状态，比如：

```
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```

表示该函数有三个状态，分别是 hello，world，和 return（结束时执行），关于函数的调用，和普通函数一样，但是执行后，什么都得不到，必须掉要 next() 方法才能一步一步执行，比如：

```
hw.next()
// { value: 'hello', done: false }

hw.next()
// { value: 'world', done: false }

hw.next()
// { value: 'ending', done: true }

hw.next()
// { value: undefined, done: true }
```

next() 的功能就是引导函数一步一步向下执行，直到 return 后，再执行就返回 underfined，

第一次调用，Generator函数开始执行，直到遇到第一个yield语句为止。next方法返回一个对象，它的value属性就是当前yield语句的值hello，done属性的值false，表示遍历还没有结束。

**yield语句 **

yield 语句其实就是暂停标志，

```
function* gen() {
  yield  123 + 456;
}
var a = gen();
a.next();
// { value: 579, done: false }
a.next();
// { value: underfined, done: true }
```

一定要清楚一点，Generator 函数不会赋值就执行，只有在 next 才会执行，

配合 iterator 更好，next 函数，

```
var myIterable = {};
myIterable[Symbol.iterator] = function* () {
  yield 1;
  yield 2;
  yield 3;
};

[...myIterable] // [1, 2, 3]
```

** for of**

此时不用遍历

```
function *foo() {
  yield 1;
  yield 2;
  yield 3;
  yield 4;
  yield 5;
  return 6;
}

for (let v of foo()) {
  console.log(v);
}
// 1 2 3 4 5
```

**Generator.prototype.throw() **

**yield\*语句 **

yield 函数后面跟着一个 yield 函数，表示 for of

```
function* concat(iter1, iter2) {
  yield* iter1;
  yield* iter2;
}

// 等同于

function* concat(iter1, iter2) {
  for (var value of iter1) {
    yield value;
  }
  for (var value of iter2) {
    yield value;
  }
}
```

如果 yield 后面加 * 并且跟了一个数组，表示数组每一项都是一个单独的 yield，

```
function* gen(){
  yield* ["a", "b", "c"];
}

gen().next()
// { value:"a", done:false }
```

然后又 Inerator 接口的数据结构，都可用 yield * 的方法，

```
let read = (function* () {
  yield 'hello';
  yield* 'hello';
})();

read.next().value // "hello"
read.next().value // "h"
```

**取出嵌套数组的成员**

```
function* iterTree(tree) {
  if (Array.isArray(tree)) {
    for(let i=0; i < tree.length; i++) {
      yield* iterTree(tree[i]);
    }
  } else {
    yield tree;
  }
}

const tree = [ 'a', ['b', 'c'], ['d', 'e'] ];

for(let x of iterTree(tree)) {
  console.log(x);
}
// a
// b
// c
// d
// e
```

当然取出嵌套数组，还有其他办法，此方法只是作为参考。

因为 yield 函数不支持 this，但是可以通过气体方法将 this 帮到其他对象上面，比如：

```
function* F() {
  this.a = 1;
  yield this.b = 2;
  yield this.c = 3;
}
var obj = {};
var f = F.call(obj);

f.next();  // Object {value: 2, done: false}
f.next();  // Object {value: 3, done: false}
f.next();  // Object {value: undefined, done: true}

obj.a // 1
obj.b // 2
obj.c // 3
```

如果将 `F.call(obj)` 改成 `F.call(F.prototype)` 就可以实现在 F 对象上面进行赋值操作。

顺便可以将 F 改成函数的方法，

```
function* gen() {
  this.a = 1;
  yield this.b = 2;
  yield this.c = 3;
}

function F() {
  return gen.call(gen.prototype);
}

var f = new F();

f.next();  // Object {value: 2, done: false}
f.next();  // Object {value: 3, done: false}
f.next();  // Object {value: undefined, done: true}

f.a // 1
f.b // 2
f.c // 3
```

