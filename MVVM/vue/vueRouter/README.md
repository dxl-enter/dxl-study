1. 什么是vueRouter
  * 官方 作用：设定访问路径  组件切换  建立组件和url之间的一个映射关系
  * route：路由，单个路由或某一个路由
  * routes：路由集合 数组类型
  * router：路由器  负责管理route和routes
  * vue-router的实现原理
    + 单页面应用spa：单个html文件，通过路由实现跳转，更新视图而不会重新请求页面
    + 多页面应用mpa：多个html文件，通过a链接实现跳转，会有白屏的问题
  * 前端路由
    + hash模式（#）：默认模式，页面不会重新加载

    ```
    if("onhashchange" in window){
     window.onhashchange = () => {
      console.log(this.location.hash)
     }
    }
    ```
   
    + history模式（不会有#）：2014年html5标准发布多了两个api，一个是pushState 一个是replaceState
    + 都对历史记录有修改功能：back，forward，go
  * 
2. 如何使用
 * script方式   不推荐
 * npm install vue-router --save  推荐
 * 兜底路由(必须放在routes的最下面)

  ```
  {
   path:"**",
   redirect: 'home'
  }
  ```
 
  * 监听路由

  ```
  watch:{
   $route(to,from){
    console.log((to.params.name,from.path)
   }
  }
  ```
  
  * 传参
   + params：只能name引入路由，不能path引入（用了path，params参数回自动忽略）
   + query：path、name都可以
   
 
3. 路由的一些知识，开发中必须掌握的一些知识
