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
  3. 将bus抽离出来，组件有需要时引用，推荐
  const bus = new Vue();
  export default bus
  ```
  
  * vuex状态管理  state 状态管理  推荐
  * 不是方法的方法  通过父组件进行过滤   不推荐
  
   ```
   使用：
    子组件A通过事件$emit传值给父组件
    父组件通过属性props传值给子组件B
   ```
4. 深层次嵌套（不确定嵌套多深）
  * 依赖注入   provide/inject  不推荐直接用于应用程序代码中，主要是为了高阶组件/组件库提供用例
  * 2.4中新增的属性：$attrs/inheritAttrs(没有申明任何props)

## 组件通深入
1. slot
 * 普通插槽
 * 具名插槽：v-slot 配合 name 使用

```
// v-slot 需要绑定在template模板上，如果使用在html标签上会报错 v-slot can only be used on componebts or <template>
<slot name="header"></slot>
// 使用
<template v-slot:header><p>dfhhhfhgfhgfhgfh</p></template>
```

 * 作用域插槽：让插槽内容可以访问到子组件中才有的数据

```
<slot name="header" :lastName="lastName">{{firstName}}</slot>
// 使用
<template v-slot:header="slotProps"><p>{{slotProps.lastName}}</p></template>
```
2. 动态组件
 * component is属性
 * 组件缓存 keep-alive
3. 指令
 * 内嵌指令
 * 自定义指令：
   需求：页面中有个输入框，页面加载获得焦点事件，autofocus存在兼容性问题
   实现：
      自定义指令
 
 ```
 Vue.directive('focus',{
  inserted:function(el){
   el.focus();
  }
 })
 
 <input v-focus type="text" placehoder="请输入内容" />
 ```
 
 * 自定义指令钩子函数
   bind: 只会调用一次，初始化
   inserted：绑定元素插入父节点时调用
   updated：节点更新时
   componentUpdated：组件节点更新时
   unbind：只调用一次，指令与元素解绑时触发
 * 
4. 

