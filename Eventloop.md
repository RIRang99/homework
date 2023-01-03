### Eventloop

```js
 setTimeout(function () {
      console.log(1)
    })
    new Promise(function (resolve, reject) {
      console.log(2)
      resolve(3)
    }).then(function (val) {
      console.log(val)
    })
    console.log(4)
        // 2 4 3 1
        // js异步执行列表中包含宏任务和微任务
        // 宏任务：计时器
        // 微任务：promise.then
        // 先执行同步执行列表，然后执行主线程的微任务，然后宏任务
```

**事件循环**（eventloop）:
1、主线程上面的同步代码，
2、取出微任务列表里面所有的微任务，全部执行
3、取出宏任务队列里面的一个宏任务，执行
4、继续执行第2步
5、继续执行第3步
6、继续执行第2步
7、继续执行第3步

```js
 <script>
      console.log(1)

      setTimeout(function () {
        console.log(2)
        new Promise(function (resolve) {
          console.log(3)
          resolve()
        }).then(function () {
          console.log(4)
        })
      })

      const p = new Promise((resolve, reject) => {
        console.log(5)
        resolve() // 标记为成功
        console.log(6)
      })

      p.then((data) => {
        console.log(7)
      })

      console.log(8)
      //1 5 6 8 7 2 3 4
    </script>
```

