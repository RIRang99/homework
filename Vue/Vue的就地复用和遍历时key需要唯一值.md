### Vue的就地复用和遍历时:key需要唯一值

```js
// 假设现在渲染一个数组

cosnt list = [
    {id:1,name:老张,age:18},
    {id:2,name:老王,age:19},
    {id:3,name:老六,age:20},
             ]

<li v-for='(item, index)in list' :key='index'>{{list.name}} <input type:'text'> </li>

1.一开始，当vue操纵数据进行渲染，一开始先会在自己内部生成数据的虚拟dom，然后将虚拟dom生成真实dom
2.此时每个生成的虚拟dom上，存在着key的唯一标识。

老的虚拟dom：
老张+ipt k0
老王+ipt k1
老六+ipt k2

3.生成的真实dom上，如果节点是可以页面输入内容的类型如input框，文本域等，在页面向节点写入的内容，不算在虚拟dom里面，虚拟dom只会保留一开始v-for时需要进行循环生成的模板，并添加key值。

当我用数组的下标作为key值，会发生什么？
比如点击按钮，使list数组在开头新添加一条数据
[	{id:0,name:老李,age:555}
    {id:1,name:老张,age:18},
    {id:2,name:老王,age:19},
    {id:3,name:老六,age:20},
             ]
 vue开始重新渲染
 1.生成虚拟dom，并且key值为数组下标
 老李+ipt k0
 老张+ipt k1
 老王+ipt k2
 老六+ipt k3
 
 2.将新的虚拟dom与老的虚拟dom比较
 此时老李+ipt k0 找老dom里面有没有k0
 有，老张+ipt k0 ，但是老张这两个字和老李不一样
 所以老李这两个字得由虚拟dom生成真实dom
 再看ipt相同,ok，老虚拟dom生成的真实dom直接征用给新一代，并且把原来ipt上可能有用户输入的文本内容一起征用了
再对应往下找 老张+ipt k1 找老dom有没有k1
有,老王+ipt k1 ，ok字不一样ipt一样，字靠新虚拟dom生成真实dom，ipt征用原来的真实dom
最后老六k3比较难顶，老虚拟dom没有k3，所有东西都得靠新虚拟dom生成
影响:结构不对应，内容错位崩了，虚拟dom生成真实dom耗费的性能远超征用老的真实dom


如果用id作为key值
老的虚拟dom：
老张+ipt k1
老王+ipt k2
老六+ipt k3

新的虚拟dom
 老李+ipt k0
 老张+ipt k1
 老王+ipt k2
 老六+ipt k3
 
 开始对比
 老李k0，找谁？
 没有k0，ok，老李k0全部靠新虚拟dom生成真实dom
 老张k1 ,对比老dom，老张k1，good一模一样，完全复用老真实dom
同理到老六也一样
整个流程只有老李需要靠新虚拟dom生成真实dom，节省性能，还不错位

总结：用index作为key会引发的问题
1.如果对数据进行了破坏顺序，如数组排序的操作，会产生没有必要的真实dom更新，降低效率。
2.如果结构中还包含input等用户输入内容的dom，会导致产生错位的dom更新，界面出现问题
```

