# javascript 基础测试题（2019/05/13）
### 1. 关于函数/变量提升
```
	alert(a);    1
	a();   2
	var a=3;
	function a(){
	    alert(10)
	} 
	alert(a);    3
	a=6;
	a();   4
```
* 执行顺序：

	```
	function a(){
     alert(10)
	}
	var a;
	alert(a);
	a();
	a=3;
	alert(a);
	a=6;
	a();
	
	```
* 执行结果：

	```
	1. f a(){alert(10)} //变量提升，并且函数优先级高于变量。
	2. 10 //执行了a(){alert(10)}
	3. 3 //给a赋值了3
	4. a is not a function 此时已经给a赋值了6,a已经不是函数了，所以会弹出错误
	
	```
* 小知识：

	```
	console.log(c)//ƒ c(){console.log('hahha') 
	function c(){
	    console.log('hahha')
	}
	var c = 1;
	```
	```
	console.log(c) //ƒ c(){console.log('hahha') 
	var c = 1;
	function c(){
	    console.log('hahha')
	}
	
	```
	- 解释：如果变量名和函数名相同时，当变量没有意思时（只声明不赋值）时，会被函数覆盖，只要在调用之前赋值（无论是null还是undefined都是有意义的），会覆盖函数。

	```
	function yideng() { 
        console.log(1);
    }
    (function () { 
        if (false) {
            function yideng() {
                console.log(2);
            }
        }
        yideng(); //yideng is not a function
    })();
	```
	- 解释：在早期的浏览器中，弹出来的结果应该是2,（因为变量提升，整个`function yideng(){}`会被提升到整个函数作用域的顶端）但是如果弹出来是2的话，我们写的if语句就完全没有意义了。后来浏览器为了修正这个错误，像这种情况下面的函数提升就只是 `var yideng`提升到函数作用域的顶端，本题中false所以没进入函数体，所以yideng()就会报错`yideng is not a function`。而不是像第一题那样，整个函数体都提到前面。(据说除了if，好像while，switch，for也一样)

	```
	if(false){
        var a = 1;
    }
    console.log(a)//undefined
	
	```
	- 解释：变量声明提前，但是没有赋值

### 2. 关于this
```
	this.a = 20; 
	var test = {
    a: 40,
    init:()=> {
        console.log(this.a);  
        function go() {
            console.log(this.a);
        }
        go.prototype.a = 50; 
        return go;
        }
    };
    new(test.init())();   //20   50 
	
```
- 解释：箭头函数的this绑定父级的词法作用域，所以他的`this.a`固定了是20。go本身没有a 这个属性，所以new出来的对象也没有这个属性，会到原型链上面去找。所以是50。

```
  this.a = 20; 
  var test = {
    a: 40,
    init:()=> {
        console.log(this.a); 
        function go() {
           this.a = 60;
            console.log(this.a);
        }
        go.prototype.a = 50; 
        return go;
        }
    };
    var p = test.init();  //20 
    p();  //  60 
    new(test.init())();   //  60，60
```
* 执行结果

```
	1. var p = test.init(); 此时test.init()会执行一遍。此时的箭头函数中的this绑定了最外层的this（test父级作用域的this），也就是this.a = 20
	2. p() 此时相当于执行go()，注意：这个时候是var p = test.init（）,所以执行p()时的this是指向windows，也就是我们现在看到的最外层的this.a = 20的那个this，此时会执行this.a = 60，将windows的this.a 更改成60,执行之后打印出来的this.a=60.
	3. new(test.init())()：test.init()会取到已经绑定了的父级词法作用域的this，不过此时的this.a已经被改为60,所以打印出来60。继续执行，打印出60。
```
* 小知识：

	```
	this.a = 20;
	var test = {
		a:40,
		init:function(){
			function pp(){
				var a = 30;
				function go(){
					console.log(this.a);
				}
				go();
			}
			pp();
		}
	}
	```
	- 解释：因为这里是var 不是this.a
	
	```
	 function test(){
        console.log(this)
    }
    var obj = {
        f:test
    }
    (obj.f)()  //Cannot read property 'f' of undefined
	```
	- 解释：没有加分号，在浏览器看来var obj = {f:test}(obj.f)() 是这样连在一起的

	```
	function test(){
        console.log(this)
    }
    var obj = {
        f:test
    };
    (obj.f)()//{f: ƒ}
	```
	- 解释：指向了obj这个对象，因为是obj调用了test()

	```
	function test(){
        console.log(this);//window
    }
    var obj = {
        f:test
    };
    (false || obj.f)()
	```
	- 短路语句的结果不也是obj.f，运算的结果应该也是obj才对啊。
但是()里面是计算，所以里面应该是表达式，也就是说里面相当于var xx = obj.f，然后xx(),此时this肯定是指向全局变量window

### 3. 关于闭包块级作用域
请写出如下点击的输出值，并用三种办法正确输出li里面的数字

```
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
</ul>
<script type="text/javascript">
    var list_li = document.getElementsByTagName("li"); 
    for (var i = 0; i < list_li.length; i++) {
        list_li[i].onclick = function() { console.log(i);
        }
    }
</script>
```
- 解释：真的是很经典的一道题啊！！！！大家可以闭着眼睛说不管点击哪个li都只会输出6。跟Js的单线程和异步队列【定时器setTimeout、setInterval和事件触发onclick、onfocus等和http请求都是异】有关。JS引擎线程会先执行同步代码，之后才执行处于任务队列里面的异步代码
- ES6的let

	```
	for (let i = 0; i < list_li.length; i++) {
	  list_li[i].onclick = function() { 
	      console.log(i+1);
	  }
	}
	```
- 闭包，立即执行函数

	```
	for(var i = 0; i < list_li.length; i++){
	  (function(i){
	      list_li[i].onclick = function(){
	          console.log(i+1)
	      }
	  })(i)
	}
	```
- this指向

	```
	for (var  i = 0; i < list_li.length; i++) {
	      list_li[i].onclick = function() { 
	          console.log(this.innerHTML);
	      }
	  }
	```

### 4. 按地址传递和按值传递

```
function test(n){
    n = {
        v:5
    };
}
var m = {
    k:30
};
test(m);  
alert(m.v); //undefined
```
- 解释：n = {v:5};重写了n，是在堆内存空间中新建了一个Object（）。注意的是，在这个函数里n和我们的实参m指向的并不是同一块内存了，n不管什么操作都和m没有关系了，也就是说在这个函数里面，只是新建了一个局部变量n,并没有真正对m进行说明操作。我们可以看到打印出来的m{k:30},证明了这个观点。
* 小知识

	```
	function test(n){
        n.v = 5;
    }
    var m = {
        k:30
    };
    test(m);  
    alert(m.v); //5
	```
	- 解释：这里的m,n指向同一个内存，对n进行操作肯定也会对m造成影响

	```
	var a = 1;
    var b = a;
    b = 2;
    console.log('a',a);  //1
    console.log('b',b);  //2
    ```
    - 这是按值传递，b对a并没有造成任何影响

    ```
    var a = {
        num : 1
    };
    var b = a;
    b.num = 2;
    console.log('a',a); //{num:2}
    console.log('b',b); //{num:2}
    ```
    - 解释：这是按引用传递，改动b就相当于改动a

    ```
     var a = {
        num : 1
    };
    var b = a;
    b = {};  
    b.num = 3;
    console.log('a',a); //{num:1}
    console.log('b',b); //{num:3}
    ```
    - 此时 b = {}开辟了新的内存地址

    ```
    function add(n) {
        return n += 100;
    }

    var _count = 100;
    var result = add(_count);
    console.log(result);    //200
    console.log(_count);    //100 
    ```
    - 解释：在向参数传递 基本类型 的值时，被传递的值会被赋给一个局部变量（即命名参数/arguments对象中的一个元素），_count没有变化，因为是值传递，内部的变化不会反映到函数外部

    ```
    function setName(p) {
        p.name = 'hello';
    }

    var person = new Object();
    setName(person);
    alert(person.name);     //hello
    ```
    - 解释：在向参数传递  引用类型 的值时，会把这个值在内存中的地址复制给一个局部变量，因此这个局部变量的变化会反映在函数的外部。<br/>也就是说以上代码创建的一个对象并保留在一个变量  person中。然后，person在执行setName()函数时被复制给了p，在这个函数内部，p和person引用的是同一个对象。即使变量person是按值传递的，p也会按引用来访问同一个对象。<br/>所以，当执行`p.name = 'hello'`，外部的`person.name => hello`,因为person所指向的对象在堆内存中只有一个，而且是全局对象。

    ```
    function setName(p) {
        p.name = 'hello';
        p = new Object();
        p.name = 'world';
    }

    var person = new Object();
    setName(person);
    alert(person.name);     //输出仍然是 hello
    ```
    - 当在函数内部重写p的时候，这个变量的引用就是一个局部对象了。
<br/><strong>也就是说，这个时候，p和person指向的是不同的地方，p的任何操作（增删查改）跟person是没有任何关系的,而这个局部对象，会在函数执行完毕后自动销毁。</strong>

	```
	function setName(p) {
        p = {
            name : 'world'
        }
        p.name = 'hello';
    }

    var person = new Object();
    person.age = 10;
    setName(person);
    console.log(person);
    console.log(person.age);  //10
    console.log(person.name);     //undefined
    ```
    - 本来p和person开开心心指的同一块内存，但是p重写了！重写是什么概念，就是p指向了一块新的内存，接下来不管p有什么操作，和person都没有关系，所以我们打印出来person，可以看到他还是和原来一样。{age:10}。person.name就还是undefined了。

    ```
    function setName(obj) {
        obj.name = 'Nicholas';
        obj = new Object();
        obj.name = "Greg";
        console.log(obj.name); // "Greg"
    }
    var person = new Object();
    setName(person);
    alert(person.name) // "Nicholas"
    ```
    - 解释：person这个object作为参数传递给function的时候，function内部的作用域可以找到person而且这个时候obj的值是一个指向的是“堆内存空间中person所指向的这个Object它本身”（person本身也是个指针，obj是person这个指针被作为参数传递后复制出来的副本）；然后下一步new出一个Object的时候，是在堆内存空间中新建了一个Object（），这个时候obj是指向这个新new出来的Object的指针，但是！person依旧是指向原来的堆内存，所以对这个新Object新增一个叫name的属性的时候对person并没有任何影响。需要注意的是，在function执行的这一个阶段里，对于原来的Object进行操作只有一次，即给它的name属性赋值为'Nicholas'，随后的操作是对另外一块新的内存进行操作了。所以在外部的输出就是"Nicholas"；

    ```
    function setName() {
        person.name = 'Nicholas';
        person = new Object();
        person.name = "Greg";
        console.log(person.name); // "Greg"
    }
    var person = new Object();
    setName();
    console.log(person.name) // "Greg"
    ```
    - 从始至终person伴随着我们的一直是person这个指针， 最初在声明阶段即在function外部那个 `var person = new Object()；` 时，这一步它是指向new出来位于堆内存内的Object。但在之后function中的执行阶段， person指针又被指向function里new出的这个Object了，<strong>注意这次不是局部变量，所以person就一直指向新的Object()了，</strong>所以后边的log输出就是这个新new出来的对象的name: "Greg" 。

### 5. 写代码要聪明
请用一句话算出0-100之间学生的学生等级，如90-100输出为1等生、80-90为2等 生以此类推。不允许使用if switch等

```
10-Math.floor(x/10)
```
有这样的一段代码：

```
var a = "test";
if(a == "test"){
    console.log(1);
}else if(a == "qq"){
    console.log(2);
}
```
我们可以直接改写为：

```
var obj = {
    "test": function(){
        console.log(1)
    },
    "qq": function(){
        console.log(2)
    }
}
var s = "test";
obj[s]()
```
- 有这么一句话，叫做，只要超过了两层的if-else的代码那都不是好代码。可以看看书。《代码简洁之道》 《重构》

### 6. 数组方法
请问已经一句话遍历变量a（禁止使用for 已知var a = "abc")

```
var a = "abc";
Array.prototype.slice.call(a)
```
- 借用数组原型链上面的方法

```
var a = "abc";
[].forEach.call(a,item=> {
    console.log(item)
})
```
- 让数组方法指向我们要遍历的a

```
var a = "abc";
[...a].map(item=>{
    console.log(item);
})
```
- 把a变成数组

```
var a = "abc";
Array.from(a).map(item => {
    console.log(item)
})
```
- 把a 变成数组。`Array.from()`方法从一个类似数组或可迭代对象中创建一个新的数组实例。

```
console.log(Array.from('foo'));
// expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], x => x + x));
// expected output: Array [2, 4, 6]
```

### 7. 关于继承
-请在下面写出JavaScript面向对象编程的混合式继承。并写出ES6版本的继承。<br/>要求：汽车是父类，Cruze是子类。父类有颜色、价格属性，有售卖的方法。Cruze子类实现父类颜色是红色，价格是140000,售卖方法实现输出如下语句：将 红色的Cruze买给了小王价格是14万。

```
var Car = function(color,price){
    this.color = color;
    this.price = price;
}
Car.prototype.sale = function(){
    console.log(this.color + '色的车卖了'+this.price)
}
var Cruze = function(color,price){
    Car.call(this,color,price);
}
//需要解决的问题有
//1.拿到父类原型链上面的方法
//2.不能让构造函数执行两次
//3.引用的原型链不能按地址引用（不然子类上面的修改会影响到父类，可以使用Object.create来给做个副本）
//4.修正子类的constructor 
var __pro = Object.create(Car.prototype);//复制原型链
__pro.constructor = Cruze;
Cruze.prototype = __pro;
var m = new Cruze('red',14);
console.log(m);
m.sale()
```
ES6写法

```
class Car{
    constructor(color,price){
        this.color = color;
        this.price = price;
    }
    sale(){
        console.log(this.color +'色的车卖了'+this.price)
    }
}
class Cruze extends Car{
    constructor(color,price){
        super(color,price);
    }
}

var bmw = new Cruze('red','199万');
bmw.sale()
```

### 8. arguments
```
var length = 10; 
function fn() {
    console.log(this.length);
}
var yideng = { 
    length: 5,
    method: function (fn) { 
        fn();
        arguments[0]();
    }
};

yideng.method(fn, 1); //10 2 
```
- 解释：其实arguments是类数组对象{0:{console.log{},1:1}，arguments0是arguments在调用这个fn函数，自然而然就是指向arguments了，如果是yideng.method(fn, 1，2)那么将会输出3，也就是实参的个数。

```
function fn() {
    console.log(this.length);
}
var yideng = { 
    length: 5,
    method: function (fn) { 
        fn();
    }
};

yideng.method(fn);
```
- 这个时候执行fn的this还是指向window的。window.length是啥？
length 属性返回在当前窗口中frames的数量（包括IFRAMES）。
没想到吧！！所以这个时候的输出就要看有多少个iframe了。
