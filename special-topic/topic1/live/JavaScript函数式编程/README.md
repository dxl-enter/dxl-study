# 函数式编程（javascript functional programming）
 * 函数式编程思维
 	- 范畴论
 		+ 1. 函数式编程是范畴论的数学分支是一门很复杂的数学，认为世界上所有的概念都可以抽象出一个个范畴
 		+ 2. 彼此之间存在某种关系概念、事物、对象等等，都构成范畴。任何事物都要找出它们之间的关系，就能定义
 		+ 3. 箭头表示范畴成员之间的关系，正式的名称叫做“态射”。范畴论任务，同一个范畴的所有成员，就是不同状态的“变形”。通过“态射”，一个成员可以变形成另一个成员
 		+ 4. 所有成员是一个集合，变形关系是函数
 	- 函数式编程基础理论
 		+ 1. 函数式编程其实相对于计算机的历史而言是一个非常古老的概念，甚至早于第一台计算机的诞生。函数式编程的基础模型来源于lambda（lambda x=>x*2）演算，而lambda演算并非设计于在计算机执行，他是在20世纪三十年代引入的一套用于研究函数定义、函数应用和递归的形式系统。
 		+ 2. 函数式编程不是用函数来编程，也不是传统的面向对象编程。主旨在于将复杂的函数复合成简单的函数（计算理论，或者递归论，或者lambda演算）。运算过程尽量写成一系列嵌套的函数调用。
 		+ 3. javascript是披着c外衣的lisp
 		+ 4. 真正的火热是随着react的高阶函数而逐步升温
 	- 概念
 		+ 1. 函数是一等公民，所谓“第一等功能”，指的是函数与其他数据类型一样，处于平等地位，可以赋值给其他变量，也可以作为参数，传入另一个函数，或者作为别的函数的返回值
 		+ 2. 不可改变的量。在函数式编程中，我们通常理解的变量在函数式编程中也被函数代替了：在函数式编程中变量仅仅代表某个表达式。这里所说的“变量“是不能被修改的。所有的变量只能被赋值一次初值
 		+ 3. map & reduce它们是最常用的函数式编程的方法 
 		+ 4. 好处：函数是“第一等公民”；只用“表达式”，不用“语句”；没有副作用；不修改状态；引用透明（函数运行只靠参数）
 * 函数式编程常用核心概念
 	- 纯函数
 		+ 对于相同的输入，永远会得到相同的输出，而且没有任何可观察的副作用，也不依赖外部环境的状态。
 		
 		```
 		var xs = [1,2,3,4,5,6];
 		// Array.slice式纯函数，因为它没有副作用(并没有改变原数组)，对于固定的输入，输出总是固定的(arrayObject.splice(index,howmany,item1,.....,itemX)改变了原数组的值，函数脏)
 		xs.slice(0,3);
 		xs.slice(0,3);
 		xs.splice(0,3);
 		xs.splice(0,3);
 		```
 		+ 优缺点
 		```
 		import _ from 'lodash'
 		var sin = _.memorize(x=>
 			Math.sin(s);
 		)
 		// 第一次计算的时间会稍微慢一点
 		var a = sin(1);
 		// 第二次有了缓存，速度极快
 		var b = sin(1);
 		```
 		<strong>纯函数不仅可以有效降低系统的复杂度，还有很多很棒的特性，比如可缓存性</strong>
 		```
 		// 不纯的
 		var min = 18;
 		var checkage = age => age > min;
 		
 		// 纯的，这很函数式
 		var checkage = age => age > 18;
 		```
 		<strong>在不纯的版本中，checkage不仅取决于age还有外部以来的变量min。纯的checkage吧关键数字18硬编码在函数内部，扩展性比较差，柯里化优雅函数式解决</strong>
 		+ 纯度和幂等性
 			- 幂等性是指执行无数次后还具有相同的效果，同一的参数运行一次函数应该与连续两次结果一致。幂等性在函数式编程中与纯度相关，但又不一致
 			- Math.abs(Math.abs(-42))
 		+ 
 	- 偏应用函数、函数的柯里化
 		+ 偏应用函数：传递给函数一部分参数来调用他，让它返回一个函数去处理剩下的参数
 		+ 偏函数之所以“偏“，就在于其只能处理那些能与至少一个case语句匹配的输入，而不能处理所有可能的输入

 		```
 		// 带一个函数参数 和 该函数的部分参数
 		const partial = (f,...args) => (...moreArgs) => f(...args,... moreArgs)
 		
 		const add3 = (a,b,c)=>a+b+c
 		//偏应用2 和 3到add3给你一个单参数的函数
 		const fivePlus = partial(add3,2,3);
 		fivePlus(4)
 		//bind实现
 		const add1More = add3.bind(null,2,3)//(c)=>2+3+c
 		```
 		+ 函数的柯里化：柯里化通过偏应用函数实现
 		+ 传递给函数一部分参数来调用他，让它返回一个函数去处理剩下的参数
 		+ 我们一起来用柯里化来改它

 		```
 		var checkage = min => (age => age > min);
 		var checkage18 = checkage(18);
 		checkage18(20);
 		```
 		```
 		// 柯里化之前
 		function add(){
 			return x+y;
 		}
 		add(1,2);
 		
 		// 柯里化之后
 		function addX(y){
 			return function(x){
 				return x+y;
 			}
 		}
 		addX(2)(1)
 		```
 		```
 		function foo(p1,p2){
 			this.val = p1+p2;
 		}
 		// 软绑
 		var bar = foo.bind(null,"p1");
 		var baz = new bar("p2");
 		console.log(bar.val)
 		```
 		bind传参也是柯里化
 		+ 柯里化优缺点

 		```
 		impot {curry} from 'lodash'
 		var match = curry((reg,str) => str.match(reg));
 		var filter = curry((f,arr) => arr.filter(f));
 		var havaSpace = match(/\s+/g);
 		// havaSpace("fffffff");
 		// havaSpace("a b");
 		
 		//filter(havaSpace, ["aaaaaa","hello world"]);
 		filter(havaSpace)([aaaaaa","hello world"]);
 		```
 		事实上柯里化是一种“预加载”函数的方法，通过传递较少的参数，得到一个已经记住了这些参数的新函数，某种意义上讲，这是一种对参数的“缓存”，是一种非常高效的编写函数的方法
 	- 函数组合
 		+ 纯函数以及如何把它柯里化写出的洋葱代码h(g(f(x))),为了解决函数嵌套的问题，我们需要用到“函数组合”
 		+ 我们一起来用柯里化该它，让多个函数像积木一样

 		```
 		const compose = (f,g) => (x=>f(g(x)));
 		var first = arr => arr[0];
 		var reverse = arr => arr. reverse();
 		var last = compose(first, reverse);
 		last([1,2,3,4,5]);
 		```
 	- point free
 		+ 把一些对象自带的方法转化成纯函数，不要命名转瞬即逝的中间变量
 		+ 这个函数中，我们使用了str作为我们的中间变量，但这个中间变量除了让代码变得长了一些以外是毫无意义的。
 		```
 		const f = str => str.toUpperCase().split(' ')
 		```
 		+ 优缺点：

 		```
 		var toUpperCase = ward => word.toUpperCase();
 		var split = x => (str => str.split(x));
 		var f = compose(split(' '),toUpperCase);
 		f("abcd efgh")
 		```
 		<strong>这种风格能够帮助我们减少不必要的命名，让代码保持简洁和通用</strong>
 	- 声明式与命令式代码
 		+ 命令式代码的意思就是，我们通过编写一条又一条的指令去让计算机执行一些动作，这其实一般都会涉及到很多繁杂的环节。而声明式就要优雅很多了，我们通过写表达式的方式来声明我们想干什么，而不是通过一步一步的指示。
 		```
 		// 命令式(最蠢的)
 		let ceos = [];
 		for(var i=0;i<companies.length;i++){
 			ceos.push(companies[i].ceo)
 		}
 		// 声明式
 		let ceos = companies.map(c => c.ceo)
 		```
 		+ 优缺点：
 			- 函数式编程的一个明显的好处就是这种声明式的代码，对于无副作用的纯函数，我们完全不考虑函数内部是如何实现的，专注于编写业务代码。优化代码时，目光只需要集中在这些稳定坚固的函数内部即可。
 			- 相反，不纯的函数式的代码会产生副作用或者以来外部系统环境，使用它们的时候总是要考虑这些不干净的副作用。在复杂的系统中，这对于程序员的心智来说是极大的负担
 	- 惰性求值、惰性函数、惰性链
 		+ 在指令式语言中以下代码会按顺序执行，由于每个函数都有可能改动或者依赖于其外部的状态，因此必须顺序执行。

 		```
 		function somewhatLongOperation1(){somewhatLongOperation1}
 		new LazyChin([1,2,3])
 		```
 		+ 很早以前，都用过ajax兼容代码（可以把里面的代码改成createAjax=new XMLHttpRequest()...）把函数给重写了，下次函数就不需要计算了
 * 更加专业术语
 	- 高阶函数
 		+ 函数当参数，把传入的函数做一个封装，然后返回这个封装函数，达到更高程度的抽象

 		```
 		// 命令式
 		var add = function(a,b){
 			return a+b;
 		};
 		function math(func,array){
 			return func(array[0],array[1]);
 		}
 		math(add,[1,2]);
 		```
 		+ 他是一等公民、它以一个函数作为参数、以一个函数作为返回结果（对象没有它这么便利，不能在内部执行，只能往对象上挂值）
 	- 尾调用优化PTC
 		+ ecs：函数执行栈
 		+ 指函数内部的最后一个动作是函数调用。该调用的返回值，直接返回给函数。函数调用自身，称为递归。如果尾调用自身，就称为尾递归。递归需要保存大量的调用记录，很容易发生栈溢出错误，如果使用尾递归优化，将递归变为循环，那么只需要保存一个调用记录，这样就不会发生栈溢出错误了。

 		```
 		// 不是尾递归，无法优化 斐波那契数列
 		function factorial(n){
 			if(n ===1) return 1;
 			return n * factorial(n-1);
 		}
 		function factorial(n,total){
 			if(n === 1) return total;
 			return factorial(n-1,n*total);
 		} //es6潜质使用尾递归
 		```
 		+ 传统递归

	 		```
	 		function sum(n){
	 			if(n===1) return 1;
	 			return n+sum(n-1);
	 		}
	 		```
	 		执行循序为
	 		```
	 		sum(5)
	 		(5+sum(4))
	 		(5+(4+sum(3)))
	 		(5+(4+(3+sum(2))))
	 		(5+(4+(3+(2+sum(1))))
	 		(5+(4+(3+(2+1)))
	 		(5+(4+(3+3))
	 		(5+(4+6))
	 		(5+10)
	 		15
	 		```
	 		普通递归时，内存需要记录调用的堆栈执行的深度和位置信息。在最底层计算返回值，再根据记录的信息，跳回上一层级计算，然后再跳回高一层，一次运行，直到最外层的调用函数。在cpu计算和内存会消耗很多，而且当深度过大时，或出现堆栈溢出（栈的递归和死循环时不一样的，栈的递归你把内存用完了，死循环是UI的主线程没有能力执行其他的代码了，js是单线程，主线程不能激活其他的代码）
	 		
 		+ 细数尾递归

 			```
 			function sun(x,total){
 				if(x ==== 1) return x + total;
 				return sun(x - 1, x + total);
 			}
 			```
 			执行顺序为
 			```
 			sum(5,0)
 			sum(4,5)
 			sum(3,9)
 			sum(2,12)
 			sum(1,14)
 			15
 			```
 			整个计算过程是线性的，调用一次sum(x,total)后，会进入下一个栈，相关的数据信息和跟随进入，不再放在堆栈上保存。当计算完最后的值之后，直接返回到最上层的sum(5,0).这能有效的防止堆栈溢出。
 			在es6，我们将迎来尾递归优化，通过尾递归优化，js代码在解析机器码的时候，将会向while看起，也就是说，同时拥有数学表达式能力和while的效能。
 		+ 尾递归优化

 		```
 		function foo(){
 			return bar(n*2);
 		}
 		function bar(){
 			// 查看调用帧
 			console.trace()
 		}
 		foo(1);
 		```
 		上面代码的目标
 		```
 		// 只有一个执行栈
 		foo
 		```
 		+ 尾递归问题
 			- 尾递归的判断标准是函数运行（最后一步）是否调用自身，而不是是否在函数的（最后一行）调用自身，最后一行调用其他函数 并返回叫尾调用。尾调用优化`（function init(){test(i);} function test(i){init(i-1 );}）`
 			- 按道理尾递归调用 调用栈永远都是更新当前的栈帧而已，这样就完全避免了爆栈的危险。但是现如今的浏览器并未完全支持。原因有二：1.在引擎层面消除递归是一个隐式的行为，程序猿意识不到；2. 堆栈信息丢失了开发者难以调试；3. 既然浏览器不支持我们可以把这些递归写成while，不留堆栈执行记录 ，浏览器的尾递归我们可以强制开启
 			- 能用while解决的问题，都用while，它是线性的，不会在我们的栈里面留那么多执行记录
 			- 尾递归有2种：一种是浏览器实现的（如下，它比较狠，无论你调用了多少帧，它会把只留当前的一帧），一种是自己写的
				```
		 		function foo(){
		 			return bar(n*2);
		 		}
		 		function bar(){
		 			// 查看调用帧
		 			console.trace()
		 		}
		 		foo(1);
		 		```
		 		上面代码的目标
		 		```
		 		// 只有一个执行栈
		 		foo@ VM65:2
		 		(anonymous) @ VM65:10
		 		// 强制执行 只留下bar
		 		return continue
		 		return
		 		#function()
		 		// 遗憾的是浏览器并未支持
		 		```
 		+ 
 	- 闭包
 		+ 如下例子，虽然外层的makePowerFn函数执行完毕，栈上的调用帧被释放，但是堆上的作用域并不被释放，因此power依旧可以被powerFn函数访问，这样就形成了闭包

 		```
 		function
 		```
 	- 容器、functor
 	- 错误处理、either AP
 	- IO
 	- Monad

 * 当下函数式编程最热的库
 * 函数式编程的实际应用场景
