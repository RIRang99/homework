### 前期准备: 类

#### class的用法

```js
// 类:用于创建对象的目标，描述了一类对象的行为和特征。
// 和构造函数类似，首字母大写

class Father {
    //类的默认方法constructor()，===>构造函数
    constructor(name,age){
        this.name = name
        this.age = age
    }
    // 类创建的构造函数添加公共方法，在构造函数内部直接写就可以，传参也一样
    // 与构造函数添加公用方法不同，构造函数添加公用方法需要写在构造函数的原型对象上
    // function Father(uname, age) {
    //   this.uname = uname
    //   this.age = age
    //   // function sing(song) {
    //   //   console.log(song)
    //   // } ===> 无效
    // }
    // Father.prototype.sing = (song)=>{
    //   console.log(song)
    // } ===>需要在原型对象上添加
    // const son = new Father()
    // son.sing('love')


      sing(song) {
        console.log(song)
      }
     // 多个方法之间不用空格隔开
      dance(dac) {
        console.log(dac)
      }
}

// 通过创建实例对象来使用类，用new关键字调用
const me = new Father('RIRang',18)
console.log(me) // ==> Father{
	name:'RIRang',
	age:18
}
me.sing('love') // ===> console.log('love')
```

#### 类的注意事项

```js
  // 1.  ES6中  类 没有变量提升，所以必须先声明类，再通过类实例化对象。
    // const ldh = new Star('刘德华', 18)
    class Star {
      constructor(name, age) {
        this.name = name
        this.age = age
   // console.log(this)
     // sing()
        this.sing()
      }
    // 2. 公共的属性和方法，在类里面使用的时候，前面一定要记得加this
      sing() {
        console.log('唱冷冷的冰雨')
        console.log(this.name)
      }
      dance() {
        console.log('跳舞')
      }
    }

    // 1. 类的本质是一个函数，我们可以简单的认为，类就是构造函数的另一种写法。
    // 2. 类有原型
    console.log(Star.prototype)
    // 3. 通过类创建的实例，有__proto__属性，可以访问到原型
    const ldh = new Star()
    console.log(ldh.__proto__)
```

#### 类的继承

```js
extends继承，ES6新增语法 ===>寄生式组合继承
继承:让子类拥有父类的属性和方法
 class Father {
     constructor(name,age) {
     this.name = name
     this.age = age 
     }
    dance(dac) {
        console.log(dac)
    }
 }

// 子类继承父类
class Son extends Father {
    // 子类里面没有写属性和方法，但是 通过extends，直接继承了父类的name和age
    // 子类 创建的实例，可以调用父类的方法 （继承父类的属性和方法）
    // 子类继承父类时默认需要写constructor和super，如果没写，会默认新增一个
}
const shanbao = new Son('扇宝',18)
console.log(shanbao) // ==> Son {
//name = '扇宝'
//age = 18
//}
shanbao.dance('舞') // ==>console.log('舞')
```

#### super关键字

```js
// super() super关键字可以理解为父类的构造函数，写在子类的constructor内，
// 且要写在this之前，不然无法识别。
// super()的括号内可以写形参，形参会传递到父类中调用父类的方法，实现子类继承父类的方法。
    class Son extends Father {
    }

    // 等同于
    class Son extends Father {
      constructor() {
        super()
      }
    }
```

