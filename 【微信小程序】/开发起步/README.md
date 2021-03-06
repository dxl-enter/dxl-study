### 小程序简介
1. 小程序特点
* 体验好
* 一次开发，多端共享（开发成本低）
* 离线缓存（10M）
* 接口更多（相比订阅号及服务号）
2. 小程序与app的区别
* 下载安装
* 内存占用
* 手机匹配
* 产品发布
* 功能区别
* 应用场景
3. 小程序与H5的区别
* 规范不一样：w3c环境、腾讯
* 运行环境不一样
* 开发方式不一样
* 获取权限不一样
4. 小程序与native app、webapp以及hybrid app的区别

![图片](https://github.com/dxl-enter/dxl-study/blob/master/%E3%80%90%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E3%80%91/%E5%BC%80%E5%8F%91%E8%B5%B7%E6%AD%A5/Dingtalk_20210106103611.jpg?raw=true)

5. 小程序与普通网页开发的区别
* 开发语言
* 多线程：网页开发渲染线程和脚本线程是互斥的，这也导致长期脚本运行导致页面渲染卡顿；在小程序中渲染线程和脚本线程是分开的线程。
* DOM、Bom操作：网页开发是可以操作的；小程序的逻辑层和渲染层是分开的，没有DOM api和Bom api，像前端一些jquery和zpto是不能运行的
* 运行环境：小程序的开发环境

![图片](https://github.com/dxl-enter/dxl-study/blob/master/%E3%80%90%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E3%80%91/%E5%BC%80%E5%8F%91%E8%B5%B7%E6%AD%A5/Dingtalk_20210106105519.jpg?raw=true)

* 开发
### 开发入门
1. 账号注册

![图片](https://github.com/dxl-enter/dxl-study/blob/master/%E3%80%90%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E3%80%91/%E5%BC%80%E5%8F%91%E8%B5%B7%E6%AD%A5/Dingtalk_20210106110155.jpg?raw=true)

2. 申请域名和证书
* 开发环境中

```
{
  "setting" {
    "urlCheck": false
  }
}
```

* 生产环境中：需要备案的域名并且安装ssl证书
* 云开发： 都不需要
3. 小程序的项目结构

```
app.json: 全局页面样式
project.config.json: 微信开发者工具配置
pages：页面
sitemap.json: 当开发者允许微信索引时，微信会通过爬虫的形式，为小程序的页面内容建立索引。当用户的搜索词条触发该索引时，小程序的页面将可能展示在搜索结果中。 
wxss：750rpx为100%的屏幕宽度；仅支持部分的选择器（.class、#id、element、element,element、::after、::before）；class和hover-class的文件是需要有先后顺序的。
```

4. 数据更新与事件机制
* 在小程序中并没有提供类似操作DOM的api来直接更新视图，所以我们需要使用setData（不仅会对本页面的data对象进行改变，还可以动态向data对象添加变量）方式来更新数据，让框架自动更新视图。如果使用this.data.currentIndex = 1;赋值的话，业务逻辑层数据会更新，但是视图层不会更新。
* 小程序中的数据并不是双向绑定的，而是单向绑定：视图层的数据改变不会影响逻辑层的数据改变
* 事件机制：冒泡事件（bind）、非冒泡事件（catch）
* 视图层到逻辑层的数据传递方式event事件对象，target是触发的目标元素；而surrentTarget是冒泡事件回触发父级的点击事件，里面的dataset会获取到页面设置的自定义元素(wxml - data-movie-id="{{movie.id}}" ---> js - event.surrentTarget.dataset.movieId)；changeTouches会获取到手指触摸屏幕的坐标

5. 实现电影推荐页路由带参跳转
* 

