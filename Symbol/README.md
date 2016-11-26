Symbol 和 null underfined boolean string number object 一样成为数据类型

Symbol函数前不能使用new命令，

```
var s1 = Symbol('foo');
var s2 = Symbol('bar');

s1 // Symbol(foo)
s2 // Symbol(bar)

s1.toString() // "Symbol(foo)"
s2.toString() // "Symbol(bar)"
```

## 属性名的遍历

`Object.getOwnPropertySymbols` 可以获得，其他均不可以获得对象的 Symbol 属性。

## Symbol.for()，Symbol.keyFor() 

Symbol.for() 会先查看当前对象是否有 Symbol 值，不会每一次都返回一个新的 Symbol，

```
Symbol.for("bar") === Symbol.for("bar")
// true

Symbol("bar") === Symbol("bar")
// false
```

Symbol.keyFor() 返回一个已经登记的 Symbol 类型的 key，

```
var s1 = Symbol.for("foo");
Symbol.keyFor(s1) // "foo"

var s2 = Symbol("foo");
Symbol.keyFor(s2) // undefined
```

## 内置的Symbol值 

下面就不看了，感觉看了也记不住。。

