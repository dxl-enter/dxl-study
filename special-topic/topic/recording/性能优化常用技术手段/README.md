# 性能优化常用技术手段
## 雅虎军规
1. 34条雅虎军规（必须要践行）
2. 能用自动化工具解决的问题，坚决不用人工
3. 留3-5个js（尽量不要放在同一个域名下，要放在cdn下面）和css，雪碧图
4. dns预解析提升页面速度(再打开其他页面时百度分享按钮的加载明显提高)
	```
	<meta http-equiv="x-dns-prefetch-control" content="on"></meta>
	<link rel="dns-prefetch" href="http://bdimg.share.baidu.com"/>
	```
5. 推迟加载内容
6. 预加载
7. 减少DOM元素数量
8. 根据域名划分页面内容
9. 使iframe的数量最小
	* 尽量少用iframe，因为即使内容为空，加载也需要时间；会阻止页面的加载；没有语义
10. 不要出现404错误
11. 使用内容分发网络
	* 使用cdn，静态资源文件服务器
12. 为文件头指定Expires或Cache-Control
13. Gzip压缩文件内容
14. 配置ETag
15. 尽早刷新输出缓冲
	* 模版引擎
16. 使用GET来完成AJAX请求
	* get-2k
17. 把样式表置于顶部
	* 加快页面的下载速度
18. 避免使用CSS表达式（Expression）
19. 使用外部JavaScript和CSS
20. 削减JavaScript和CSS
21. 用<link>代替@import
	* 加载会形成串行
22. 避免使用滤镜
	* 滤镜对渲染性能要求很高
23. 把脚本置于页面底部
24. 剔除重复脚本
	* 版本号控制（md5）
25. 减少DOM访问
26. 开发智能事件处理程序
	* 开启智能事件处理：使用代理，domready代替onload
27. 减小Cookie体积
28. 对于页面内容使用无coockie域名
29. 优化图像
30. 优化CSS Spirite
31. 不要在HTML中缩放图像
32. favicon.ico要小而且可缓存
33. 保持单个内容小于25K
	* js或者css合并体积小于25
34. 打包组件成复合文本
	* css和js合并一个文件以减少http请求（.jscss）很少用
https://blog.csdn.net/camel20/article/details/7283893

## 面向切面的概念解读
1. Aspect Oriented Programming（AOP），面向切面编程，是一个比较热门的话题。AOP主要实现的目的是针对业务处理过程中的<strong>切面进行提取</strong>，它所面对的是处理过程中的某个步骤或阶段，以获得逻辑过程中各部分之间低耦合性的隔离效果(在人家的业务代码中穿插了一些代码，)（用刀切面包，不要乱切，只要在开头或者结尾切，面包还保存完整的形状）

## 面向切面代码实战
```
function test(){
	var start = new Date();
	alert(2);
	var end = new Date();
	console.log(end-start)
}
// 你要统计一下当前的所有函数中谁耗时最长
```
* 每个函数中都需要插入start和end这样的代码，显然比较无耻，搞不好会出现变量污染

```
function test(){
	alert(2)
	return "me test"
}
// 切入的方法
Function.prototype.before = function(fn){
	var __self = this;
	fn()
	return __self.apply(this,arguments)
}
Function.prototype.after = function(){
	//after 先执行本身this 再执行回调
	var __self = this;
	__self.apply(this,arguments);
	fn()
}
test.before(function(){
	alert(1)
})
test.after(function(){
	alert(3)
})
```
*  默认函数test被执行了两遍
*  test作为中转
*  before回调和before一起送到after去
*  after和test一起送到before去

```
Function.prototype.before = function(fn){
	var __self = this;
	return function(){
		// this指向了调用的函数
		fn.apply(this,arguments)
		return __self.apply(__self,arguments)
	}
}
Function.prototype.after = function(){
	//after 先执行本身this 再执行回调
	var __self = this;
	return function(){
		// this指向了调用的函数
		var result = __self.apply(__self,arguments)
		if(result==false){
			return false;
		}
		fn.apply(this,arguments)
		return result;
	}
}
test.before(function(){
	alert(1)
}).after(function(){
	alert(3)
})()
```
## Nginx服务器缓存策略
