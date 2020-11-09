### 在严格模式下运行脚本，不少导致提醒buggy行为的事情会抛出错误，例如
* 1.  未声明的变量赋值抛出ReferenceError，而不是创建一个全局变量
* 2. 不止一次对对象字面量分配相同的属性会抛出SyntaxError
* 3. 使用with语句抛出SyntaxError
