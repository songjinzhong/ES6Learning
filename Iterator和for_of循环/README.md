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

makeiterator 