### 箭头函数的this指向

```js
// this指向 可以理解为等于，代表谁
// this指向在定义的时候不能确定，只有调用执行的时候才能确定

//1. 全局作用域 / 普通函数调用 / 定时器 this指向的是window
console.log(this) // window

function fn() {
    console.log(this)
}
fn() // window

setTimeout(function(){
    console.log(this)
},1000) //window

//2.对象方法调用中，谁调用这个方法，this指向谁
const obj = {
    name:'扇宝'，
    age: 6,
    sayHi: function(){
        console.log(this)
    }
}
let fun = obj.sayHi 
fun() // window中调用fun，this指向fun

//3.事件注册的时候，this指向被绑定的元素
const btn = document.querySelector('button')
btn.addEventListener('click',function(e){
    console.log(this) // 绑定事件的元素
    console.log(e.target) // 触发事件的元素
    console.log(e.currentTarget) // 绑定事件的元素
})

//4.构造函数中，this指向的是实例对象
function Person(name,age){
    this.name = name,
    this.age = age
    console.log(this)
}

// 5.原型方法里面，this指向的是实例对象
Parent.prototype.sayhi = function (){
    console.log('hi')
    console.log(this)
}
const p = new Parent('灰灰',9)
const p2 = new Parent('超超',10)
```

