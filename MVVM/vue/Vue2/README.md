## 组件通信
1. 父组件向子组件传值
  * props v-bind 推荐
  * $patent 在子组件中直接使用，严格意义上：不是值的传递  不推荐
2. 子组件向父组件传值
  * $emit 事件传值  -->  父级/父组件  v-on   推荐
  * $children 在父组件中直接使用，返回的是数组    不推荐
3. 兄弟组件
  * bus中央事件总线：使用一个非空的vue实例，将bus挂载到vue根实例的原型上，注册的bus要即使销毁（this.$bus.off('事件名')）。使用$on $emit
  
  ```
  1. 
  Vue.prototype.$bus = new Vue();
  2. 
  const bus = new Vue();
  new Vue({
   el:'#app',
   data:{
    data:{ bus }
   }
  })
  ```
  
  * 
4. 

