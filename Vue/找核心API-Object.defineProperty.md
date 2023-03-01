### 找 Vue中 响应式的核心API 

**Object.defineProperty**

---

```js

// src/core/instance/index.ts
function Vue(){
    this._init(options)
}

initLifecycle(vm)
initEvents(vm)
initRender(vm)
callHook(vm, 'beforeCreate', undefined, false /* setContext */)
initInjections(vm) // resolve injections before data/props
initState(vm) // props data 
initProvide(vm) // resolve provide after data/props
callHook(vm, 'created')

===> initState(vm)  ==> 初始化 data props / watch /methods /computed 等

initState,按住ctrl键鼠标点击 ==> 

=> 跳转到instance / state.ts 
65行   执行initData(vm) 这个方法
if (opts.data) {
    initData(vm)
  }
```

![image-20230202101617814](https://zxd-blog-imgs.oss-cn-beijing.aliyuncs.com/imgs/image-20230202101617814.png)

=> observe函数 core/observer/index.ts   => observe函数

![image-20230202101713705](https://zxd-blog-imgs.oss-cn-beijing.aliyuncs.com/imgs/image-20230202101713705.png)

![image-20230202101751356](https://zxd-blog-imgs.oss-cn-beijing.aliyuncs.com/imgs/image-20230202101751356.png)

在defineReactive内部 找到核心的API  Object.defineProperty

![image-20230202101825403](https://zxd-blog-imgs.oss-cn-beijing.aliyuncs.com/imgs/image-20230202101825403.png)



















