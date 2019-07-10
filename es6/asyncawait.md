用同步的方法来写异步

* 可以让异步逻辑用同步写法实现
* 最底层的await返回需要是Promise对象
* 可以通过多层 async function 的同步写法代替传统的callback嵌套



async 修饰 function，说明这是一个异步的方法

await 后面可以跟 Promise 和其他 async 函数，也可以跟普通的同步函数。假如其后跟的是普通的同步函数，则行为跟普通同步函数一样。



使用async/await 之后，就可以直接通过 try/catch 来捕获错误。



可以让异步逻辑用同步写法实现

最底层的await返回需要是Promise对象

可以通过多层 async function 的同步写法代替传统的callback嵌套

