# JavaScript

JavaScript（简称“JS”） 是一种具有函数优先的轻量级，解释型或即时编译型的[编程语言](https://baike.baidu.com/item/编程语言/9845131)。虽然它是作为开发[Web](https://baike.baidu.com/item/Web/150564)页面的[脚本语言](https://baike.baidu.com/item/脚本语言/1379708)而出名，但是它也被用到了很多非[浏览器](https://baike.baidu.com/item/浏览器/213911)环境中，JavaScript 基于原型编程、多范式的动态脚本语言，并且支持[面向对象](https://baike.baidu.com/item/面向对象/2262089)、命令式、声明式、[函数](https://baike.baidu.com/item/函数/301912)式编程范式。

JavaScript在1995年由[Netscape](https://baike.baidu.com/item/Netscape/2778944)公司的Brendan Eich，在网景导航者浏览器上首次设计实现而成。因为Netscape与[Sun](https://baike.baidu.com/item/Sun/69463)合作，Netscape管理层希望它外观看起来像Java，因此取名为JavaScript。但实际上它的语法风格与[Self](https://baike.baidu.com/item/Self/4959923)及[Scheme](https://baike.baidu.com/item/Scheme/8379129)较为接近。

JavaScript的标准是[ECMAScript ](https://baike.baidu.com/item/ECMAScript /1889420)。截至 2012 年，所有浏览器都完整的支持ECMAScript 5.1，旧版本的浏览器至少支持ECMAScript 3 标准。2015年6月17日，ECMA国际组织发布了ECMAScript的第六版，该版本正式名称为 ECMAScript 2015，但通常被称为ECMAScript 6 或者ES2015。

**ECMAScript可以看作是JavaScript的一个标准。**

**一个合格的后端语言，必须精通JavaScript**



## JavaScript--HelloWorld

**依旧是两种方式，内部 js 代码以及外部 js 代码**

内部js：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        alert("HelloWorld01");
    </script>
</head>
<body>

</body>
</html>
```

![image-20210809211932600](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809211932600.png)

外部js：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="js/js01.js"></script>
</head>
<body>

</body>
</html>
```

```js
alert("HelloWorld02!")
```

![image-20210809212039041](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809212039041.png)

**ps：JavaScript引入的标签是一个双标签**



## 基本语法入门

**JavaScript严格区分大小写**

```js
//定义变量javascript与python相似，即定义的变量
//的类型随着变量的值确定
var i = 1;
var name = "jfc";
```

```js
// 条件控制

var score = 58;
if (score < 70 && score > 60){
    alert("D");
} else if (score > 70 && score < 80){
    alert("C");
}else if (score > 80 && score < 90){
    alert("B");
}else if (score > 90 && score < 100){
    alert("A")
}else if (score > 100 || score < 0){
    alert("出错了")
}else {
    alert("回家挨揍吧")
}
```

![image-20210809213520981](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809213520981.png)

利用浏览器的审查元素的控制台功能调试javascript代码。

![image-20210809213745888](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809213745888.png)



## 数据类型

![image-20210810104724349](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210810104724349.png)



JavaScript不区分小数和整数

数值类型：number

```js
123 //整数
123.1 //浮点数
1.123e4 //科学计数法
-99 //负数
-99.9 //浮点负数
NaN //Not a number 不是一个数字
Infinity //表示这个数字无限大
```

字符串：

```js
'abc'
"abc"
```

布尔值

```js
false
true
```

**精度问题：**

```js
console.log((1/3) === (1-2/3))
// false

console.log(Math.abs((1/3) === (1-2/3))<0.00000000000001)
// true
```

尽量避免使用浮点数运算，存在精度损失

**null与undefined**

null：空值

undefined：未定义的，未初始化的



**数组**

```js
var arr = [1,2,3,'a',"abc",null,true]
// 为了代码的可读性，尽量使用[]
new Array(1,2,3,'a',"abc",null,true)
```

**JavaScript中，如果数组越界，则会报undefined错**



**js对象**

```js
var person = {
    name:"jfc",
    age:18,
    arr:[1,2,3]
}
```

每个属性用逗号隔开，最后于一个属性不需要加逗号



## 运算符

逻辑运算符：

```bash
&& # 与，两者皆为真则为真

|| # 或，一者为真则为真

!  # 非，真即假，假即真
```



比较运算符

```bash
= # 赋值运算符
== # 比较运算符 等于（类型不一样，值一样，结果也为true）
=== # 比较运算符 绝对等于（类型一样，值一样，结果为true）
```

**坚持使用===**



```js
NaN === NaN //结果为false
isNaN(Nan) //结果为true
```

NaN与所有的数值都不想等，包括自己，只能用 isNaN来判断



## 变量

跟Java的变量定义相似，我们书写过程中，遵循Java的变量定义规则就可以。



## JavaScript的严格检查模式strict

一些书写的规则

1. 在ES6中，let定义局部变量
2. JavaScript尽量不要定义全局变量

```js
'use strict'
```

use strict 必须写在第一行，因为JavaScript的代码的随意性，导致一些莫名的问题，所以我们一般使用严格检查模式，遵循严格检查模式



## 数据类型详解



### 字符串类型

1. 正常的字符串使用 单引号、双引号 包裹

2. 注意转义字符：跟Java中的转义字符一致

3. 多行字符串编写

   ```js
   var msg = `hello
   你好
   wdnmd
   我带你们打
   `
   // tab键上面，esc下面
   ```

4. 字符串的拼接

   ```js
   // js中字符串的拼接遵循Java的规则，但是也会存在自己的规则
   var name = "jfc"
   var msg = `你好呀,${name}`
   ```

5. 简单的方法

   字符串的长度的获取与Java中一致

   ```js
   var arr = 'student'
   arr.length
   ```

   JavaScript中字符串也是不可变的

   大小写转换

   ```js
   // 大小写转换
   student.toUpperCase()
   student.toLowerCase()
   
   // 获取下标
   student.indexOf('')
   
   // 字符串的截取，与Java的语法一样
   student.substring(1,3)[1,3)
   ```

   

### 数组类型

**Array可以包含任意的类型**

```js
var arr = [1,2,3,4,5,6]

// 数组长度,如果给arr.length赋值，数组的长度则会改变
arr.length

// 获取下标索引
arr.indexOf('')

// 数组的截取，与string的substring一致
arr.slice()

// 给数组压入数值，弹出数值，都是在尾部操作
arr.push() // 压
arr.pop() // 弹出

// 给数组压入数值，弹出数值，在头部操作
arr.shift() // 弹出
arr.unshift() // 压入

// 数组的排序
arr.sort()

// 元素反转
arr.reverse()

// 数组的拼接，不会改变原来的数组，只是返回一个新的数组
arr.concat()

// 拼接数组，使用特定的字符拼接
arr.join('-')
```



**多维数组**

```js
arr[[1,2],[1,2]]
```



### 对象类型的详解

```js
var 对象名 = {
    属性名:属性值,
    属性名:属性值,
    属性名:属性值
    ......
}
```

**JavaScript中{......}表示一个对象，键值对描述属性：属性名：属性值，属性之间用逗号隔开，最后一个属性不需要逗号**

```js
var person = {
    name:'jfc'
}

// 对象属性的赋值
person.name = jfc

// 对象属性值的获取
person.name
> jfc
```

JavaScript中使用一个不存在的属性不会报错，只会输出 undefined



**动态增删属性**

```js
// 动态的删除属性
delete person.name

// 动态的增加属性直接给要增加的属性赋值就可以
person.age = 18
```



**判断属性是否在某个对象中：**

```js
// '属性名' in 对象名
'name' in person

// 继承寻找属性,JavaScript中可以找到父类的属性
'toString' in person

// 判断一个属性是否是自身的属性
person.hasOwnProperty('name')
```



## 流程控制详解

if 判断

```js
var score = 58;
if (score < 70 && score > 60){
    alert("D");
} else if (score > 70 && score < 80){
    alert("C");
}else if (score > 80 && score < 90){
    alert("B");
}else if (score > 90 && score < 100){
    alert("A")
}else if (score > 100 || score < 0){
    alert("出错了")
}else {
    alert("回家挨揍吧")
}
```

**循环**

where

```js
var age = 18
where (age < 30){
    age = age + 1;
    console.log(age)
}

var age = 18
do {
    age = age + 1;
    console.log(age)
} where (age < 30)
```

for

```js
var age = 18

for (let i = 0; i < 30; i ++){
    age = age + 1;
    console.log(age);
}
```

数组循环

```js
var arr = [1,2,3,4,5]

for (let k in arr){
    consloe.log(arr[k]);
}

for (let k of arr){
    consloe.log(k);
}
```

**for in 的k遍历到的是下标，for of 遍历的为数值**



## Map和Set集合

> ES6 的新特性

**Map**

```js
// 通过key获取value
var map = new Map([['jfc',80],['jsx',90]]);
var sc = map.get('jfc');
console.log(sc);

// 设置新增键值对
map.set('admin',123456);
```



**Set**

```js
var set = new Set([3,1,1,2,5,8])

// 获取set的值
set
> 3,1,2,5,8

// set是无序的，不重复的集合，所以会去掉重复的值

// set增加值
set.add(9)

// set 删除值
set.delete(1)

// 是否含有某个元素
set.has(3)
```



## 函数



### 定义函数

```js
// 绝对值函数
function abd(x){
    if (x < 0){
        return -x;
    }else{
        return x;
    }
}
```

一旦执行return 代表函数结束，返回结果。

如果没有执行return，函数也会执行返回结果，返回结果为NaN



```js
// 这是一种匿名函数，但是可以把值结果返回赋值给ads，通过abs就可以调用
var abs  = function(x){
    if (x < 0){
        return -x;
    }else{
        return x;
    }= function(x){
    if (x < 0){
        return -x;
    }else{
        return x;
    }
}
}
```

参数问题：JavaScript可以传递任意个参数，也可以不传递参数

JavaScript中的自定义异常

```js
var abs  = function(x){
    // 手动抛出异常
    if (typeof x != 'number'){
        throw 'Not a Number';
    }
    if (x < 0){
        return -x;
    }else{
        return x;
    }= function(x){
    if (x < 0){
        return -x;
    }else{
        return x;
    }
}
}
```



**arguments 代表传进来的参数是一个数组**

```js
function abd(x){
    // 获取全部的传入的参数
    for (let i = 0; i < arguments.length; i ++){
        console.log(arguments[i]);
    }
}
```

**rest 获取除了已经定义了的参数之外其他的参数**

```js
function abd(x,...rest){
    console.log(rest)
}
```

**rest 参数必须写在最后面，并且用 ... 标识**



### 变量的作用域

在JavaScript中变量是有作用域的

```js
function f() {
    var x = 0;
    x = x + 1
}

x = x + 2 // Uncaught ReferenceError: x is not defined
```

如果两个函数使用了相同的变量名，只要在函数的内部，则不冲突

```js
function f() {
    var x = 0;
    x = x + 1
}
function f1() {
    var x = 0;
    x = x + 1
}
```

内部函数可以使用外部函数的变量，反之不可以

```js
function f() {
    let x = 0;
    x = x + 1

    function f1() {
        let y = x + 1
    }
    let z = y + 1
} //Uncaught ReferenceError: z is not defined
```

在JavaScript中，函数查找变量从自身的函数开始，由 内 向 外 查找，假设在外部存在重名的变量，则会屏蔽外部的变量



```js
function f() {
    let x = 'x' + y;
    console.log(x)
    let y = 'y'
}
// 等价于
function f() {
    let y;
    let x = 'x' + y;
    console.log(x)
    y = 'y'
}
```

输出结果：xundefined

JavaScript会自动提升变量的声明，但是不会提升变量的赋值



**全局变量：**

```js
x = 1
function f(){
    console.log(x)
}
f()
console.log(x)
```



全局对象：window

```js
var x = 'xxx'

alert(x)
alert(window.x)

window.alert(x)
window.alert(window.x)
```

![image-20210811083004377](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811083004377.png)

JavaScript实际上只有一个全局的作用域，任何变量（函数也可以视为变量），假设没有在函数作用域范围内找到，就会向外查找，如果在全局作用域没有找到，报错 **RefrenceError**

> 规范

```js
// 唯一的全局变量
var jadan = {}

jadan.name = 'jfc'

jadan.add = function (a,b){
    return a + b;
}
```

由于JavaScript的所有的全局变量都绑定在 window 上，为了解决命名冲突，把自己的代码放入自己定义的唯一空间名字中，降低全局冲突的问题。



**局部作用域 let：**

```js
var age = 18

for (let i = 0; i < 30; i ++){
    age = age + 1;
    console.log(age);
}
consloe.log(i + 1) // ReferenceError: consloe is not defined
```

建议都是用let



**常量：**

ES6 之前，全部的大写字母定义的变量为常量，但是这个量可以被修改

```js
var PI = 3.14
console.log(PI)

PI = 123
console.log(PI)
```

ES6 引入了常量的关键字

```js
const PI = 3.14
console.log(PI)

PI = 123
console.log(PI) // Uncaught SyntaxError: missing ) after argument list
```



### 方法

```js
var jfc = {
    name:'jfc'
    age = 2000
    // 方法
    add = function(){
        let now = new Date().fetFullYear();
        return now - this.age;
    }
}
```

方法就是把函数放在对象里面，对象只有两个成员：属性和方法



```js
var jfc = {
    name:'jfc'
    age = 2000
    // 方法
    add = getAge;
}

function getAge(){
    let now = new Date().fetFullYear();
    return now - this.age;
}

jfc.age;
```

不可以直接调用getAge，this是无法指向的，默认指向调用它的对象



> apply

在JavaScript中可以控制this的指向

```js
// 代表getAge指向了jfc这个对象，参数为null
getAge.apply(jfc,[])
```



## 对象

> 标准对象

![image-20210811085920768](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811085920768.png)

### 日期和时间

```js
var now = new Date(); // 获取当前时间
now.getFullYear(); // 年
now.getMonth(); // 月
now.getDate(); // 日
now.getHours(); // 时
now.getMinutes();// 分
now.getSeconds(); // 秒
now.geDay(); // 星期几
now.getTime(); // 时间戳

new Date('时间戳') // 时间戳转当前时间

now.toLocaleString() // 时间的转换
now.toGMTString()
```



### JSON对象

[JSON](https://baike.baidu.com/item/JSON)([JavaScript](https://baike.baidu.com/item/JavaScript) Object Notation, JS 对象简谱) 是一种轻量级的数据交换格式。它基于 [ECMAScript](https://baike.baidu.com/item/ECMAScript) (欧洲计算机协会制定的js规范)的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。



**JSON和XML**

1. 可读性

JSON和[XML](https://baike.baidu.com/item/XML)的可读性可谓不相上下，一边是简易的语法，一边是规范的标签形式，很难分出胜负。

2. 可扩展性

XML天生有很好的扩展性，JSON当然也有，没有什么是XML可以扩展而JSON却不能扩展的。不过JSON在Javascript主场作战，可以存储Javascript复合对象，有着xml不可比拟的优势。

3. 编码难度

XML有丰富的[编码工具](https://baike.baidu.com/item/编码工具)，比如Dom4j、Dom、SAX等，JSON也有提供的工具。无工具的情况下，相信熟练的开发人员一样能很快的写出想要的xml文档和JSON[字符](https://baike.baidu.com/item/字符)串，不过，xml文档要多很多结构上的字符。

4. 解码难度

[XML](https://baike.baidu.com/item/XML)的解析方式有两种：

一是通过文档模型解析，也就是通过父标签索引出一组标记。例如：xmlData.getElementsByTagName("tagName")，但是这样是要在预先知道文档结构的情况下使用，无法进行通用的封装。

另外一种方法是遍历节点（document 以及 childNodes）。这个可以通过[递归](https://baike.baidu.com/item/递归)来实现，不过解析出来的数据仍旧是形式各异，往往也不能满足预先的要求。



**在JavaScript中一些皆为对象、任何JavaScript支持的类型都可以用JSON表示**

格式：

* 对象用{}
* 数组用[]
* 所有的键值对都是 key:value

```js
var user = {
    name : 'jfc',
    age : 18,
    sex : '男'
}

// 对象转字符串
var jn = JSON.stringify(user)
// {"name":"jfc","age":18,"sex":"男"}

// 字符串转对象
var a = JSON.parse('{"name":"jfc","age":18,"sex":"男"}')
// {name: "jfc", age: 18, sex: "男"}
// age: 18
// name: "jfc"
// sex: "男"
// [[Prototype]]: Object
```

JSON和JavaScript对象的区别

```js
// JSON 实质为一个字符串
var jn = '{"a":"hello","b":"world"}'

// JavaScript
var js = {a:"hello",b:"world"}
```



## 面向对象的编程

* 类：模板
* 对象：具体的实例

对于JavaScript来说，需要转变一下思想

```js
var Student = {
    name : 'jfc',
    age : 18,
    sex : '男',
    run:function () {
        console.log(this.name + 'running.....')
    }
}

var xiaoming = {
    name : 'xiaoming'
}
// 小明的原型为Student
xiaoming._proto_ = Student;
```



### 面向对象class继承

> class 继承，是在ES6引入

**对象**

```js
'use strict'
class Student {
    constructor(name) {
        this.name = name;
    }

    hello(){
        console.log('hello')
    }
}

var xiaoming = new Student('xiaoming')
```



**继承**

```js
'use strict'
class Student {
    constructor(name) {
        this.name = name;
    }

    hello(){
        console.log('hello')
    }
}

var xiaoming = new Student('xiaoming')


class xiaoStudent extends Student{
    constructor(name,grade) {
        super(name);
        this.grade = grade;
    }
    myGrade(){
        console.log("我是小学生")
    }
}
```



这个实现的原型还是上面的 _ photo _ 而且JavaScript的继承是一个链结构，被称为原型链

![image-20210811133457252](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811133457252.png)



## 操作BOM对象

B：浏览器对象模型

JavaScript的诞生就是为了能够早浏览器中运行

JavaScript中的window对象代表浏览器对象



![image-20210811150926375](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811150926375.png)

![image-20210811151143691](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811151143691.png)

> localtion
>
> 代表当前的页面的URL信息



> document 
>
> 代表当前面的页面



![image-20210811151448308](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811151448308.png)

获取具体的文档树节点，也可以直接获取cookie



> history 
>
> 代表浏览器的历史记录

![image-20210811151921123](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811151921123.png)



## 操作DOM树（核心重点）

**浏览器的网页从HTML代码以及结构来看，就是一个DOM树的结构**

* 添加：添加一个DOM树节点
* 删除：删除一个DOM树节点
* 更新：更新一个DOM树节点
* 遍历：得到DOM树节点



#### 获得DOM节点：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="css/style.css">
    <title>Title</title>
</head>
<body>
<script src="js/js.js"></script>

<div id="father">
    <p></p>
    <p class="p1"></p>
    <input type="text" name="i1">
</div>
</body>
</html>
```

```js
// 分别是，根据标签名，id，name，以及class获取DOM节点
var x1 = document.getElementsByTagName('p')
var x2 = document.getElementById('father')
var x2 = document.getElementsByName('i1')
var x3 = document.getElementsByClassName('p1')

// 获取他的所有的子节点
var ch = x2.children;
// 第一个以及最后一个子节点
var ch1 = x2.firstChild;
var ch1 = x2.lastChild;
// 获取某个节点的上一个节点
var p11 = p1.nextNode();
```



#### 更新DOM节点

```js
'use strict'

var id1 = document.getElementById('di1')

// 插入文本
id1.innerText = '802399'
// 插入标签
id1.innerHTML = '<strong>802399</strong>>'

// 操作css样式
id1.style.color = 'red'
```



#### 删除DOM节点

```js
// 分别是，根据标签名，id，name，以及class获取DOM节点
var x1 = document.getElementsByTagName('p')
var x2 = document.getElementById('father')
var x2 = document.getElementsByName('i1')
var x3 = document.getElementsByClassName('p1')

// 通过父节点删除子节点
x2.removeChild(x3)
```

```js
// 删除父节点下第一个子节点
x2.removeChild(x2.children[0])
```

**ps：删除节点时，节点是不断的在变化的，一定要注意这个变化**



#### 创建和插入DOM节点

**插入标签**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="css/style.css">
    <title>Title</title>
</head>
<body>
<p id="js">JavaScript</p>
<div id="list">
    <p id="p1">JavaEE</p>
    <p id="p2">JavaSE</p>
    <p id="p3">JavaME</p>
</div>
<script src="js/js.js"></script>  
</body>
</html>
```

```js
var js = document.getElementById('js');
var ls = document.getElementById('list');
ls.appendChild(js);
```



**创建标签：**

```js
var ls = document.getElementById('list');

var newp = document.createElement('p')
newp.innerText = "jfcniubi"

ls.appendChild(newp)
```

创建一个标签并插入

```js
var p1 = document.createElement('p');
p1.setAttribute('id','p5');
p1.innerText = "jfccccc"
ls.appendChild(p1);
```

利用 setAttribute 设置属性插入

```js
var p1 = document.createElement('p');
p1.setAttribute('id','p5');
p1.innerText = "jfccccc"
ls.appendChild(p1);

p1.style.backgroundColor = 'red'
```

设置css样式插入

![image-20210811192401516](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811192401516.png)

将某俄国节点插入到那个节点下面的某个子节点的前面

![image-20210811192703985](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811192703985.png)



## 操作表单

表单是 form 也是DOM树的节点

表单的目的：提交信息

获得表单的信息

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="css/style.css">
    <title>Title</title>
</head>
<body>
<form action="">
    <p>
        姓名：<input type="text" id="username">
    </p>
    <p>
        <input type="radio" value="boy" id="boy">男
        <input type="radio" value="girl" id="girl">女
    </p>
</form>
<script>
    var name = document.getElementById('username').value;
    alert(name)

    var radio1 = document.getElementById('boy').value;
    var radio2 = document.getElementById('girl').value;
    var radio3 = document.getElementsByTagName('input')[1].value;
    var radio4 = document.getElementsByTagName('input')[2].value;
    // 这样只能获得单选框或者多选框的值

    // 判断多选框或者单选框是否被选中
    var boo = radio1.checked;
    alert(boo)
</script>
</body>
</html>
```



### 提交表单验证即前端密码MD5加密

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="js/md5.js"></script>
</head>
<body>
<form action="https://www.baidu.com/" method="post" onsubmit="return f()">
    <p>
        账号：<input type="text" name="name" id="username">
        密码：<input type="password" name="password" id="password">
        <input type="hidden" id="md5password" name="md5password">
    </p>

    <button type="submit" id="sub">提交</button>

</form>

<script>
    function f() {
        let username = document.getElementById('username').value;
        let password = document.getElementById('password').value;
        let md5password = document.getElementById('md5password')

        md5password.value = hex_md5(password);
        alert(md5password.value)
        return true;
    }

</script>
</body>
</html>
```

