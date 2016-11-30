## Promise 的含义

Promise 是异步编程的一种解决方案，比回掉函数和事件更合理、更强大。

Promise 是一个容器，里面保存某个未来才会结束的事件，通常是异步操作，有以下特点：

1. 对象不受外界的影响，只有一步操作的结果，才会决定当前是哪一种状态；
2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果，状态改变有两种结果，从Pending变为Resolved和从Pending变为Rejected，状态改变之后，即使添加回掉函数，也不在变。

## 基本用法

一个 Promise 的实例，

```
var promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

resolve 是指状态从未改变到成功，而 reject 指从未改变到失败，然后用 then 来接受两个回掉函数作为参数。

下面可以测出 Promise 函数具体的执行时间，只有当所有同步函数执行完之后才会执行 Promise 函数：

```
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('Resolved.');
});

console.log('Hi!');

// Promise
// Hi!
// Resolved
```

比如用 Promise 实现异步加载图片：

```
function loadImageAsync(url) {
  return new Promise(function(resolve, reject) {
    var image = new Image();

    image.onload = function() {
      resolve(image);
    };

    image.onerror = function() {
      reject(new Error('Could not load image at ' + url));
    };

    image.src = url;
  });
}
```

比如还可以有一个异步 Ajax 请求，

```
var getJSON = function(url) {
  var promise = new Promise(function(resolve, reject){
    var client = new XMLHttpRequest();
    client.open("GET", url);
    client.onreadystatechange = handler;
    client.responseType = "json";
    client.setRequestHeader("Accept", "application/json");
    client.send();

    function handler() {
      if (this.readyState !== 4) {
        return;
      }
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };
  });

  return promise;
};

getJSON("/posts.json").then(function(json) {
  console.log('Contents: ' + json);
}, function(error) {
  console.error('出错了', error);
});
```

## Promise.prototype.then() 

then 方法是在 prototype 上面的，then 返回的不是之前的那个对象，而是一个新对象，所以可以用链式来调用，以为 Promise 的状态只能改变一次。

```
getJSON("/posts.json").then(function(json) {
  return json.post;
}).then(function(post) {
  // ...
});
```

**Promise.call, Promise.catch, Promise.race, Promise.resolve, Promise.reject, **

**还有两个附加的方法，done 和 finally