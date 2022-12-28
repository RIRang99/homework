## 防抖 debounce

**防抖的定义**：在事件被触发n秒后再执行回调，如果在这n秒内又被触发，则重新计时。

**实质**：闭包和定时器的搭配使用。

**优点**：减少向后端请求数据的次数，降低服务器的压力。

**应用场景**：1. 搜索框输入查询的时候，只有当用户输入完关键字并等待一定时间后才会向后端请求数据。

2. 鼠标连续点击按钮提交。

3. 窗口页面的resize事件，不断调整浏览器窗口大小会不断触发这个事件监听，用防抖让代码只执行一次。 

   

```js
// 基本格式
// 1.用表达式将事件触发后执行的代码单独写出来。
const input = document.querySelector('input')

// 函数表达式
const sendMsg = function(){
    console.log('我爱扇宝')
}

// 封装防抖函数debounce
// 格式：闭包加定时器，外层作用域声明定时器
const debounce = (fn,ms)=>{
    // fn为监听事件后执行的参数，ms为等待执行代码的时间，单位毫秒
    let timerId // 声明一个定时器
    return function(...args){
        clearTimeout(timerId)
        timerId = setTimeout(()=>{
            fn.apply(this,args)
        },ms)
    }
}

// 给事件源绑定监听事件
input.addEventListener('keyup',debounce(sendMsg,300)).bind(input,...arr)

//1.绑定事件时debounce直接小括号调用并传参

//2.return
//return外部的函数立即执行，return内部的函数在接收debounce通过监听事件执行后才调用，所以需要将定时器的函数写在return内，而声明定时器写在return外。

//3.timerId
//声明一个定时器放在return外面，当防抖时，在return内清除定时器，再重新开启定时器。
//当第一次执行debounce时，清除定时器为undefined
//后续执行防抖时，清除的定时器就是上一次设置的定时器

//4.箭头函数和this指向
// 在不使用防抖函数的时候，sendMsg这个函数内部的this指向的是调用它的事件源，在这个例子中指向input，但在防抖函数中使用sendMsg时，由于sendMsg处于计时器内部，而计时器内部的this指向window，导致防抖函数改变了sendMsg的this指向，因此需要将它改回来

const debounce = (fn,ms=3000)=>{
    let timerId
    return function(){
        clearTimeout(timerId)
        //在重启计时器时用箭头函数书写
        timerId = setTimeout(()=>{
            //箭头函数内部的this指向为上层作用域的this
            //相当于这里面的this为上层作用域function的this
            //function的this为谁调用指向谁，在事件监听中input调用防抖，防抖返回function，因此function的this指向input，计时器用箭头函数书写，它内部的this指向和function相同，也为input
            //因此改变fn的this，只需要在计时器内部改变fn的this指向为计时器内部作用域的this
            fn.call(this)
        },ms)
    }
}


//5.debounce接收参数
//debounce作为表达式的函数，接收参数的方法为执行debounce后.bind,bind可以接收参数，并改变debounce的this指向。
debounce(sendMsg,3000).bind(this,1,2)
//debounce接收的参数会对应传递给sendMsg
const sendMsg = function(x,y){
    console.log('发送请求')
    console.log(x+y)
}

//传递给定时器内
const debounce = (fn,ms)=>{
    let timerId
    //使用剩余参数，args变为真数组，在监听事件内写的debounce的参数会以数组的形式传入function中
    return function(...args){
        clearTimeout(timerId)
        timerId = setTimeout(()=>{
            fn.apply(this,args)
            //fn.call(this,...args)
            //fn.call,fn.apply都会立即调用fn
        },ms)
    }
}

以上
```

