### 你不知道的HTML
* 什么是同源：协议相同、域名相同、端口相同（http://www.ruanyifeng.com/blog/2016/04/same-orgin-policy.html）
* 浏览器不同的域名间不能访问彼此的cookie ，但是内部的表单没有限制
* 限制范围：cookie、localstoryge、indexdb无法读取；dom无法获取；ajax请求不能发送
* 如何设置同源策略（hosts）：domain 是最最实用的策略
```
test.xxx.com a.html
<script>document.domain = 'xxx.com';//设置同源策略document.cookie = "test1=hello";</script>
```
```
test2.xxx.com b.html
<script>document.cookie; //test1=hello</script>
```
* 可以实现跨域：
	- img：
	```
	var s = new Image();
	var p = Date.now();
	s.src = "http://www.baidu.com/s.gif";
	s.onload = function(){
	  var end = Date.now();
	  t = end - p;
	}
	```
	- iframe：
	- link：css攻击漏洞（background）、伪造
	- script（jsonp（jsonp原理））：
		1. 语义化：（http://www.cnblogs.com/freeyiyi1993/p/3615179.html）给爬虫写
		2. 使用div进行布局，不要用div进行无意义的包裹 span行内常见的元素
		3. header、nav、article、aside、section、footer```<header><nav></nav></header><div class="content"><section></setion><aside></aside></div><footer></footer>```
		4. 尽量少写html一定要少写：html第一减少dom渲染的时间 减少整个文件大小。一个html元素最少最少顶三个元素用
