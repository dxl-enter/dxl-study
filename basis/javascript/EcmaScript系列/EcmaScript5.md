# ES5核心技术
```
(funcction(){
	alert(a); // undefined
	let a = 3;
}
)();
alert(a); // a is not defined
```
- 解析：闭包：匿名函数（把变量集中在这样的空间内，外部访问不到,内部的东西不被外部污染）自执行、表达式

```
this.a = 20;
var test = {
	a:40,
	init:()=>{
		console.log(this.a);
		function go(){
			this.a = 60;
			console.log(this.a);
		}
		go.prototype.a = 50;
		return go；
	}
};
var p = test.init();
p();
new(test.init())();
```
- 答案：
- 解析：js谁调用this指谁<br/>
箭头函数： <br/>
- 小知识

```
this.a = 20;
var test = {
	a:40,
	init:function(){
		function go(){
			console.log(this.a);
		}
		return go；
	}
};
var p = test.init();
p(); //20
```
- 解析：`var p = test.init();`是将`function go(){
			console.log(this.a);
		}`函数赋值给了p，p是全局的变量名，执行`p()`时this指向window
		
```
this.a = 20;
var test = {
	a:40,
	init:function(){
		function go(){
			console.log(this.a);
		}
		go()；
	}
};
test.init(); //20
```
- 解析：只是调用了test里面的函数，在执行`go()`执行时操作的this，函数并没有操作
	
```
function f1() {
	var n =0;
	function f2(){
		n+=1;
		console.log(n);
	}
	return f2();
};
var resule = f1();
resule();
resule();
resule();
```
- 解析：函数f2时操作变量的，n会永驻到内存空间中，当函数声明的变量，在执行的时候，var会被内存回收机制收回。`return f2();`执行一次后它不知道下一次什么时候执行，所以永远不能释放n。这又执行完之后释放n`resule = null`。
- 私有变量：在变量前加__
- 闭包：函数体内部的变量，外部不能访问，起到变量保护的机制，<strong>但是需要在调用完之后把它置成null</strong>

```
// 父类
var Car = function(color){
	this.color = color;
	this.sail = function(){
		console.log(this.color+"卖13万");
	}
}
Car.prototype.sail = function(){
	console.log(this.color+"卖13万");
}
var s = new Car();
console.log(s.sail());
console.log(s); //{color:red,__proto__}:this.color指向s变量
// 子类
var BWM = function(){
	Car.call(this,color);
}
// 子类继承父类(浅拷贝)
/*BWM.prototype = Car.prototype; // 子类把父类覆盖了
BWM.prototype.test=function(){}
var s = new Car();
console.log(s.sail());*/
// js实现面向对象的过程
// 1. 拿到父类的原型链上的方法
// 2. 不能让构造函数执行2次：如果BWM.prototype=new Car()：new的话父类的函数执行了2次 && 子类的原型链上的constructor指向的是父类
// 3. 引用的原型链不能按地址引用
// 4. 修正子类的constructor
var __pro = Object.create(Car.prototype);
__pro.constructor = BWM;
BWM.prototype=__pro;
var m = new BWM('red');
console.log(m);

```
- js内部的constructor == car，构造函数和初始化这个类就是一个东西了.<br/>原型链：当你声明汽车的时候，所有的人都会共享这个方法，省去每一次重新构建的成本。<br/>子类把父类覆盖：js中有按值传递和按引用传递，按引用传递：对象、数组、原型链.

```
(function(){
	var a = 20;
	function a(){}
	console.log(a);// 20
})();
```
- 函数提升：函数的提升优先级大于变量的优先级，因此上面的代码解析顺序为：

```
function a(){}
var a;
a=20;
console.log(a);
```

```
(function(){
	var a = 20;
	var b=c=a;
})();
alert(c); //20
```
- 解析：c提升成全局变量（如果写成`var b，c，a;`外面就会报错“c is not defined”）执行顺序为： 

```
var a = 20;
var b = 20;
c = 20;
```

```
function test(){
	this.a = 20;
}
test.prototype.a = 30;
var p = new test;
alert(p.a); //20
```
- 解析：在构造函数内的a的优先级要比原型链上的a优先级高

```
var user = {
	age:20,
	init:function(){
		console.log(this.age);
	}
}
var data = {age:40};
// 输出data中的age需要用到bind,bind之后返回的是新对象，必须加入var s
var s = user.init.bind(data);
s();   // 40
```
- 解析：改变this的指向，输出data中的age需要用到bind,bind之后返回的是新对象，必须加入var s

```
function test(m){
	m.v = 20;
	// m={v:40;} //40
}
var m = {age:30};
test(m);
alert(m.v); //20
```
- 解析：重写是没有意义的，和赋值之前那个变量值的不是同一个堆内存，原型链也变了


```
$('#test').click(function(){
	console.log(1);
});
setTimeout(function(){
	console.log(2);
});
while(true){
	console.log(3);
}
```
- 执行结果：都输不出 浏览器会卡死
- 解析：1. 在浏览器开发里面，js是分成对应的线程的，分为同步队列（while（true）、for）和异步队列（onclick、setTimeout、ajax），同步队列不执行完，异步队列是拉不回来的<br/>
	2. 为什么平时我们写的setTimeout时间不准，就是因为同步队列的执行时间非常长，阻塞了异步队列的执行

* 模块化(函数式)

```
var module = (function(){
	var n = 5;
	function print(){
		console.log(n);
	}
	function add(x){
		var z = x + n;
		console.log(z);
	}
	return {
		des:"这里是一个模块",
		add:add
	}
})();
module.add(3);
```

* 静态化:不需要对对象进行new

```
var index = {
	data:{
		age:20;
	},
	methods:function(){
	}
}
index.methods(30);
```

* 总结知识点
	- 1. 立即执行函数
	- 2. 闭包：内部的函数可以访问外部函数的变量，把这个函数返回出去。闭包可以保护内部变量，闭包造成内存泄漏（=null）
	- 3. 原型链：
		+ 3.1 构造函数里的属性的优先级比原型链的高
		+ 3.2 在实现面向对象编程的时候 js里面没有类的概念，可以用函数替代
		+ 3.3 但是在函数替代的过程中，我们要注意constructor，实际就是对应的那个函数本身
		+ 3.4 prototype是按引用类型传递的，可以用Object.create可以创建原型链的副本
	- 4. 数值、字符串、布尔类型都是按值传递，对象、数组、原型链是按引用传递的
	- 5. 改变this的方法：call、apply、bind
	- 6. 函数提升和变量提升：函数提升的级别要比变量高
	- 7. jq内部有很多经典的写法，模块化编程的概念、闭包等


	
