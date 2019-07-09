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





