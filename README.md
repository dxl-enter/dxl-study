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
    
    
    
  9.4 ES6编程风格【下】
10 专题一.JavaScript语言新发展【深度实践课】
