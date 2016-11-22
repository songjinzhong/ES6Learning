## 构造函数合法化

`var regex = new RegExp(/xyz/, 'i');` 已经合法

## u 修饰符 

处理 unicode 大于 `\uffff` 情况，加上 u 之后，. 可以识别这种情况，

`/^.$/u.test('\uD83D\uDC2A')`

## y 修饰符

粘连 的意思表示，全局情况，下一次匹配必须从第一个字符开始

```
'aaa_aa_a'.match(/a+/g)
// ["aaa", "aa", "a"]
'aaa_aa_a'.match(/a+/y)
// ["aaa"]
'baaa_aa_a'.match(/a+/y)
// null
```

关于 y 的检测，

```
var r = /hello\d/y;
r.sticky // true
```

## flags

返回 flag，（ps：这个我以为 es5 就自带的呢。。）

## 后行断言

据说修改 chrome flags 就可以用了，试了还是没用。

