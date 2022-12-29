## 节流throttle

**定义**：持续地触发事件，在一段时间内，只允许函数执行一次//减少一段时间内，事件的触发频率。

**应用场景**：1. 浏览器窗口缩放 ，resize事件。

2. scroll滚动事件 / mousemove 事件等。

节流中只存在一个定时器，不需要每次点击后都清空重开定时器

节流是在一段时间内，不管事件触发多少次，代码只执行一次

防抖时在事件触发后的一段时间内，如果事件再次触发，计时器就清空重来，直到这段时间内没有再次触发事件，代码才会执行一次。

```js
// 节流定时器版本
// 需求，鼠标在盒子里移动，每隔三秒才会执行一次函数
const box = document.querySelector('.box')

//单独拿出执行函数
const move = ()=>{
    // 鼠标移动，i加1
    box.innerHTML += 1
    
}

// 节流一下
const throttle = (fn,ms)=>{
    声明一个定时器
    let timerId
    return function(){
        // 如果没有定时器，就开启定时器
        if(!timerId){
            timerId = setTimeout(()=>{
                fn.apply(this,arguments)
                timerId = null
            },ms)
        }
        
    }
    
}

 box.addEventListener('click', throttle(fn, 3000))

//让我来详细解说下流程
// 我在box里点击一下
// throttle节流被激活
// 第一步 throttle声明了一个叫做timerId的变量
// 第二步 此时timerId的值为undefined ，节流函数return了一个方法判断
// 第三步 如果timerId为假，则继续执行后面的函数，因为此时timerId为undefined，所以为假，符合条件继续执行。
// 第四步 设置一个定时器，并将定时器的id/即这是在全篇代码中运行的第几个计时器以num的形式返回一个数字给timerId,此时timerId = 1
// 第五步 定时器内执行操作，在3秒后调用fn函数/即真正想进行的操作，并apply改回它的this指向为事件源，以伪数组arguments的形式接收参数
// 第六步 timerId 的值改为null/空，定时器结束运行。  
-----------------------------------------------------------------------------------
// 当第二次点击box时,如果此时三秒还没过
// throttle节流被激活
// 因为三秒还没过，此时定时器内的函数还没执行操作，timerId的值还是没改之前的1 
// timerId被声明，值还是1 
// 进行if判断，timerId为1，为真，不进行后续代码，结束运行。
-----------------------------------------------------------------------------------
// 当第二次点击box时，如果三秒已经过去 
// timerId的值变为null，并在一开始let声明再次被赋为null，为假
// 进行if判断符合条件，执行后续代码
// timerId被重新赋值，此时因为是第二个定时器，timerId的值被改为2
// 第五步 定时器内执行操作，在3秒后调用fn函数/即真正想进行的操作，并apply改回它的this指向为事件源，以伪数组arguments的形式接收参数
// 第六步 timerId 的值改为null/空，定时器结束运行。  
```

