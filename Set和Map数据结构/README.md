## set

set 类似于数组，但是值都是唯一的，

```javascript
var s = new Set();

[2, 3, 5, 4, 5, 2, 2].map(x => s.add(x));

for (let i of s) {
  console.log(i);
}
// 2 3 5 4
```

数组去重的方法

```
// 去除数组的重复成员
[...new Set(array)]
```

set 不会对类型进行改变，5 盒 "5" 时不同的

array.from 也可以对数组进行去重，它接受一个 set 类型的对象，

```
var items = new Set([1, 2, 3, 4, 5]);
var array = Array.from(items);
```

由于 set 只有键值，所以 key、values、entries 方法都只会返回键值或键值键值键值对，foreach 也一样，

```
let set = new Set([1, 2, 3]);
set.forEach((value, key) => console.log(value * 2) )
// 2
// 4
// 6
```

## WeakSet 

WeakSet 与 set 类似，WeakSet 的成员只能是对象，而不能是其他的值，WeakSet 的对象是弱引用，

```
var a = [[1,2], [3,4]];
var ws = new WeakSet(a);
```

## Map

它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object结构提供了“字符串—值”的对应，Map结构提供了“值—值”的对应，是一种更完善的Hash结构实现。

```
var m = new Map();
var o = {p: 'Hello World'};

m.set(o, 'content')
m.get(o) // "content"

m.has(o) // true
m.delete(o) // true
m.has(o) // false
```

**实例的属性和操作方法 **

size，set(key,value),get(key),has(key),delete(key), clear()。

**与其他类型相互转换**

数组

```
let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
[...myMap]
// [ [ true, 7 ], [ { foo: 3 }, [ 'abc' ] ] ]
//数组转 map
new Map([[true, 7], [{foo: 3}, ['abc']]])
// Map {true => 7, Object {foo: 3} => ['abc']}
```

对象

```
function strMapToObj(strMap) {
  let obj = Object.create(null);
  for (let [k,v] of strMap) {
    obj[k] = v;
  }
  return obj;
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToObj(myMap)
// { yes: true, no: false }
```

Json

```
function strMapToJson(strMap) {
  return JSON.stringify(strMapToObj(strMap));
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToJson(myMap)
// '{"yes":true,"no":false}'
```

## WeakMap 

WeakMap结构与Map结构基本类似，唯一的区别是它只接受对象作为键名（null除外），不接受其他类型的值作为键名，而且键名所指向的对象，不计入垃圾回收机制。

