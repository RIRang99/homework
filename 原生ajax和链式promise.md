### 原生ajax

```js
	// post传参JSON
    const btn = document.querySelector('button')
	btn.addEventListener('click',function(){
        //1.实例化异步对象
        const xhr = new XMLHttpRequest()
        //2.设置请求的地址和方法
        xhr.open('post','http://ajax-api.itheima.net/api/data')
        //3.请求头设置，文档需求参数是什么格式就写什么格式
        xhr.setRequestHeader(
        'content-type',
        'application/json')
        //4.注册回调函数，服务器响应内容回来之后触发
        xhr.addEventListener('load',function(){
            console.log(xhr.response)
        })
        let obj = {
            username:'admin',
            password:'123456',
        }
        //原生ajax请求接口返回的数据默认是字符串的格式，想用的话要转化成对象格式 JSON.parse
        
        //5.发送请求
        // 发送请求是的参数要为字符串格式，请求数据是通过JSON.stringify()转化为JSON格式
        xhr.send(obj)
    })
```

### Promise

定义：Promise是一个对象，它代表了一个一步操作的最终完成或者失败。

axios就是基于Promise封装的。

```js
//Promise的链式调用
 function timeoutPromise(delay) {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(`延迟了${delay}秒钟`)
        }, delay * 1000)
      })
    }
    const p = timeoutPromise(1)
      .then((res) => {
        console.log(res)
        return timeoutPromise(2)
      })
      .then((res) => {
        console.log(res)
        return timeoutPromise(3)
      })
      .then((res) => {
        console.log(res)
      })

    //小试牛刀
    // 创建一个函数
    // 内部new一个promise 
    // Promise内部写一个定时器
   
    function timeoutPromise(delay){
        new Promise((resolve,reject)=>{
            setTimeout(()=>{
                resolve('成了')
            },delay*1000)
        })
    }

 // 用表达式创建这个函数
 // .then
// 内部写接受promise返回的函数要干嘛
// return这个函数，传入新参数
const p = timeoutPromise(1)
.then((res)=>{
    console.log(res)
    return timeoutPromise(2)
}).then((res)=>{
    console.log(res)
    return timeoutPromis(3)
}).then((res)=>{
    console.log(res)
})
```

