### Vue监测数据的原理

```js
 let data = {
      name:'扇宝',
      age:18
    }
    const obs = new Observe(data)
let vm =  {}
vm._data = data = obs
    function Observe(obj){
      // 第一步，将传入的对象的属性名遍历成一个数组
      const keys = Object.keys(obj) // ['name','age']
      // 第二步，遍历操作data对象的每一个属性
        keys.forEach(el=>{
          Object.defineProperty(this,el,{
            get(){
              return obj[el]
            },
            set(val){
              return obj[el] = val
            }
          })
        })
    }
```

1.Vue会监视data中所有层次的数据。

2.如何监测对象中的数据？

对象中后追加的属性，Vue默认不做响应式处理。

如果要实现新增属性响应式，请使用Vue.set(对象，属性名，值)或this.$set()

3.如何监测并修改数组中的数据？

使用Vue认可的会更改数组的方法,pop,push,shift,unshift,splice,sort,reverse

使用Vue.set()或者vm.$set将原数组替换为新数组