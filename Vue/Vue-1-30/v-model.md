### v-model

**定义**：v-model是一个语法糖，作用是将data中的数据和表单元素做双向绑定

**原理**：v-model仅限表单元素，vue底层会让v-model实现不同的属性绑定和事件监听



```js
v-model实现的是双向绑定，数据驱动视图，视图也可以驱动数据
如果要模拟v-model的效果，通过 v-bind:变量名（对应不同标签类型，有固定的变量名，如input框的是value）=变量 实现数据驱动视图，通过监听事件 @事件名(不同的事件名对应的名字如input框有input，change)=fn 实现视图驱动数据
//1.当input的type=text时
//1.1 v-model
<input type="text" v-model="msg"> ===> <input type="text" :value="msg" @input="handle">

//1.2 v-model.lazy 监听事件@change
 <input type="text" v-model.lazy="msg"> ===> <input type="text" :value="msg" @change="handle">
    
//2.当input的type=checkbox时
  <input type="checkbox" v-model="flag">等价于  
 <input type="checkbox" :checked="flag" @change="handleInput">
    
 <!-- 模板中使用事件对象 如果监听的是dom元素事件 $event => 事件对象-->
<!-- <input type="text" :value="msg2" @input="msg2 = $event.target.value"> -->
```



### this.$nextTick

```js
// Vue是异步更新DOM元素的， ==> Vue不会在数据修改后，立刻更新页面上的dom元素

// 如果修改了数据，我就更新一次dom元素 ===> 性能消耗很大
// 假设每次+1，都更新一次dom，dom元素要修改五次 ==> 内部，每执行一次count++就会对比新旧虚拟dom

// 所以，不能数据一变化就更新DOM元素（渲染页面内容） ==> 实际情况是先攒着~~，最后一次性的批量更新
$nextTick则是在dom元素更新后立即执行内部的函数
```



