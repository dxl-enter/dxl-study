# 大规模nodejs项目架构与优化
* nodejs的BFF（后端为前端）
* 最初vue、jq - index.html - java服务（跨域：nginx）
* 以上不好的地方
	- 返回的json会很大，想削减一些，后端不管
	- 接口格式不对，后端不管
	- 要输出的首页直出（真路由变成假路由[]）时间（性能），后端不管
	- 真正做到前后端分离
* node做ssr同构 ssr+vue ： nodejs直接渲染vue

### z这节课我们要讨论什么
* nodejs异步io原理浅析及优化方案
	- 异步io的好处
		+ io是昂贵的，分布式io是更昂贵的（必考）
		+ nodejs适用于io密集型不适用cpu密集型（必考）
	- node对异步io的实现
		+ nodejs一口气吃崩，nodejs给多少吃多少，需要监控 - 不能给他那么多，io平衡取决于node代码的健壮性
		+ libuv：是node事件队列的大管家，告诉nodejs的io
* 代码执行顺序
	- promise写的时候同步，then异步的
	- process.nextTick同步任务执行完毕后执行
	- setTimeout 观察者观察 如果是0（有个间隔值）优先返回于setImmediate - 没有进入循环，就在那儿呆着，是被看着的（nodejs官网上）
* 内存管理与优化
	- v8垃圾回收机制
		+ node使用javascript在服务器操作大内存对象受到了一定的限制（堆区），64位系统下约为1.4G，32位操作系统下是0.7G，栈区新声代（分代式）是32M，32位是16M
		```
		node ---max-new-space-size app.js
		-max-old-space-size app.js
		```
		+ process.memoryUsage->rss、heapt
		+ v8的垃圾回收策略主要基于分代式垃圾回收机制。在自动垃圾回收的演变过程中，人们发现没有一种垃圾回收算法能够胜任所有场景。v8中内存分为新声代和老生代两代。新声代为存活时间较短对象，老生代中为存活时间较长的对象
		+ 一句话表示：小孩子尽管玩，到处丢东西大人受
		+ scavenge新声代算法 to的空间超过25%时继承到老生代
		+ 老生代（先采用mark-sweep进行清楚，内存就会不连续。然后采用mark-compact把用的东西移动到右面，左边就是不用的，直接清楚。如果两个都不够用直接奔溃）定期回收（实时回收weakmap）
	- 经典的mvc框架
		backbode：view 可以渲染controller和model
* 预备上线的
	- 预备上线
		+ 前端工程师的搭载动态文件的map分析压缩打包合并至cdn
		+ 单侧、压测性能分析工具发现bug
		+ 编写nginx-
	- 负载均衡：有两层：网络层nginx 本机的负载pm2
	- nginx：nagios检测内存和cpu使用情况，会收到短信
	- pm2:nodejs服务器
	- varnish、stuqid（http缓存） - java 中间架起keepalived（保持连线）heartbeat心跳检测是否还活着

### 作业

	
