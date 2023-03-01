### computed和watch进行比较

#### watch

**注意:**watch函数(所有vue所管理的函数)不能用箭头函数的形式，理由是箭头函数绑定了父级作用域的上下文，所以 `this` 将不会按照期望指向 Vue 实例，而是指向window

```js
const obj = {
    name:'扇宝',
    age:18,
    hobby:{
    like1:'捡瓶子',
    like2:'毛东西'    
}
}

export default {
    data(){
        return{
            
        }
    },
    watch:{
        obj:{
         	// 浅浅监视obj对象的变化，当检测到obj发生变化（浅），handler函数就会被执行
            handler(){
                console.log('扇宝被人打了')
            }，
            immediate:true //默认为false，当true，进入页面就执行一次handler函数,
            deep:true // 深深监视
        }
    },
    //简写形式
    vm.$watch('obj',{
    //配置项
})
// 1.computed能做的操作，watch都能做。
// 2.watch做的操作，computed不一定能做，如异步操作，定时器，等待几秒才让数据发生变化，computed中监听数据是及时响应的，不能做到异步操作。
// 3.vue所管理的函数，不能用箭头函数的形式来写，因为箭头函数绑定的作用域是父级作用域上下文的，this指向不是vue实例。
// 4.所有不被vue所管理的函数，如定时器的回调函数，ajax的回调函数，最好写成箭头函数，这样this在只想的时候会指向所在函数的上层作用域，才会指向vm或实例对象


}
```



