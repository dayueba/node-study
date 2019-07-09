## 文档概要

本文基于koa实现了简易的登录/登出功能，完整的代码示例可以在[这里](https://github.com/chyingp/nodejs-learning-guide/tree/master/examples/2016.12.06-session)找到。

## 环境初始化

 首先， 初始化项目

```
koa2 auth-koa2
```

 然后，安装依赖

```
npm i
```

 接着，安装session相关的包

```
npm i --save koa-session redis koa-redis
```



