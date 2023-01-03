### Promise.then的第二个参数和.catch

```js
let p = new Promise((resolve, reject) => {
      resolve('22')
      // throw new Error('test')
    })
    // 如果是在promise内部抛出的错误，.then的第二个参数和.catch都可以捕获到他
    // 如果是在promise内部不抛出的错误，而是在外部（.then里面的第一个参数中），只有.catch可以捕获到它
    p.then(
      (res) => {
        throw new Error('test')
      },
      (err) => {
        console.log('err', err)
      }
    ).catch((err1) => {
      console.log('err1', err1)
    })
     // then的第二个参数会在失败的时候触发（只要你写了）
      // then的第二个参数就和catch都写了的时候，会优先触发第二个参数
```



### Promise的三种状态

- *待定（pending）*：初始状态，既没有被兑现，也没有被拒绝。
- *已兑现（fulfilled）*：意味着操作成功完成。
- *已拒绝（rejected）*：意味着操作失败。

当页面加载时，一开始promise就处于待定状态pending