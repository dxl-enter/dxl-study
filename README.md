# dxl-study
01 专题一.JavaScript语言新发展【直播课】
02 精英班预读班
03 Linux基础入门
04 EcmaScript5.1新增语法【上】
05 EcmaScript5.1新增语法【下】
06 PHP与MySQL开发入门【上】
  6.1 初识php
  6.2 php基础操作
  6.3 初识phpMyAdmin
  6.4 PHP与MySQL
  6.5 PHP与MySQL小实战
  6.6 PHP PDO
07 PHP与MySQL开发入门【中】
  7.1 PHP面向对象的介绍
  7.2 构造方法与析构方法
  7.3 PHP面向对象之封装性
  7.4 PHP面向对象之继承和多态
    （1）类继承的应用
      php只支持单继承，不允许多重继承。一个子类只能有一个父类，不允许一个类直接继承多个类，但一个类可以被多个类继承。
      可以有多层继承，即一个类可以继承某一个类的子类，如类b继承了类a，类c又继承了类b，那么类c也间接继承了类a
    （2）访问类型控制
                    private       protected        public(默认的)
      在同一类中      可以           可以              可以
      在子类中        不可以         可以              可以
      在类的外部      不可以         不可以             可以
    （3）子类中重载父类的方法
      在子类里面允许重写（覆盖）父类中的方法
      在子类中，使用parent访问父类中被覆盖的属性和方法
      parent::construct();
      parent::fun();
  7.5 PHP抽象类与接口
    (1)抽象方法和抽象类
      当类中有一个方法，他没有方法体，也就是没有花括号，直接分号结束，像这种方法我们叫抽象方法，必须使用关键字abstract定义。如public abstract function fun();
      包含这种方法的类必须是抽象类，也要使用关键字abstract加以声明。（即使用关键字abstract修饰的类为抽象类）
      抽象类的特点的：不能实例化（也就是不能new成对象）；若想使用抽象类，就必须定义一个类去继承这个抽象类，并定义覆盖父类的抽象方法（实现抽象方法）
    (2)接口技术
      php与大多数面向对象编程语言一样，不支持多重继承，也就是说每个类只能继承一个父类。为了解决这个问题，php引入了接口，接口的思想是指定一个实现了该接口的类必须实现的一系列函数
      定义格式：interface 接口名称{// 常量成员（使用const关键字定义）// 抽象方法（不需要使用abstract关键字）}
      使用格式：class 类名 implements 接口名1，接口名2{......}
    (3)抽象类和接口有什么区别
      当你关注一个食物的本质的时候，用抽象类；当你关注一个操作的时候，用接口。
      接口是对动作的抽象，表示这个对象能做什么，对类的局部行为进行抽象。
      抽象类是对根源的抽象，表示这个类是什么，对类的整体进行抽象，对一类事物的抽象描述。
      比如，男人和女人这两个类（如果是类的话，他们的抽象类是人）。说明，他们都是人，人可以吃东西，狗也可以吃东西，你可以把“吃东西”定义成一个接口，然后让这些类去实现它。
      所以，在高级语言上，一个类只能继承一个类（抽象类）（正如人不可能同时是生物和非生物），但是可以实现多个接口（吃饭接口、走路接口）
      接口是抽象类的变体，接口中所有的方法都是抽象的。而抽象类是声明方法的存在而不去实现它的类。
      接口可以多继承，抽象类不行。
      接口定义方法，不能实现，而抽象类可以实现部分方法。
      接口中基本数据类型为static而抽象类不是的。
      接口中不能含有静态代码块以及静态方法，而抽象类可以含有静态方法和静态代码块。
    (4)多态应用
      对象的多态性：是指在父类中定义的属性或行为被子类继承之后，可以具有不同的数据类型或表现出不同的行为。这使得同一个属性或行为在父类及其各个子类中具有不同的语义。
  7.6 PHP常见的关键字
    (1)final关键字
      在php5中新增加了final关键字，它只能用来修饰类和方法。不能使用final这个关键字来修饰成员属性。
      final的特性：
      使用final关键字标识的类不能被继承
      使用final关键字标识的方法不能被子类覆盖（重写），是最终版本
      目的：一是为了安全，二是没必要被继承和重写
    (2)static关键字
      static关键字表示静态的意思，用于修饰类的成员属性和成员方法（即静态属性和静态方法）
      类中的静态属性和方法不用实例化（new）就可以直接使用类名访问         格式： 类::$静态属性
      在类的方法中，不能this来引用静态变量或静态方法，而需要用self来引用  格式： self::$静态属性   self::$静态方法
      静态方法中不可以使用非静态的内容，就是不让使用$this
      静态属性是共享的，也就是new很多对象也是公用一个属性
    (3)单例设计模式
      单例模式的主要作用是保证在面向对象编程设计中，一个类只能有一个实例对象存在
    (4)const关键字
      const是一个在类中定义常量的关键字，我们都知道在php中定义常量使用的是“define()”这个函数，但是在类里面定义常量使用的是"const
      "这个关键字
      语法：
      const CONSTANT = 'constant value';//定义
      echo self::CONSTANT;              //类内部访问
      echo className::CONSTANT;         //类外部访问
    (5)instanceof关键字
      instanceof关键字用于检测当前对象实例是否属于某一个类或这个类的子类
    (6)php面向对象程序设计的魔术方法：
      克隆对象
      类中通用的方法__toString()
      __call()方法
      自动加载类
        php5中当new实例化一个不存在的类时，则自动调用此函数__autoload(),并将类名作为参数传入此函数。可以使用这个实现类的自动加载。
      对象串行化
    (7)php面向对象程序设计的常用函数：
      class_exists（检查类是否已存在）与get_class_methods（返回由类的方法名组成的数组）函数
      get_class（返回对象类名）与get_object_vars（返回由对象属性组成的关联数组）函数
      get_parent_class（返回对象或类的父类名）与is_a（如果对象属于该类或该类是此对象的父类则返回true）函数
      method_exists（检查类的方法是否存在）与property_exists（检查对象或类是否具有该属性）函数
  7.7 PHP错误处理类
    （1）系统自带的异常处理
    （2）自定义异常处理
    （3）捕捉多个异常处理
  7.8 PHP和JavaScript的比较
  （www.cnblogs.com/xiaochaohuashengmi/archive）
    （1）
    （2）
    （3）
08 PHP与MySQL开发入门【下】
  8.1 MySQL数据库客户端基础
    （1）www.mysql.com -> downlods -> mysql community -> mysql workbench
  8.2 MySQL创建表
    create table 数据库名.表名(
      `id` int not null auto_increment comment '',
      primary key(`id`) comment ''
    );
  8.3 MySQL函数SQL语句
    count(*):查询的数据有几条
    min(birthdate):求最小值
    表名.*: 返回表中的其他数据
    max():求最大值
    sum():求和
  8.4 MYSQL条件查询
    where 列名 between ‘’ and ‘’ ： 中间
    where 列名 like ‘%王%’：%表示通配符，表示字符串中含有王这个字（模糊查询）数据库效率比较低
  8.5 MYSQL复杂条件查询
    排序：order by 列名 desc(倒序)/asc(正序，默认)
    多个数据表操作时，必须有关联的字段：
    select * from 表名1，表名2 where 表名1.classid = 表名2.id
    *会消耗数据库性能，网络的性能
    leftjoin：
    select * from 表名1 left join 表名2 on 表名1.classid = 表名2.id
    mysql用join on比较多
09 EcmaScript6
  9.1 ES6简介与环境搭建
    kangax.github.io/compat-table/es6   查看js支持情况
    解码器：traceur 、babel
    shim和polyfill 、css polyfill
  9.2 ES6编程风格【上】
    （1）const、let
      const：常量（不能被赋值=，但可以加东西push），建议使用
      优点：可以提醒大家 不能被改变
      比较符合函数式编程
      本质的区别：编译器内部处理机制不同
    （2）对象解构
      {a,b} = a
    （3）字符串模版
      // 不用使用+连接字符串
      const s = "hello"
      const e = "world"
      const c = `foor ${a} ${b} bar`
      function test(strs,...values){
        console.log(values); // ["hello","world"]
        console.log(strs);   // ["foor","","bar"]
      }
      startswith（开始检测）、 endsWith（结尾检测）、includes（是否包括）
    （4）对象和数组
      const s = "12"
      const test = [6,...s]  //[6, "1", "2"]
      const k = "arr"
      array.from():把类似数组的字符串转换成数组
      ["","",...s]
      const result={[k+1]:1,s,test} // {arr1: 1, s: "12", test: [6, "1", "2"]}
      // 对象中添加属性
      const s={}
      object.assign(a,{x:3})
      //对象其他
      object.is(nan,nan)：是否相等
      object.create:创建对象原型链的副本
      object.setprototypeof(sunday,drink) //设置原型链
      let sunday = {__proto__:对象名}      //设置原型链
      // 继承
      let sunday = {__proto__:对象名，getdrink(){return super.getdrink + "coffi"}}
    （5）函数
      const fn = function pp(){}
      console.log(fn.name) // pp
      // 箭头函数
      const result = [1,2,3].map((index)=>index*3)
      console.log(result) //[3,6,9]
      // 函数的参数
      function test(a=1,{opteions=true}={}){console.log(options)}
      test(30,{options:111}) //111
      // 变形为
      function test(...result){console.log(result)} //[30,{options:111}]
  9.3 ES6编程风格【中】
    (1)iterator 遍历器(解决异步变成同步) 现在用的不多
      function* a(){yield "";} a.next()
    (2)generator
      for in 遍历索引   for of遍历
    (3)class
       class Person{
        constructor(age){this.age = age}
        tell(){console.log(`年龄是${this.age}`)}
       }
       class Man extends Person{
        constructor(age){super(age);this.arr=[];}
        set menu(data){this.arr.push(data);}
        get menu(){return this.arr}
        tell(){super.tell();console.log(`hello`)}
        static init(){console.log("static")}
       }
       Man.init();   // static
       const xiaoming = new Man(30);
       xiaoming.menu = "aaa";
       console.log(xiaoming.menu);   //["aaa"] 
    (4)set\map
      //set
      let arr = new Set("123")
      arr.add("4")
      arr.add("4")
      arr.delete("2")  // 删除数据
      arr.clear() // 清空数据
      console.log(arr); //{"1", "2", "3", "4"}
      console.log(arr.size); //4
      console.log(arr.has("1")); //true
      允许使用for of遍历
      //map 键值对形式
      let food = new Map();
      let fruit = {},cook = funcion(){};
      food.set(fruit,"a")
      food.set(cook,"b")
      console.log(food.get(fruit)) //a
      console.log(food.size) //2
      food.delete(fruit)
      food.clear()
    (5)module
      export 函数名
      import {a,b} from "j" 或者import * as data from "j" 
      export default 函数名
      import j from "j"
  9.4 ES6编程风格【下】
    async await： 
10 专题一.JavaScript语言新发展【深度实践课】
  10.1 JavaScript与QA工程师
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
  10.2 JavaScript语言精粹1
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
  10.3 JavaScript语言精髓2
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
    （9）
  10.4 ES6在企业中的应用
  10.5 TypeScript前世今生
