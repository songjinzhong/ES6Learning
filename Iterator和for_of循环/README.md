## Iterator（遍历器）的概念 

现在 ES6 共有四种集合结构类型，如对象，数组，Map

遍历器的作用大概如下：

1. 创建一个指针对象，只想当前对象的开始位置；
2. 每一次调用 next 方法，指向下一个元素；
3. 不断调用 next 直到结束。

```
var it = makeIterator(['a', 'b']);

it.next() // { value: "a", done: false }
it.next() // { value: "b", done: false }
it.next() // { value: undefined, done: true }
```

makeiterator 是一个遍历器生成器，会返回每个对象。

**数据结构的默认 Iterator 接口**

```
const obj = {
  [Symbol.iterator] : function () {
    return {
      next: function () {
        return {
          value: 1,
          done: true
        };
      }
    };
  }
};
```

通过这种自己定义的方法，就可以使得 iterator.next value值为 1。

有三种数据结构原生具备 Iterator 接口，数组，某些类似数组的对象，Set 和 Map，

**调用 Iterator 的场合**

1. 解构赋值回调用，`let [first, second] = new Set().add('a').add('b')`;
2. 扩展运算符 ... 也会用到，`['a',..['b', 'c'], 'd']`;
3. for of, Array.from(), Map(), Set(), WeakMap(), WeakSet();

**字符串的 Inerator 接口**

## for...of循环 

对于默认部署了 Inerator 方法的数据结构都可以使用 for of 循环，可用来替代 forEach 方法

JS 种的 for in 方法，只允许获得键名，而 for of 允许获得键值

```
var arr = ['a', 'b', 'c', 'd'];

for (let a in arr) {
  console.log(a); // 0 1 2 3
}

for (let a of arr) {
  console.log(a); // a b c d
}
```

Set 和 Map 一样，可用直接使用，

**key，values，entries()**

这三个也可以分别使用 for of，而且得到的结果很有意思，

```
let arr = ['a', 'b', 'c'];
for (let pair of arr.entries()) {
  console.log(pair);
}
// [0, 'a']
// [1, 'b']
// [2, 'c']
```

entries() 获得的是对象数组

**对象的 for of**

```
var es6 = {
  edition: 6,
  committee: "TC39",
  standard: "ECMA-262"
};

for (e in es6) {
  console.log(e);
}
// edition
// committee
// standard

for (e of es6) {
  console.log(e);
}
// TypeError: es6 is not iterable
```

对象会报错，可用通过 object.keys() 来生成一个