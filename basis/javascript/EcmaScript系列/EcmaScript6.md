# EcmaScript6新增语法
### 1. ES6简介与环境搭建
    kangax.github.io/compat-table/es6   查看js支持情况
    解码器：traceur 、babel
    shim和polyfill 、css polyfill
### 2. ES6编程风格【上】
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
### 3. ES6编程风格【中】
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
### 4. ES6编程风格【下】
    async await： 
    
### 5. ES6深度克隆
    (1)拷贝数据
      基本数据类型：拷贝后会生成一份新的数据，修改拷贝后的数据不会影响原数据
      对象/数组：拷贝后不会生成新的数据，而是拷贝的引用。修改拷贝后的数据会影响原来的数据
    (2)拷贝数据的方法
      1. 直接赋值给一个变量   // 浅拷贝
      2. Object.assign()    // 浅拷贝
      3. Array.prototype.concat() // 浅拷贝
      4. Array.prototype.slice()  // 浅拷贝
      5. JSON.parse(JSON.stringify())   // 深拷贝，拷贝的数据里不能有函数，处理不了（原因是JSON只能针对原生js的object和array数据）
