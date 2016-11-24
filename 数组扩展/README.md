## Array.from

这个函数可以将类似数组的对象转换成数组，比如 arguments 参数和 document.querySelectorAll() 的返回值，他们都不是数组，可以通过这个方法返回数组。

```
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};

// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```

只要部署迭代器接口的，都可以用 from 函数：

```
Array.from("hello");
//["h", "e", "l", "l", "o"]
Array.from([0, 1, 2]);
//[0, 1, 2]
```

参数是数组的话，会返回原数组。

接受第二个参数函数，和 map 方法一样，对每一个参数就行处理。

## Array.of()

将一组值返回数组，

```
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1

// Array 方法的缺陷
Array() // []
Array(3) // [, , ,]
Array(3, 11, 8) // [3, 11, 8]
```

## 数组实例的copyWithin() 

看不懂这个函数要干啥

## 数组实例的find()和findIndex() 

找到满足的实例，参数是函数，找到返回该元素，找不到 underfined，findIndex() 返回的是位置而不是元素，

```
[1, 4, -5, 10].find((n) => n < 0)
```

## 数组实例的entries()，keys()和values() 

这方法，真是不知道有啥用，

```
let letter = ['a', 'b', 'c'];
let entries = letter.entries();
console.log(entries.next().value); // [0, 'a']
console.log(entries.next().value); // [1, 'b']
console.log(entries.next().value); // [2, 'c']
```

## includes()

可以传递两个参数，第一个表示比较的值，第二个参数表示比较的开始位置，负数采用补数，

主要还是看 indexOf() 的差异，两点，返回值为 -1，需要比较结果，没有 true false 来的直接，第二点，`[NaN].indexOf(NaN)` 无法比较。

## 数组空位的处理

将空位改变成 underfined，ES5 对于数组空位是不会处理的，forEach(), filter(), every() 和some()都会跳过空位，很多函数对空位的处理不同。