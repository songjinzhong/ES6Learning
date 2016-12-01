## 0 == null

## 数组的空位

```
const a1 = [undefined, undefined, undefined];
const a2 = [, , ,];

a1.length // 3
a2.length // 3

a1[0] // undefined
a2[0] // undefined

a1[0] === a2[0] // true
```

数组的空位，被省略的内容虽然是 undefined，但是与 undefined 又本质的区别。

## map

对于空位数组， map 并不会去处理，

```
const arr = [, , ,];
arr.map(n => {
  console.log(n);
  return 1;
}) // [, , ,]
```
