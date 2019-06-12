# Express入门必看
## 1.Express介绍
* -- save 保存在package.json里面的是dependencies
* -- save-dev 保存在package.json里面的是devDependencies,开发环境所用到的
* 中间件：next传递
* 每次修改代码都得重新启动，安装一个supervisor，这样就能修改之后自动运行
* 伪静态：localhost:8081/index.html?name=aaa
* 当用户采用?name=a&age=12这种形式的时候，采用req.query.name进行获取，当用户采用/index.html/:id的形式时，需要采用req.params.id进行获取
* 1. 安装并引用express，启用一个express的实例
* 2. app.listen一个端口， 启动一个后台服务
* 3. app.get 设置基础的路由 然后吐出数据
* 4. 平时的请求都是get 浏览器上直接拼接
* 5. get、post、put、delete $.ajax->put
* 
## 2.Express中间件
* stackstaw社区
## 3.Express路由
* 采用get、post设置路由
* controller/action 标配路由
*  req：接收用户的信息；res：返回给用户；next：跳转下一个句柄，如果没有next浏览器会等待
*  为什么要用数组？处理单个路由请求比较复杂 `app.get('/',[a1,a2,a3])` 先把活干完，最后输出send/end/json
*  use：毕竟路由：获取登录状态
*  router：迷你的app
## 4.Express错误处理
* nodejs是单线程，如果错误处理不好的话，整个站就会挂掉
* 错误处理能友好的提示，跳到一个很漂亮的页面（一句简单的话/一个json字符串），让用户得到很好的反馈
* `res.status(500).send('错误提示')`
* 放在最下面，用来兜底
* 日志服务器：方便工程师进行排查 log4j.js
## 5.Express模板引擎
* 安装 `npm install jade --save`不是推荐使用，推荐使用``
* 前端没有能力去直接操作服务器，只能通过接口进行传递
* 
