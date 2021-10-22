## 6.额外的数组
```
forEach
var sum = "";
[1,2,3,4].forEach(function(item,index,array){
  console.log("数组项",item,"索引"); // true
  sum += item;
});
// 对于古董浏览器，如IE6-IE8

if(typeof Array.prototype.forEach != "function"){
  Array.prototype.forEach = funcion(){ //实现 }
}
```

```
map
// map处理数组中的所有值并返回处理后的值，不影响原数组，返回结果为新的数组
var users = [
  {name:"张含韵",email:"zhang@email.com"},
  {name:"江一眼",email:"jiang@email.com"},
  {name:"李小璐",email:"li@email.com"}
];
var emails = users.map(function(user){ return user.email;});
console.log(emails);
```

```
filter
// filter 数组元素过滤，把返回true的汇集成新的数组，返回结果为新的数组
// 筛选出zhang开头的邮件
filter(function(email){return /^zhang/.test(email);});
```

```
// some找到数组中第一哥符合要求的值后就不再继续执行
// 用来判断数组中是否存在符合要求的值，返回结果true｜false
// function 返回类型为bool
some
var scores = [5,8,3,10];
var current = 7;
function higherThanCurrent(score){
  return score > current;
}
if(scores.some(higherThanCurrent)){
  alert("我批准了");
}
```

```
every
// every匹配每一个元素，直到有一个返回false为止
// function 返回类型为布尔
if(scores.every(higherThanCurrent)){
  alert("朕准了");
}else{
  alert("来人，拖出去斩了！");
}
```

```
indexOf
var data = [2,5,7,3,5];
console.log(data.indexOf(5,"x")); // 1("x"被忽略)
console.log(data.indexOf(5,"3")); // 4（从3号位开始搜索）

lastIndexOf
var data = [2,5,7,3,5];
console.log(data.lastIndexOf(5)); // 4
console.log(data.lastIndexOf(5,3)); // 1(从后往前，索引值小于3的开始搜索)
```

```
reduce
var matrix = [
  [1,2],
  [3,4],
  [5,6]
];
// 二维数组扁平化
var flatten = matrix.reduce(function(previous,current){
  return previous.concat(current);
});
```

```
TypeArray
它是一种通用的固定长度缓冲区类型，允许读取缓冲区中 的二进制数据

```

## 7. ES6 Map 与 Set
* Set 对象
+ Set 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。
* Set 中的特殊值
+ Set 对象存储的值总是唯一的，所以需要判断两个值是否恒等。有几个特殊值需要特殊对待：
+ +0 与 -0 在存储判断唯一性的时候是恒等的，所以不重复；
+ undefined 与 undefined 是恒等的，所以不重复；
+ NaN 与 NaN 是不恒等的，但是在 Set 中只能存一个，不重复。

* Set 对象作用
```
数组去重
var mySet = new Set([1, 2, 3, 4, 4]);
[...mySet]; // [1, 2, 3, 4]
```

```
并集
var a = new Set([1, 2, 3]);
var b = new Set([4, 3, 2]);
var union = new Set([...a, ...b]); // {1, 2, 3, 4}
```

```
交集
var a = new Set([1, 2, 3]);
var b = new Set([4, 3, 2]);
var intersect = new Set([...a].filter(x => b.has(x))); // {2, 3}
```

```
差集
var a = new Set([1, 2, 3]);
var b = new Set([4, 3, 2]);
var difference = new Set([...a].filter(x => !b.has(x))); // {1}
```

