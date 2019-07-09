### 安装node.js的mysql模块

```
npm i mysql --save
```

## 开始使用

### 创建数据库会话

    const mysql = require('mysql')
    const connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '123',
        database: 'microblog'
    })

    connection.query(`select * from users`, (error, results, fields) => {
        if( error ) throw error

        // 处理查询出来的数据

        // 结束会话
        connection.release()
    })

注意：一个事件就有一个从开始到结束的过程，数据库会话操作执行完后，就需要关闭掉，以免占用连接资源。

###  创建数据库连接池

```
const pool = mysql.createPool({
    host: 'localhost',
    user: 'root',
    password: '123',
    database: 'microblog'
})

pool.getConnection((err, connection) => {
    connection.query('select * from users', (error, results, fields) => {
        // 结束会话
        connection.release()
        
        // 如果有错误就抛出
        if (error) throw error
    })
})
```

### promise封装执行操作的函数

```
const query = sql => {
    return new Promise(((resolve, reject) => {
        pool.getConnection((err, connection) => {

            if( err ){
                reject(err)
                return
            }

            connection.query(sql, (error, rows) => {

                // 如果有错误就抛出
                if (error) reject(error)
                else resolve(rows)

                // 结束会话
                connection.release()
            })
        })
    }))
}

```

### 使用async/await

```
const getAllUsers = async () => {
    try {
        const sql = 'select * from users'
        return await query(sql)
    } catch (e) {
        console.log(e)
        return []
    }
}
```



