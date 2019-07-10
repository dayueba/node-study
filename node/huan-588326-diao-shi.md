## CommonJS 模块管理规范

每个文件是一个模块 有自己的作用域 

在模块内部module变量代表模块本身 

module.exports属性代表模块对外接口

require /表示绝对路径 ./相对路径 支持js.json.node扩展名 不写依次尝试 不写路径则认为是build-in模块或者各级node\_modules内的三方模块

module被加载时时执行 加载后缓存 一旦出现某个模块被循环加载,就只输出已经执行的部分, 还未执行的部分不输出

#### module.export & export

export默认情况下和module.export一样 但是不能修改export的指向

## global 全局对象

## process

argv argv0 execArgv execPath

## 调试

Inspector 使用ide

