# KOA1入门必看
## 1.KOA简介
* Koa 是一个新的 web 框架，由 Express 幕后的原班人马打造， 致力于成为 web 应用和 API 开发领域中的一个更小、更富有表现力、更健壮的基石。 通过利用 async 函数，Koa 帮你丢弃回调函数，并有力地增强错误处理。 Koa 并没有捆绑任何中间件， 而是提供了一套优雅的方法，帮助您快速而愉快地编写服务端应用程序。
## 2.KOA应用
* 根据代码复制，直接修改浏览器response header里面的content-type的属性
* 可以监听多个端口：当我们在部署大型集群的时候，如果fork一些线程，如果想让nodejs支持多线程，我们fork的时候每个端口都要不一样
* app.use(function):为应用添加指定的中间件（middleware）
## 3.Context(上下文)
* Context = this
## 4.请求（request）
* Koa Request 对象是在 node 的 vanilla 请求对象之上的抽象，提供了诸多对 HTTP 服务器开发有用的功能。
* yield：异步变得同步
## 5.输出（response）
* Koa Response 对象是在 node 的 vanilla 响应对象之上的抽象，提供了诸多对 HTTP 服务器开发有用的功能。
* lastModified：很有用，可以在客户端进行强制缓存
