# jQuery技术内幕
* 1. 不能一行一行的看源码
```
(function(window,undefined){
	// 变量 
	undefined = 42；
	alert(undefined); // 42
})(window);
// 关键字
undefined = 42；
alert(undefined); // undefined
```
- 闭包：也就是沙箱，保护里面的变量，外部拿不到，能减少参数window查找的时间

```
function a(){var b = 1;console.log(b)}
a.age = "13";
a.fn1 = function(){var d = 4;}
a.prototype.fn = function(){var c = 3;}
// age、fn1、arguments、caller、length、name、prototype（fn、constructor（构造函数整体）、__proto__:Object）、__proto__、[[FunctionLocation]]、[[Scopes]]
console.dir(a);
// __proto__(fn、constructor（age、fn1、arguments、caller、length、name、prototype（fn、constructor（构造函数整体）、__proto__:Object）、__proto__、[[FunctionLocation]]、[[Scopes]]）、__proto__:Object)
console.dir(new a);
```

* 2. new

```
// 以下两个变量基本相等（但是原型链不同）
// new的话s、n能够访问jq原型链上所有的方法（.val）
// 不new的话 q也能访问jq原型链上所有的方法
var s = new $('#test').val;
var q = $('#test');
```

```
(function(window,undefined){
	var jQuery = function(selector,context){
		// 相当于new了一个jQuery()，new了自己
		return new jQuery.fn.init(selector,context);
	}
	jQuery,fn = jQuery.prototype = {
		init:function(selector,context){
			
		}
	}
})(window);
```
- 当new一个对象的时候，执行两步：1.构造方法 2. 原型链的方法
- new的时候，第一步 返回一个init的函数，原型链就挂载了一个init的函数，没有主动执行（init没调用，被搁置了）
- 解释：`new jQuery.fn.init(selector,context)`就是new出来了`jQuery.prototype`,言外之意就是`jQuery.fn.init.prototype  = jQuery,fn = jQuery.prototype`,简化之后`jQuery.fn.init = jQuery`
- 为什么要`return new jQuery.fn.init(selector,context);`,而不直接`new jQuery()`呢？
	+ 为了得到jquery原型链上的方法
- $.fn:写插件的，jq所有的方法都在$.fn上，平时用到的方法都是这个上面的

```
//jQuery.fn.extend:是把属性直接挂载到jQuery原型链上
jQuery.fn.extend({
	a:function(){
		console.log(123);
	}
})
$('').a(); //123
//jQuery.extend:是把属性直接挂载到jQuery对象上
jQuery.extend({
	a:123;
})
$.a; //123
```

```
//链式调用
var s = {
	a:function(){
		console.log('first');
		return this;
	},
	b:function(){
		console.log('second');
		return this;
	},
	c:function(){
		console.log('three');
	},
}
s.a().b().c(); // undefind(a、b没有加return this;)

```

```
// on或者live: $('.test').click()不生效
$('body').append('<div class="test"></div>')
$('.test').click()
```
- on:`$('body').on('click','.test'function(){})`，采用事件代理的形式，绑定到body上，就把所有的东西通过e.target()找到(e.target()==test)

```
// $()->函数 函数的重载
$('.test').val("test") // 取值 赋值
$('.test','td')
$(['.test','#id'])
$(function(){})
```
```
function addMethod(obj,name,f){
	// undefind
	var old = obj[name];
	obj[name]=function(){
		if(f.lenght===arguments.length){
			// 如果实参 == 形参 this指obj
			return f.apply(this, arguments);
		}else{
			return old.apply(this, arguments);
		}
	}
}
var people = {
	name:['dxler','dxfer'];
}
var find0 = function(){
	return this.name;
}
var find1 = function(name){
	var arr = this.name;
	for(var i = 0;i<=arr.length;i++){
		if(arr[i] == name){
			return arr[i]+"在第"+i+“位”;
		}
	}
}
var find2 = function(){
	return this.name;
}
addMethod(people,'find',find0);
people.find(); //old：undefinded； obj.find:find0
addMethod(people,'find',find1); // dxfer在第2位
people.find("dxfer"); //old：find0； obj.find:find1
people.find(); //['dxler','dxfer'] 
addMethod(people,'find',find2); //old：find1； obj.find:find2
people.find(“”，“”);
```
```
function test(a){
	console.log("实参个数", arguments.length);
	console.log("形参个数", test.length);
}
test(); //0 1
```

* 短路表达式和多重短路表达式

```
var a;
if(a){
	foo = a;
}else{
	foo = b;
}
// 直接替换成|| &&
var foo = a||b;
"test"&&false = false
"test"&&true = true
"test"||false = test
"test"||true = test
false||"test" = test
```
- 平时这种东西很有用的：

```
var a;
function test(){}
a && test();
```
	
- 多重短路表达式

```
var foo = a && b && c
a && (b && c);
```
- 小技巧1

```
core_version = "1.19.2";
core_string = core_version.trim;
trim:function(data){
	//return String.prototype.trim(data);
	return core_string(data);
}
```
	+ 1. 不用去原型链找trim这个方法
	+ 2. 代码不用写那么长了
	+ 3. 速度超级快
- 小技巧2（钩子机制）:判断数组`Object.prototype.tostring.call([])``$.isArray()`

```
$.each("Boolean Number String Function Array Date RegExp Object Error".split(" "),function(i,name){
	class2type["[object "+name+"]"] = name.toLowerCase();
})
```

```
var data = {
	index1:1,
	index2:2
}
var s = "index1";
// 平时都用if...else去判断
// jq里面是用的钩子
data[s] && function(){}
```
- $.ready

```
var $ = ready = window.ready = function(fn){
	if(document.addEventListener){//兼容非IE
		//注销事件，避免反复出发
		document.removeEventListener("DOMContentLoaded",function(){
			document.removeEventListener("DOMContentLoaded",arguments.callee,false);
			fn();//调用参数函数
		},false);
	}else if(document.attachEvent){//兼容IE
		IEContentLoaded(window,fn);
	}
	function IEContentLoaded(w,fn){
		var d = w.document,done=false,
		// only fire once
		init = function(){
			if(!done){
				done = true;
				fn();
			}
		};
		//polling for no errors
		(function(){
			try{
				// throws errors until after ondocumentready
				d.documentElement.doScroll('left');
			}catch(e){
				// 一定会拿到ready
				setTimeout(arguments.callee,50);
				return;
			}
			// no errors,fire
			init();
		})();
		// trying to always fire before onload
		d.onreadystatechange = function(){
			if(d.readyState == 'complete'){
				d.onreadystatechange = null;
				init();
			}
		};
	}
}
ready(function(){alert(1)})
```

- 设计模式(实现观察者) 请查阅汤姆大叔的博客

```
$({}).on
```
<strong>jquery源码是精华，一定要学习</strong>
