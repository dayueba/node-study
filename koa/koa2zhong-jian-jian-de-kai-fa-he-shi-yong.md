## async中间件开发

log中间件

```
// middleware/log.js
function log(ctx) {
    console.log( ctx.method, ctx.header.host+ctx.url )
}

module.exports = function () {
    return async (ctx, next) => {
        log(ctx)
        await next()
    }
}
```

## 中间件的使用

```
const log = require('./middleware/log')
app.use(log())
```



