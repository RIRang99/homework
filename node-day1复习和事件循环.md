#### fs  ==> file system

```js
1. 读文件 
const res = fs.readFileSync(路径, 'utf-8')
2. 写文件
fs.writeFileSync(路径)
```

#### path路径

```js
动态路径拼接的问题 
node js文件名 
node '/test/app.js'   
===> 绝对路径解决 

1. __dirname 返回当前文件所处的文件夹的绝对路径
2. __filename 返回当前文件的绝对路径

const fullPath = path.join(__dirname, '相对路径') 
```

#### http模块

```js
// 1. 导入模块
const http = require('http')
// 2. 创建一个server
const server = http.createServer()
// 3. 启动服务，监听端口
server.listen(3000, () =>{
    console.log('running')
})
// 4. 监听请求 request
server.on('request', (request, response) => {
    // request请求
    // 1. request.url 请求地址
    // 2. request.method 请求方法
    
    // response响应
    // 1. res.statusCode 响应状态码
    // 2. res.setHeader() 设置响应头
    // 3. res.end(数据) 返回给浏览器的数据  数据==> 字符串格式
})
```

#### 事件循环EventLoop

```js
宏任务
1. script代码块 
2. setTimeout
3. setInterval
4. setImmediate

微任务
1. promsie.then() .catch()
2. async await 
3. process.nextTick
4. MutationObserver

script代码块，一开始相当于执行第一个宏任务
1. 先执行完所有的同步代码
2. 遇到宏任务放到宏任务队列中
3. 遇到微任务就放到微任务队列中 
4. 清空所有微任务队列中的所有微任务  ===> 这一次的宏任务结束 Tick
5. 再执行下一个宏任务 

==> 拔出萝卜带出泥 
```

