### 细说var的作用域

老子今天就要把var说得仔仔细细

### 作用域

作用域分为全局作用域和局部作用域

**在全局作用域和函数作用域中**

```js
// var在全局作用域中声明变量
console.log(a) // undefined
var a = 10
// 在全局作用域或者函数作用域中，用var声明变量这个步骤会被切割成两步，声明变量步骤提升到当前作用域的最顶层，赋值步骤停留在原地。
// var a = 10 ===> 1. var a     2. a = 10
// 上面的代码等价于
var a
console.log(a) // a===undefined
a = 10

// 再来个例子
function foo(){
    console.log(a) // undefined
    var a = 5
}
console.log(a) // error a not defined
foo()
// 在函数作用域中，等价于
function foo(){
    var a 
    console.log(a) // a === undefined
    a = 5
}
// 当函数被调用,因为a的变量提升被限制在了函数内部的顶层，全局作用域中并没有声明a，所以会报错

```

### 函数内声明相同变量

**当在函数作用域内用var声明了一个变量，而在函数外部用var声明了相同变量，函数外部的变量的值无法延伸到函数内部，而函数内部变量的值也无法影响到外部**

```js
var a = 1
function foo(){
    console.log(a)
    var a = 10
    console.log(a)
}
foo() // undefined , 10
console.log(a) // 1

// 变形一下
var a = 1
function rea(){
    console.log(a)
}
rea() // 1
// 当函数作用域内没有用var声明和外部作用域相同的变量，外部作用域的变量可以渗透到函数作用域内
```

### 函数内声明相同变量前调用return关键字

**return**对于var来说就是一坨浓谢，眉笔用

```js
var a = 1

function foo(){
    console.log(a) // undefined
    a= 10
    var a = 20
    return  a
}
console.log(foo()) // 20
console.log(a) // 1
```

### 块级作用域，即if，for形成的作用域对于var没用

```js
// 块级作用域内用var声明的变量，会提升到块级作用域以上
for(var i = 0;i<btn.length;i++){
    btn[i].addEventListener('click',function(){
        console.log(i)  // 5
    })
}
// for和if生成的块级作用域对于var声明的变量不起作用
var i 
i=0,1,2,3,4,5
for(i=0,1,2,3,4,5){
    btn[0,1,2,3,4]{
        console.log(i)
    }
}
第一，代码执行非常他妈的快，一个循环五次的for，在页面展开的时候就已经全部执行完毕了
第二，执行完毕的结果，是全局作用域中，i最终经过五次循环，等于5
第三，按钮的绑定监听事件，是在事件发生后才会触发函数
第四，打印i，函数作用域内没有var i，那么i的值就会从上级作用域中查找
第五，因为函数的上级作用域是for循环，对于for循环此时已经执行完毕，for内的i赋值与全局作用域中i的赋值一致
等于5
第六，所以打印5

for(let i = 0;i<btn.length;i++){
    btn[i].addEventListener('click',function(){
        console.log(i)  // 0,1,2,3,4
    })
}
for(i = 0){
    btn[0].addEventlistener('click',function(){
        console.log(i) // 在for形成的这个块级作用域里，let声明的i赋值固定为0
    })
}
第一，当用let或const声明变量时，会在for和if内形成块级作用域
第二，每个单独的作用域内，变量的赋值被固定

```

