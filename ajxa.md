## ajxa



**定义**：使用XMLHttpRequest异步对象和服务器通信，在不重新刷新页面的情况下与服务器通信，交换数据，更新页面。

### 接口

**定义**：使用ajax和服务器通讯时，被请求的URL地址

1. `ajax`请求的服务器一般称之为:**接口服务器**

2. 接口服务器一般提供操纵服务器数据的**一系列方法**

3. **调用(请求)接口**有点类似于**调用后端封装好**的**函数**

4. 工作中接口一般由后端工程师编写，并提供**接口文档**指导调用

接口调用首先要引入在线的js文件

https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js

### 请求方法

客户端浏览器在请求服务器时，根据**操作性质**的不同，可以分为以下 **5 种常见**的操作:

| 序号 | 请求方式 |                             描述                             |
| :--: | -------- | :----------------------------------------------------------: |
|  1   | POST     |                    向服务器新增数据(传递)                    |
|  2   | GET      |                       从服务器获取数据                       |
|  3   | DELETE   |                      删除服务器上的数据                      |
|  4   | PUT      | `更新服务器上的数据(侧重于完整更新:例如更新用户的完整信息) ` |
|  5   | PATCH    | `更新服务器上的数据(侧重于部分更新:例如只更新用户的手机号) ` |

除了这**5**种以外还有一些其他的方法，比如`OPTIONS`,`HEADER`等,可以参考如下接口确认是否符合

### 语法

```js

<script scr="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
document.querySelector('button').addEventListener('click',()=>{
    axios({
	//根据请求方式决定传参的属性名 post => data  //  get => params
        url:'接口的路径名'
        method:'请求方式 post/get'
        data/params:{
        //根据接口文档来，需要什么参数就传什么参数
        uername:'admin',
        password:'123456',
    },
    }).then((res)=>{
        //res为接口返回的参数
        console.log(res)
    })
})
```



### serialize

**作用**：简化了表单内取值。

```js
// 当引入form-serialize的js文件后，开启{hash:true}，会将表单内的控件以{name:name所指控件对应的value值}的形式呈现
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script src="../03-源代码/00.knowledges/lib/form-serialize.js"></script>
<script>
  const form = document.querySelector('form')
  // 阻止表单的默认注册行为
  form.addEventListener('submit', (e) => {
    e.preventDefault()
    // const form1 = document.querySelector('form')
    const data1 = serialize(this, { hash: true })
    console.log(data1)
    axios({
      url: 'http://ajax-api.itheima.net/api/data',
      method: 'post',
      // data: {
      //   uername: document.querySelector('[name=username]').value,
      //   food: document.querySelector('[name=food').value,
      //   sign: document.querySelector('[name=sign]').value
      // }
      data: data1
    }).then((res) => {
      console.log(res)
    }).catch(
      (error) => {
        console.log('error')
        console.log(error)
      }
    )
  })
</script>
```

### formData

#### 概念:

1. `FormData`是浏览器提供的内置对象
2. 以`key/value`的形式保存数据
3. 能够结合`ajax`进行数据提交

### 常用语法:

1. 通过`new`关键字实例化
2. `.append(key,value)`添加数据
3. `.get(key)`获取`key`对应的值
4. 可以保存文件

```js
// 实例化时传入Form表单 自动获取数据
const data = new FormData(form表单)
// 直接输出看不到数据
console.log(data)
// 通过get方法获取对应的值
console.log(data.get('username')) 
console.log(data.get('email'))
console.log(data.get('habbit'))

// 添加键值对
data.append('friend','jack')
console.log(data.get('friend')) // jack
```

### FormData

onchange的触发条件是内容改变/即当你用鼠标点击了一个不同的文件

files是伪数组
