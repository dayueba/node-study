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

## session相关的配置

具体配置可以参考 官方文档

```
app.keys = ['some secret key']

const CONFIG = {
  key: 'koa:sess',
  maxAge: 10 * 1000,
  autoCommit: true,
  overwrite: true,
  httpOnly: true,
  signed: true,
  rolling: false,
  renew: false,
}

app.use(session(CONFIG, app))
```

## 实现登陆/登出借口

* 登陆：如果用户存在，则通过 创建session， 保存到本地，并通过Set-Cookie将session id保存到用户侧
* 登出：销毁session， 并清楚cookie

```
// 登陆
router.post('/login', async function (ctx, next) {
  let sess = ctx.session;
  const {username, password} = ctx.request.body
  let user = findUser(username, password);

  if(user){
    ctx.session.userinfo = {
      username: username,
    };
    ctx.body = {ret_code: 0, ret_msg: '登录成功'};

  }else{
    ctx.body = {ret_code: 1, ret_msg: '账号或密码错误'};
  }
})


// 登出
router.get('/logout', async function (ctx, next) {
  // To destroy a session simply set it to null:
  ctx.session = null;
  ctx.body = {ret_code: 0, ret_msg: '退出登陆成功'}
})
```

## 登陆态判断

用户访问[http://127.0.0.1:3000时，判断用户是否登陆](http://127.0.0.1:3000时，判断用户是否登陆)

```
router.get('/', async (ctx, next) => {
  let loginUser = ctx.session.userinfo
  let isLogined = !!loginUser

  ctx.body = {
    isLogined: isLogined,
    userinfo: loginUser || ''
  }
})
```

## 使用redis存储session

// todo

