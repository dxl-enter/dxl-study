## 1. JavaScript语言新发展【深度实践课】
### 1.1 JavaScript与QA工程师
    （1）单元测试
      目的：单元测试能够让开发者明确知道代码结果
      原则：单一职责、接口抽象、层次分离
      断言库：保证最小单元是否正常运行检测方法
      单元测试框架：better-assert(tdd断言库)、should.js(bdd断言库)、expect.js(bdd断言库)、chai.js(tdd、bdd双模)、jasmine.js(bdd)、nodejs本身集成了request
      自动化单元测试：karma自动化runner集成phantomjs无刷新
      npm install -g karma
      npm install karma-cli --save-dev
      npm install karma-chrome-launcher --save-dev
      npm install karma-phantomjs-launcher --save-dev
      npm install karma-mocha --save-dev
      npm install karma-chai --save-dev
      报告和单测覆盖率检查：
      npm install karma-coverage --save-dev
      coverageReporter:{type:'html',dir:'coverage/'} //配置代码覆盖测试生成结果
    （2）性能测试
      基准测试：
      面向切面编程aop无侵入式统计
      benchmark基准测试方法，它并不是简单地统计执行多少次测试代码后比对时间，它对测试有着严密的抽样过程。执行多少次取决于采样到的数据能否完成统计。根据统计次数计算方差。
      压力测试：
      对网络接口做压力测试需要检查的几个常用指标有吞吐率、响应时间和并发数，这些指标反应了服务器并发处理能力。
      pv网站当前访问人数 uv独立访问人数。pv每天几十万甚至上百万就需要考虑压力测试。换算公司qps = pv/t ps：1000000/10*60*60=27.7（100万请求集中在10个小时，服务器每秒处理27.7个业务请求）。
      常用的压力测试工具是：ab，siege，http_load
      ab -c 100 -n 100 http://localhost:8001 每秒持续发出28个请求request per second表示服务器每秒处理请求数，即为qps failed requests 表示此次请求 理论上压测值越大增加connection times连接时间  端向服务器建立连接、服务器端处理请求、等待报文
    （3）安全测试（web前端黑客揭秘）
      xss：评论alert(1)
      sql（万能密码1=1）
      csrf：劫持
    （4）功能测试
      用户真实性检查：
      selenium-webdriver(自动化测试) - nodejs
      protractor selenium-standalone(记录所有的log)
      http://webdriver.io/ webdriver i/o
      冒烟测试 smoketest 自由测试的一种，找到一个bug开发修复，然后专门针对此bug，优点节省时间防止build失败，缺点是覆盖率极低
      回归测试 修改一处对整体功能全部测试，一般配合自动化测试。
    （5）jslink和jshint
      目的：检测js代码标准
      原因：js代码诡异，保证团队代码规范
      jslink：http://www.jslink.com/
      jshint：http://www.jshint.com/
      搭配自动化任务管理工具完善自动化测试grunt-jshint\grunt-jslink
### 1.2 JavaScript语言精粹1
    (1)数据类型：
      值类型：boolean number string null undefined(声明但为赋值) symbol  存储：直接内存（栈内存）
      对象：object（array、regexp、date、math） 地址放到栈内存，实际上的内容放到堆内存中
    (2)变量提升
      js中可以引用稍后声明的变量，而不会引发异常，这一概念成为变量声明提升
    (3)函数
      定义函数：函数声明（function fn(){}）、函数表达式(var fn = function(){})、function构造函数(var fn = new Function(){})、箭头函数(var fn = (p) => {})
    (4)console本质是用eval包装的，如果想看真正的输出到javascript控制台watch中（javascript runtime）
    (5)构造函数
      构造函数和普通函数并没有区别，使用new关键字调用就是构造函数，使用构造函数可以实例化一个对象
      函数的返回值有可能：显式调用return返回return后表达式的求职；没有调用return返回undefined
      构造函数返回值：没有返回值、简单数据类型、对象类型
      前两种情况构造函数返回构造对象的实例，实例化对象正是利用的这个特性
      第三种构造函数和普通函数表现一致，返回return后表达式的结果
    (6)prototype
      每个函数都有一个prototype的对象属性，对象内又一个constructor属性，默认指向函数本身
      每个对象都有一个__proto__的属性，属性指向其父类型的prototype
      当作对象的属性用的时候就叫做方法
      当它单独拿出来用的时候就叫做函数
    (7)this和作用域
      作用域可以通俗的理解：
        我是谁：this
        我有哪些马仔：马仔就是我的局部变量 
       this场景：是运行时的变量（只有当函数运行的时候才知道你是谁）
        严格模式：undefined
        非严格模式：全局对象
          node：global
          浏览器：window
        构造函数：对象的实例
        对象方法：对象本身
    (8)call和apply（可以改掉你是谁，写的时候并不知道你是谁，只有在runtime中才能知道你是谁）
      改变this的作用域
      fn.call(context,arg1,arg2,...)
      fn.apply(context,args)
      借用构造函数
      function isNumber(obj){
        return Object.prototype.toString.call(obj) === '[object Number]';
      }
    (9)Function.prototypr.bind
      bind返回一个新函数，新函数的作用域为bind参数
      function fn(){this.i = 0; setIntercal(function(){console.log(this.i++);},500)} // NaN
      function fn(){this.i = 0; setIntercal(function(){console.log(this.i++);}.bind(this),500)} // 0,1,2...
    (10)箭头函数
      箭头函数是es6提供的新特性、是简写的函数表达式，拥有词法作用域（写的时候是谁，明确就是谁，没法改变）和this值
      function fn(){this.i = 0; setIntercal(()=>{console.log(this.i++);},500)} // 0,1,2...
    (11)继承
      在js的场景，继承有两个目标，子类需要得到父类的：对象的属性、对象的方法
      es6 class与继承
      class People({constructor(name,age){}}
      class English extends People{
        constructor(name,age){super(name,age)}
      }
    (12)lable statement
      loop:
        break(loop)
      var x = {a:1} //{a:1}
      {a:1} //1  此句有歧义，js中叫语句优先（能解释成语句的不会解释成表达式的），解释：a这个lable下面有个表达式是1，结果就是1
      (a:1,b:2) //报错 逗号要求所有的项都得是表达式，而b:2不是表达式，所以报错
    (13)自执行函数
      (function(){}()):如果没有()解析出错：因为js会把它当做语句。而()要求里面的东西是表达式，会按照表达式的语法执行
      (function(){})()：()要求里面的东西是表达式，表达式返回的是函数，后面的()表示调用
      [function(){}()]：同上上
      ~function(){}()：数值运算强制要求后面的是表达式，数值运算都是改变语法解析顺序的（去除语句优先原则）
      !function(){}()
      +function(){}()
      -function(){}()
      delete function(){}()：操作符强制要求后面的是表达式
      typeof function(){}()
      void function(){}()
    (14)精华
      高阶函数：是把函数当成参数或者返回值是函数的函数
        回调函数 
        [1,2,3,4].forEach(function(item){console.log(item)})
      闭包：由两部分组成：函数、环境（函数创建时作用域内的局部变量）
        解决变量污染问题
        function makeCounter(){
          var init = init || 0;
          return function(){return ++init;}
        }
      惰性函数
      柯里化
        一种允许使用部分参数生成函数的方法
        function isType(type){
          return function(obj){
            return Object.prototype.toString.call(obj) ==='[object' + type +']'
          }
        }
        var isNumber = isType('Number')
        console.log(isNumber(1))
        console.log(isNumber('s'))
        var isArray = isType('Array')
      尾递归：
        尾调用是指某个函数的最后一部是调用另外一个函数
        函数调用自身，称为递归
        如果尾调用自身，就称尾递归
        递归很容易发生“栈溢出”错误（stack overflow）
      反柯里化：
      Function.prototype.uncurry = function(){
        return this.call.bind(this);
      }
      // push属性只要有lenth和用角标反问的都可以调用
      var push = Array.prototype.push.uncurry();
      var arr = [];
      push(arr,1);
      push(arr,2);
      console.log(arr); //[1,2]
    (15)我们写的程序是需要设计的，设计的时候是需要抽象和封装的，抽象变化 ，封装共性
    (16)好的操作dom是：数据驱动ui，用事件接受action，所有的变化都是可控的
### 1.3 JavaScript语言精髓2
    （1）作用域
      一个作用域内，某一个变量没有用var申明的话，那它声明的是全局作用域下的变量
      作用域由大到小：
        程序级：
        文件级：
        函数级：
        块级：
      js的作用域：
        全局作用域：
        函数作用域：
        块级作用域：
    （2）作用域链
      在js中，函数也是对象，函数对象和其他对象一样，拥有可以通过代码访问和属性和一系列仅供js引擎访问的内部属性。其中一个内部属性是[[scope]]，由ecma-262标准第三版定义，该内部属性包括了函数被创建的作用域中对象的集合，这个集合被称为函数的作用域链，它决定了哪些数据能被函数访问。
    （3）变量与函数声明提前
      if(!(username in window)){
        var username = "dxler";
      }
      console.log(username); //undefined
      解释：js没有块级作用域，只有函数级作用域，所以这行代码中都是在全局作用域下执行的，因为变量会声明提前，所以username会被提前声明，在声明之后才执行的判断语句，判断语句false没有进行赋值操作，所以返回undefined
      function foo(){
        alert(test);      //undefined
        var test = "bbb";
        alert(test)       //bbb
      }
      foo();
      执行顺序：
      声明函数foo -> 调用函数foo -> 声明变量test -> alert（test） -> test变量赋值为bbb -> alert（test）
    （4）原型对象是什么
      在js中，没定义一个对象（函数）时，对象中都会包含一些预定义的属性，其中函数对象的一个属性就是原型对象prototype。普通对象没有prototype属性，但是有__proto__属性
      function fn(){}
      console.log(typeof fn.prototype)  //object
      console.log(typeof Function.prototype)  //Function
      console.log(typeof Object.prototype)  //object
      console.log(typeof Function.prototype.prototype)  //undefined
    （5）构造函数
      构造函数的返回值：
        不写return：返回的都是对象实例，都是类的实例
        写return：返回的是复杂的数据类型时，返回的就是实际返回的数据，不是我返回的实例了
    （6）原型对象中的constructor
      每个原型对象prototype中都有一个constructor属性，默认指向函数本身
      Person.prototype.constructor === Person //true
      Function.prototype.constructor === Function //true
      Object.prototype.constructor === Object //true
      Object.constructor === Function //true
      // 练习题1
      var name = 'global'
      function A(name){
        alert(name);  // 3
        this.name = name;
        var name = '1';
      }
      A.prototype.name = '2';
      var a = new A('3');
      alert(a.name); // 3
      delete a.name;
      alert(a.name); // 2
      解析：原型链的实现   实例话对象（属性、__proto__）-> person.prototype(getname()、__proto__) -> object.prototype(__proto__) -> null
      //练习题2
      function fun(n,o){
        console.log(o);
        return {
          fun:function(m){
            return fun(m,n)
          }
        }
      }
      var a = fun(0);
      a.fun(1);
      a.fun(2);
      var b = fun(0).fun(1).fun(2).fun(3);
      var c = fun(0).fun(1);
      c.fun(2);
      c.fun(3);
      解析：还原作用域链（树形、嵌套方式）、值传递和引用传递
    （7）闭包为什么会内存泄漏
      ie6内核：最典型的内存泄漏问题是循环引用：a引用了b，b引用了c，c引用了d，d又引用了a，这样会产生死循环的引用，而这个引用在浏览器的回收机制中叫做标记清除法
    （8）函数式编程
      《javascript函数式编程》 
    （9）小技巧
      如果直接调用fn():则this指向window，如果是obj.fn()：则this指向.之前的对象也就是obj
      如果this.date = undefeated 那么this.date.name 就会报错

