## 二进制和八进制表示法

这个很实用，0b 0B 0o 0O

```
0b111110111 === 503 // true
0o767 === 503 // true
```

## Number.isFinite(), Number.isNaN() Number.isInteger() Number.isSafeInteger() 

Number.isFinite() 用来检测是否有限，一直以为 es5 就有 isNaN 函数，

```
Number.isInteger(25) // true
Number.isInteger(25.0) // true
Number.isInteger(25.1) // false
Number.isInteger("15") // false
Number.isInteger(true) // false
```

## Math 对象的扩展

trunc -> 去除小数部分；sign -> 正数负数 0 ；cbrt -> 立方根；clz32 -> 返回 32 位表示前面有多少个 0；imul -> 32 位相乘；fround -> 单精度；hypot -> 平方和的平方根；expm1(x) -> e 的 x 次方减一；log1p -> log(1+x)；log10；log2；三角函数（ps ：好多方法我以为都是 es5 的。。。）

## 指数运算

```
2 ** 2 //4
2 ** 3 //8
//注意下面
var a = 2;
a **=2; //4
var b = 2;
b **=3; //8
```