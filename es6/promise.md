解决异步编程  避免回调地狱

简单说就是一个容器，里面保存着某个未来才会结束的事件的结果（一般是异步的结果）

```
// demo
const fs = require('fs')
const path = require('path')  // 后面获取文件路径时候会用到
const readFilePromise = function (fileName) {
    return new Promise((resolve, reject) => {
        fs.readFile(fileName, (err, data) => {
            if (err) {
                reject(err)  // 注意，这里执行 reject 是传递了参数，后面会有地方接收到这个参数
            } else {
                resolve(data.toString())  // 注意，这里执行 resolve 时传递了参数，后面会有地方接收到这个参数
            }
        })
    })
}
```

* 执行`resolve`传递的值，会被第一个`then`处理时接收到
* 如果`then`有链式操作，前面步骤返回的值，会被后面的步骤获取到

在若干个`then`串联之后，我们一般会在最后跟一个`.catch`来捕获异常，而且执行`reject`时传递的参数也会在`catch`中获取到。这样做的好处是：

* 让程序看起来更加简洁，是一个串联的关系，没有分支（如果用`then`的两个参数，就会出现分支，影响阅读）
* 看起来更像是`try - catch`的样子，更易理解

### `Promise.all`和`Promise.race`的应用

.all\(\)等每个promise都执行完 再执行接下来的操作

.race\(\)只要有一个promise执行结束就执行接下来的操作

all 方法接受一个 Promise 对象的数组，当所有 Promise 都返回的时候才会执行 then 后面的方法，假如有任何一个 Promise 返回错误，则都将失败而调用 catch 里面的回调。all 方法通常用来处理并行关系。而 race 的参数跟 all一致，只不过 race 只会返回一个最快完成的 Promise，也就是谁快就返回谁。

### Promise/A+

异步模式编程规范

关于状态

* promise 可能有三种状态：等待（pending）、已完成（fulfilled）、已拒绝（rejected）
* promise 的状态只可能从“等待”转到“完成”态或者“拒绝”态，不能逆向转换，同时“完成”态和“拒绝”态不能相互转换

**关于**`then`**方法**

* promise 必须实现`then`方法，而且`then`必须返回一个 promise ，同一个 promise 的`then`可以调用多次（链式），并且回调的执行顺序跟它们被定义时的顺序一致
* `then`方法接受两个参数，第一个参数是成功时的回调，在 promise 由“等待”态转换到“完成”态时调用，另一个是失败时的回调，在 promise 由“等待”态转换到“拒绝”态时调用



