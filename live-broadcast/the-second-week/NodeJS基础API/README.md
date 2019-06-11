# nodejs
### 01.走进nodejs
* 1. 什么事nodejs
	- nodejs的本质是一个javascript的解释器（js在运行过程中的环境 - 也就是js需要依赖nodejs来运行）
	- nodejs是js的运行环境
	- nodejs是一个服务器程序
	- nodejs本身使用的是v8引擎
	- node不是web服务器
	- 脚本语言就需要解释器，nodejs就是这种解释器；对于html中的js，浏览器就充当了解释器（js操作dom）；如果我们想独立的运行js，我们就必须依赖nodejs（js操作磁盘文件、搭建http服务器）
* 2. 为什么要用nodejs
	- 为了提供高性能的web服务（就要求io性能非常强大）
	- io性能（发送和接受数据所依赖的条件就是io端口）强大
	- 事件处理机制完善（on什么的函数背后的机制就是事件处理）
	- 天然能够处理dom
	- 社区非常活跃，生态圈日益完善（开发资源非常丰富）
* 3. nodejs的优势在哪里
	- 处理大流量数据（用户访问量大，流量就大。符合io性能强大这个特点）
	- 适合实时交互的应用（在线聊天系统）
	- 完美支持对象数据库（有区别于sql型数据库，sql型数据库一般是mysql，而对象数据库一般用mogodb数据库，它可以直接调用数据库提供的接口，使用对象数据库进行缓存能使nodejs环境速度更加快捷）
	- 异步处理大量并发连接（并发连接指一台服务器同时有很多的用户能够访问，是判断服务器性能的指标之一）
* 4. 学习nodejs的前置知识
	- javascript
	- es6（js的一种语言标准，更接近面向对象语言）
	- 一些服务器相关的知识（apache、http服务交互过程）
	- 最好在linux系统下进行开发
* 5. 相关资料和学习资料
	- 官方网站 - nodejs.org
	- 中文社区 - nodejs.cn
	- 手册
	- 开源代码 - github
### 02.nodejs入门
* 1. 安装nodejs
	- 官方网站
	- 安装nodejs
	- 检查环境
* 2. 包管理器npm
	- 允许用户从npm服务器下载别人编写的三方包到本地
	- 允许用户从npm服务器下载并安装别人编写的命令行程序到本地使用
	- 允许用户将自己编写的包或命令行程序上传到npm服务器供别人使用。
* 3. hello world
* 4. 写一个最简单的web服务器应用
### 03.nodejs环境及npm命令深入
* nodejs REPL环境
	- 输入node进入的环境，类似于window或linux终端
	- nodejs REPL环境
		+ ctrl+c - 退出当前终端
		+ ctrl+c 按两下 - 退出node REPL
		+ ctrl+d - 退出node REPL
		+ 向上/向下键 - 查看输入的历史命令
		+ .tab - 列出当前命令
		+ .help - 列出使用命令
		+ .break - 退出多行表达式
		+ .clear - 退出多行表达式
		+ .save filename - 保存当前的node REPL会话到指定文件
		+ .load filename - 载入当前node REPL会话的文件内容
* 包管理器npm详解
	- 本地安装和全局安装
		+ npm命令更新：npm install npm -g
		+ npm卸载包：npm uninstall ...
		+ 查找包：npm search ...
		+ 帮助：npm help
		+ 详细解释：npm help install
	- npm的使用方法
	- npm常用命令
### 04.nodejs回调机制
* 什么是回调
	- 函数调用方式分为三类：同步调用、回调（回调函数）和异步(消息、事件)调用
	- 回调是一种双向调用模式（被调用函数在执行的时候会调用调用函数）
	- 可以通过回调函数来实现回调
* 阻塞与非阻塞
	- 阻塞和非阻塞关注的是程序在等待调用结果（消息、返回值）时的状态
	- 阻塞就是做不完不准回来

	```
	// 阻塞代码（一步一步走）
	var fs = require('fs');
	// Sync:同步读取
	var data = fs.readFileSync('data.txt');
	console.log(data); //输出16进制的码
	console.log(data.toString()); //输出字符串
	```
	- 非阻塞就是你先做，我先看看有其他事没有，完了告诉我一声

	```
	// 非阻塞代码（控制先后顺序）
	var fs = require('fs');
	// 匿名函数起到的作用就是回调函数
	fs.readFile('data.txt', function(err, data){
		if(err){
			return console.error(err)
		}
		console.log(data.toString());
		
	});
	console.log("程序执行完毕");
	// 先输出“程序执行完毕”，然后输出文件内容
	```
### 05.Node.js事件驱动机制
* 事件驱动模型
	- nodejs单进程，它并不能完全并发很多的事情，而是只能通过事件或者回调来实现这种并发的效果，nodejs没有多线程那么多的额外工作，所以它的性能比较高。
	- nodejs中的每个api都是异步执行的，而且它都是作为独立的线程在运行，而使用异步函数调用我们就可以使用这种机制实现并发处理，nodejs几乎所有的事件机制都是依据观察者模式来实现的
	- 非阻塞io、事件驱动io模型（图）
* 事件与事件绑定
	- 1. 引入events模块，创建eventEmitter对象（事件对象）
	- 2. 绑定事件处理程序（对象和具体的函数绑定）
	- 3. 触发事件

	```
	// 1. 引入events模块，创建eventEmitter对象
	var events = require('events');
	var eventEmitter = new events.EventEmitter();
	// 2. 绑定事件处理程序
	var connectHandler = function connected(){
		console.log('connected 被调用');
	}
	// 完成事件绑定
	eventEmitter.on('connection', connectHandler());
	// 3. 触发事件
	eventEmitter.emit('connection');
	console.log("程序执行完毕！")
	```
### 06.Node.js模块化
* 模块化的概念与意义
	- 为了让nodejs的文件可以相互调用，nodejs提供了一个简单的模块系统
	- 模块是nodejs引用程序的基本组成部分
	- 文件和模块是一一对应的。一个nodejs文件就是一个模块
	- 这个文件可能是javascript代码，json或者编译过的c/c++扩展
	- nodejs中存在4类模块（原生模块和3种文件模块：第三方提供）
* nodejs中的模块
	- 原生模块和第三方模块在两个不同的内存缓存区里
* nodejs的模块加载流程
	- nodejs的模块加载方式
		+ 从文件模块缓存中加载
		+ 从原声模块加载
		+ 从文件加载
	- require方法加载模块
		+ require方法接受以下参数的传递：
		+ http、fspath等，原生模块
		+ ./mod或../mod，绝对路径的文件模块
		+ /pathtomodule/mod，绝对路径的文件模块
		+ mod，非原生模块的文件模块
* 模块化代码案例

	```
	// 模块文件 - hello.js
	// 1. 模块主要逻辑
	function Hello(){
		var name;
		this.setName = function(argName){
			name = a gName;
		}
		this.sayhello = function(){
			console.log("Hello " + name);
		}
	}
	// 2. 对模块进行导出
	module.exports = Hello;
	// 调用模块文件 - mian.js
	// 调用Hello模块(在引用自己写的模块的时候要加路径)
	var Hello = require('./hello');
	
	hello = new Hello();
	hello.setName('dxler');
	hello.sayhello();
	```
### 07.Node.js函数
* 函数概念
	 - 在javascript中，一个函数可以作为另一个函数的参数
	 - 我们可以先定义一个函数，然后传递，也可以在传递参数的地方直接定义函数
	 - nodejs中函数的使用与javascript类似

	 ```
	 function say(word){
	 	console.log(word);
	 }
	 function execute(someFunction,value){
	 	someFunction(value);
	 }
	 execute(say,"Hello");
	 ```
* 匿名函数
	- 我们可以把一个函数作为变量传递
	- 不一定“先定义，再传递”，可以直接在另一个函数的括号中定义和传递这个函数
	```
	function execute(someFunction,value){
		someFunction(value);
	}
	execute(function(word){console.log(word)},"Hello");
	```
* http服务器端的函数传递
### 08.Node.js路由
* 路由 /controller/action  一个controller对应多个action
### 09.全局方法和工具
* underscore.js 库文件
### 10.文件系统 
* 
