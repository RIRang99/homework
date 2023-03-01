### Object.defineProperty

```js
// Object.defineProperty方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。
	
let person = {
    name:'扇宝',
    gender:'female'
}
let num = 18

//这个方法接收三个参数，分别是(修改的对象，需要修改的属性名，配置项=>对象形式)
Object.defineProperty(person,'age',{
    value:18, //修改属性的属性值
    enumerable:true, //使该属性可枚举，默认为false
    writable:true, //使该属性可修改,默认为false
    configurable:true, // 使该属性可删除，并可以更改除了value和writable以外的配置，默认为false
    
    get(){
          // getter的作用是当有人读取该属性的值时，返还属性值num是多少
          console.log('age属性被读取了')
          return num
        },

    set(value){
          // setter的作用是当通过person.age = value修改age这个属性的值时，通过返还将num属性值等于修改值value，实现num值的修改
          console.log('age属性被改写了')
          return num = value
        }
})

	  console.log(person.age) // 18 可赋值
      person.age = 19
      console.log(person.age) // 19 可更改值

      for(let k in person){
        console.log(k)
      }// 可遍历

      delete person.age
      console.log(person)  //可删除
```

