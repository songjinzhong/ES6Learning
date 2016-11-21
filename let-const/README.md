## let

### 基本用法

let 和 var 很像，但只在该代码块有效。

```
{
  let a = 10;
  var b = 1;
}

a // ReferenceError: a is not defined.
b // 1
```

for 很适合 let，

### 不存在变量提升

### 暂时性死区，申明即绑定

```
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```

### 不允许重复申明

## const 命令

基本用法

```
const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```

同样有块级，暂时性死区等属性。

当 const 定义指针时，比如

```
const foo = {};
foo.prop = 123;

foo.prop
// 123

foo = {}; // TypeError: "foo" is read-only
```

指针指向的数据可变，但指针的值不可变。