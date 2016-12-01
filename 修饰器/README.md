ES7 中提案，但目前已经 babel 支持。

## 类的修饰

修饰器可以在代码编译阶段运行代码。

```
function testable(target) {
  target.isTestable = true;
}

@testable
class MyTestableClass {}

console.log(MyTestableClass.isTestable) // true
```

修饰器的工作原理：

```
@decorator
class A {}

// 等同于

class A {}
A = decorator(A) || A;
```

## 方法的修饰

