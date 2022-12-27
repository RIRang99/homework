### call/apply/bind

```js
// 三者都可以改变this指向

1.call
const obj = {
    msg:'hi'
}


function fn(x,y){
    console.log(this)
    return x + y
}

const res = fn(1,2)
console.log(res) // this指向window

// fn.call()
// 1.可以改变this的指向
// 2.调用函数，立即执行，返回执行结果
// 3.fn.call() 第一个参数，就是让this指向哪个对象，后面紧跟的是参数列表

const res2 = fn.call(obj,1,2)
console.log(res2)
const obj2 = {
    name:'hw',
    //getName:function(){}
    getName(){
        console.log(this)
        console.log(this.name)
    }
}
const obj3 = {
    name: 'iphone'
}
// obj2.getName()
// 改变getName里面的this指向，让它指向obj3
obj2.getName.call(obj3) // 可以不接收后面的参数。第一个参数就是this的指向

2.apply
 const obj = {
      msg: 'nihao'
    }
    function fn(x, y) {
      console.log(this)
      return x + y
    }
    const res = fn(1, 2)
    // console.log(res)
    const res2 = fn.apply(obj, [1, 2])
    console.log(res2)
// fn.apply()
// 1.改变this指向
// 2.调用函数，立即执行
// 第一个参数是this指向的对象，第二个参数是数组形式
// call和apply的区别 都是改变this指向，call接收参数列表，apply接收数组


3.bind
// call apply bind 
    const obj = {
      msg: 'hello world'
    }
    
    function fn(x, y) {
      console.log(this)
      return x + y
    }

    const fun = fn.bind(obj,1,2)
// 这里，相当于用fun去接收了fn.bind()改变了this之后的函数
    console.log(fun)

// 然后手动调用执行
    const res = fun()
    console.log(res)

    // fn.bind(obj,参数列表)
    // 1.改变this指向
    // 2.bind有返回值，bind的返回值是一个函数，这个函数里面的this就是我们传入的第一个参数
    // 3，bind不是立即执行的，需要手动调用


    // 总结一下
    // 面试题 call / apply / bind 的区别
    // 1.都是改变this的指向
    // 2.call接受的是参数列表，apply接受的是数组
    // 3。call和apply是立即执行的，bind返回是一个函数，需要手动调用
```

### 剩余参数

```js
    // 剩余参数
    // ...变量名
    // arr是一个真数组，存的是剩下的实参
    // ...arr只能放在形参位置的最后面
	// 当...变量名 用作剩余参数时，只能写在函数的形参位置进行表达
    function getSum(...arr) {
      let cunt = 0
      arr.forEach(el => cunt += el)
      console.log(cunt)
    }
    getSum(1, 2, 3, 5, 6)

    function getSum1(a,b,c,...arr1) {
      console.log(arr1)
    }
    getSum1(1,23,5,2,6,4,7,11)
```

### 扩展运算符

```js
// 扩展运算符：...
let arr = [2,3,4,5]
// console.log(arr)
// console.log(...arr) //2,3,4,5 当...当作扩展运算符，会将数组转化为一列数据的形式
用途1：
Math方法中，接受的参数为一列数据的形式，可以用扩展运算符将数组转化为一列数据的形式
let arr1 = [3, 4, 5, 6, 7, 8, 9]
    console.log(Math.max(...arr1))

用途2：
将数组进行浅拷贝，赋值原数组的数据给一个新数组，使得新数组在改变自身元素的数据时，原数组不会变动
    const a1 = [2, 3]
    const a2 = a1
    a2[0] = 999
    console.log(a1) // [999,3]
    const a3 = [5, 6, 7]
    const a4 = [...a3]
    console.log(a4)
    a4[0] = 888
    console.log(a3)

用途3：
将字符串形式的属性值，转化为单个字符串组成的一列数据，默认单个字符之间存在空格隔开
    const str = 'hello world'
    console.log(...str)
利用扩展运算符的这个特点，实现字符串的反转
 // 1.  str.split(分隔符)
    // 作用：把字符串分隔，得到一个字符串数组
    const str = 'The quick brown fox jumps over the lazy dog.';

    const words = str.split(' ') // 空格
    console.log(words)

    const str1 = '2022-12-23'
    // split 字符串转数组  join ：数组转字符串
    const arr = str1.split('-')
    console.log(arr)
// 2. arr.reverse()
    reverse() 方法将数组中元素的位置颠倒，并返回该数组。数组的第一个元素会变成最后一个，数组的最后一个元素变成第一个。该方法会改变原数组。
   
 // 3. arr.join()
    join() 方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串，用逗号或指定的分隔符字符串分隔。如果数组只有一个元素，那么将返回该元素而不使用分隔符。
    const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(''));
// expected output: "FireAirWater"

console.log(elements.join('-'));
// expected output: "Fire-Air-Water"

（1）    const str = 'hello world'
	先split，将字符串数据转化为字符串组成数组，str.split(''),默认将所有单个字符作为数组的一个数据。再reverse，将数组的数据反转
```

