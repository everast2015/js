# javascript 基础知识

浏览器分为两部分：渲染引擎 + JS引擎

* 渲染引擎：用来解析HTML+CSS，俗称内核，比如 Chrome 浏览器的blink，老版本的webkit
* js引擎：也称为 JS解析器，用来读取网页中的javascript代码，对其处理后运行，比如chrom 浏览器的v8

浏览器本身不会执行js代码，而是通过内置的js引擎来执行js代码，js引擎执行代码时，逐行解释每一句源码（转为机器语言），然后由计算机去执行，所以js语言归为脚本语言，会逐行解析执行。

## 变量概述

> 本质：变量是程序在内存中申请的一块用来存放数据的空间

### 变量的使用

1. 变量的声明
```js
var age; // 声明一个名称为age的变量
```
- var 是一个关键字，用来声明变量（variable变量的意思），使用该关键字声明变量之后，计算机自动为变量分配内存空间，不需要程序员管

- age是程序员定义的变量名，我们通过变量名来访问内存中分配的空间
2. 赋值

```js
var age = 18; // 把后面的值赋给变量

```

3. 变量的初始化

```js
var age = 18; // 在声明一个变量并赋值，称为变量的初始化

```

4. 只声明未赋值，值为undefined

```js

var age; // 只声明不赋值，最终的输出结果是undefined

```

5. 不声明，不赋值，会直接报错的

```js

console.log(address) // tel is defined; 报错了

```

6. 不声明，直接赋值

```js

age = 18;

console.log(age) // 可以拿到值，但是是全局变量的值
```

### 变量的命名规范

- 有字母、数字、下换线、和美元符号组成，如：username,num01,uername_,_name,$name
- 严格区分大小写，如 var app 和 var App 是两个不同的变量
- 不能以数字开头，18age 是错误的
- 不能是关键字和保留字，如 var / for/ while
- 变量名必须有意义 var username, nl -> age
- 遵循驼峰命名，首字母大写，后面单词的首字母需大写，例如：myFirstName

## 数据类型

由于，JavaScript是一种弱类型的语言，或者说是动态语言，这意味着不用提前声明变量的类型，在程序运行过程中，类型会被自动确定

```js

var age = 10 ; // 这是一个数字型
var name = 'China' // 这是一个字符串

```

在代码运行时，变量的数据类型是由JS引擎 根据 = 右边变量的数据类型来判断的，运行完毕之后，变量就确实了数据类型

### 数据类型的分类

js把数据类型分为两类：
- 简单数据类型 （string,number,boolean,null,undefined）
- 复杂数据类型 （Object)


简单数据类型 | 说明 | 默认值
---------|----------|---------
 Number | 数字型，包含整型值和浮点型值，如21，0.21 | 0
 Boolean | 布尔值类型，如true或false 等价于1和0 | false
 String | 字符串类型，如张三，注意，咱们js里面都带引号 | ""
 Undefined | var a;声明了变量a但是没有给值，此时 a = undefined | undefined
 Null | var a = null ; 声明了变量a为空值 | null

 ### 数字型 number

现阶段：在js中八进制前面加0，十六进制前面加0x

```js
isNaN()
// 用来判断一个变量是否为非数字的类型，返回true或false

```
![图片链接地址](https://github.com/everest2015/js/blob/master/img/number.png)

### 字符串 string

因为html里面的标签使用的是双引号，JS这里我们更推荐使用单引号

### 获取字符串的长度

```js

var name = 'today you are so nice'

console.log(name.length) // 可以打印出字符串中的长度

```

### 字符串的拼接

多个字符串之间可以使用 + 号进行拼接

拼接前会与字符串相加的任何类型转成字符串，在拼接成一个新的字符串

字符相接 + 数字相加

### 构造函数

构造函数通过原型分配的函数是所有对象所共享的

Javascript 规定，每一个构造函数都有一个prototype 属性，指向一个对象，注意这个prototype 就是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有。

我们可以把那些不变的方法，直接定义在prototype 对象上，这样所有对象的实例就可以共享这些方法

问答？

1. 原型是什么？

一个对象，我们也称为prototype 为原型对象

2. 原型的作用是什么？

共享方法

3. 我们为什么需要把方法放到原型上？

构造函数，每一次调用这个方法就开辟一条内存空间，这样很耗内存

因为每个构造函数中，都有一个prototype 属性，这个属性对象中所有属性和方法，都会被构造函数所拥有，我们都方法都放在构造函数中，主要的作用就是为了共享方法

## 构造函数和原型

对象都会有一个属性 __proto__ 指向构造函数的prototype 原型对象，之所以我们对象可以使用构造函数prototype原型对象的属性和方法，就是因为对象有__proto__ 原型的存在

__proto__ 对象原型和原型对象prototype 是等价的

__proto__ 对象原型的意义就在于对象的查找机制提供了一个方向，或者说一条路线，但是它是一个非标准属性，因此实际开发中，不可以使用这个属性，它只是内部指向原型对象prototype

```js
// 创建一个构造函数
function Star(uname,age) {
    this.uname = uname;
    this.age = age;
}

Star.prototype.sing = function() {
    console.log('我会写字')
}

// 调用方法
var ldh = new Star('刘德华', 18)
var zxy = new Star('张学友', 18)

console.log(Star.prototype) // 原型对象
console.log(ldh.__proto__) // 对象原型
```

![原型对象关系图](https://github.com/everest2015/js/blob/master/img/object.png)

## constructor 构造函数

对象原型`__proto__` 和构造函数(prototype) 里面都有一个属性 `constructor` 属性，`constructor` 我们称为构造函数，因为它指会构造函数本身

`constructor` 主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数

## 构造函数、实例、原型对象三者之间的关系

![原型对象关系图](https://github.com/everest2015/js/blob/master/img/relations.png)

## 构造函数，原型，原型链

```js

function Star(uname,age) {
    this.uname = uname;
    this.age = age;
}

Star.prototype.sing = function() {
    console.log('我会唱歌')
}

var ldh = new Star('刘德华', 18)
// 1、只要是对象就有 __proto__ 原型，指向原型对象
console.log(Star.prototype);
console.log(Star.prototype.__proto__ === Object.prototype)

// 2、我们Star原型对象里面的__proto__ 原型指向的是 Object.prototype

console.log(Object.prototype.__proto__) // 最终的结果是空的 null

```
![原型链关系图](https://github.com/everest2015/js/blob/master/img/prototype.png)

## 原型对象 this 指向
```js
function Demo(name) {
    this.name = name
}
demo.prototype.draw = function() {
    console.log('i like english')
}

var draw = new Demo('i like apple')
```
1. 在构造函数中，里面的this指向的是对象实例ldh
2. 原型对象函数里面的this，指向的是实例对象 ldh

## 继承

### call()

调用这个函数，并且修改函数运行时的this 指向

```js

fun.call(thisArg, arg1,arg2)

// thisArg 当前调用函数this的指向对象
// arg1,arg2 传递的其他参数

```

1. call() 可以调用函数

```js

function fn() {
    console.log('学习使我快乐')
}

fn.call() // 打印的是：学习使我快乐
```

2. 可以改变this的指向

```js
var o = {
    name: 'everast'
}

function fn() {
    console.log('学习使我快乐')
}

fn.call(o) // 改变 this 的指向，此时这个函数的this，就指向了o这个对象
```

## 构造函数总结


构造函数 | 构造函数的特点 | 
---------|----------|
 1 | 构造函数有原型对象prototype | 
 2 | 构造函数原型对象 prototype 里面有constructor 指向构造函数本身 | 
 3 | 构造函数可以通过原型对象添加方法 | 
 4 | 构造函数创建的实例对象有__proto__ 原型指向，构造函数的原型对象
 

 ## 类 

 es6通过类实现面向对象编程

```js

class Study {
    // code
}
 
console.log(typeof Study) // function
```
1. 类的本质其实就是一个函数，我们也可以简单的认为，类就是构造函数另一种写法
2. 类有原型对象prototype

```js
class demo{

}

console.log(demo.prototype) // 类有一个原型对象 prototype 指向的是原型对象的本身 construstor

console.log(demo.prototype.construstor == class demo {}) // 指向的是类的本身

```
语法糖的概念：

语法糖就是一种便捷写法，简单理解，有两种方法可以实现同样的功能，但是一种写法更加清晰，方便，那么这个方法就是语法糖

## ES5中新增方法

数组方法
   1. foreach()
   
```js
   let demo = [1,2,3,4,5,6]
   demo.forEach(function(val) {
       console.log(val * 2) // 2，4，6，8，10 输出的结果
   })
   // demo输出的结果：1，2，3，4，5
   // 最后的结论：foreach 不会改变原有数组的值
```
   2. map()
   3. filter()
    
   ```js
   // filter 表示查找到满足条件的元素，返回的是一个数组，而已是把所有满足条件的元素返回回来
   ```

   4. some()
    ```js
    // some 也是查找满足条件的元素是否存在，返回的是一个布尔值，如果查找到第一个满足条件的元素就终止循环
    ```
   5. every()

- 字符串方法

- 对象方法

1. `Object.defineProperty(Obj, prop, descriptor)` 定义对象中新属性或修改原有属性

- obj 必须，目标对象
- prop 必须，需定义或修改属性的名字
- descriptor 目标属性所拥有的特性

```js

var obj = {
    name: 'demo',
    age: 18,
    price: 1000
}

// 以前添加属性的方法
obj.num = 1000
obj.number = 1000

// 使用ES5中新增的方法

Object.defineProperty(obj, username, {
    value: '蛰伏',// 定义的具体的值
    writable: false, // 不可以重写这个属性
    enumerable: false, // 是否可枚举，表示的意思是该属性是否可遍历
    configurable: false, // 目标属性是否可以被删除或再次修改
})

```

2. `Object.keys()` 用于获取对象自身所有的属性

```js
Object.keys(); // 获取自身所有的属性，返回一个由属性名组成的数组

```

## 函数

1. 函数的定义方式

- 函数声明方式 function 关键字 （命名函数）
```js
function fn() {
    // code
}
```
- 函数表达式 （匿名函数）

```js
var fun = function() {
    // code
}
```
- 利用 new Function('参数1','参数2','参数3')

```js

var f = new Function();

// 调用的方式
f()
```
- 所有函数都是Function的实例（对象）
- 函数也属于对象

## 函数的调用方式

1. 普通函数
```js
function fn() {
    // code 
}
// 调用方法
fn(), fn.call(); // 两种方法都可以调用

```
2. 对象的方法
```js
var o = {
    demo: function() {
        // code
    }
}

// 调用的方法

```
3. 构造函数
```js
function Star() {
    // code
}
new Star(); // 调用方法

var demo = new Star(); // 构造函数中，this指向的是 demo这个实例对象
demo.prototype.sing = function() {
    // 原型对象里面的this，指向的也是 demo 这个实例对象
}
```
4. 绑定事件函数
```js
btn.onclick = function() {
    // 绑定事件函数，this指向的是函数的调用者，btn这个函数
    console.log('绑定事件函数的this：' + this)
}

```
5. 定时器函数
```js
window.setInterval(function() {
    // 定时器函数中的this，指向的是window
    console.log('定时器函数' + this)
}, 1000) // 这个定时器函数是每隔一秒钟自动调用一次
```

6. 立即执行函数
```js
(function() {
    // 立即执行函数是自动调用
    console.log('立即执行函数this的指向：' + this)
})()
```

## 函数中this执行的是谁

this的指向 | 说明 | 
---------|----------|
 普通函数中 | this 指向的是window | 
 对象的方法 | this 指向的是对象o | 
 构造函数中 | this 指向的是当前调用的实例对象 |
 绑定事件函数 | this指向的是btn这个按钮对象，当前调用的这个函数
 定时器函数 | this 指向的是window
 立即执行函数 | this 指向的是 window

 函数内this的指向，是当我们调用函数的时候确定的，调用方式的不同决定了this的指向不同，一般指向的是我们的调用者

 调用方式 | this指向 | 
---------|----------|
 普通函数调用 | window | 
 对象的方法 | 该方法所属对象 | 
 构造函数调用 | 实例对象 原型对象里面的方法也指向实例对象 |
 绑定事件函数 | 绑定事件对象
 定时器函数 | window
 立即执行函数 | window

 ## 改变函数内部this 指向

 Javascript 为我们提供了一些函数方法帮我们更优雅的处理函数内部this的指向问题，常用的有bind()/call()/apply() 方法

 1. call() 方法

 call() 方法调用一个对象，简单理解为调用函数的方式，但是它可以改变函数的this指向

```js

fun.call(thisArg, arg1, arg2)

var o = {
    name: 'everast'
}
function fn() {
    // code
    console.log('调用这个函数')
}
 
fn.call() // 调用这个函数，作用一
fn.call(o) // 改变this的指向，this的指向目前是o
```
2. apply() 方法

apply() 方法调用一个函数，简单理解为调用函数的方式，但是它可以改变函数的this指向

```js
fun.apply(thisArg, [argsArray])
```
- thisArg：在fun 函数运行时指定的this值
- argsArray：传递的值，必须包含在数组里面
- 返回值就是函数的返回值，因为它就是调用函数

```js

var o = {
    name: 'everast'
}

function fn() {
    console.log('this的指向问题' + this)
}

fn.apply(o, ['everast'])

// 1. 也是调用函数，第二个可以改变函数内部的this指向
// 2. 但是它的参数必须是数组，否则会报错的
// apply 的主要应用，比如我们可以应用apply借助于数学内置对象求最大值

var arr = [10,12,9,8,7,6,5,4]
var max= Math.max.apply(Math,arr); // 借助于数学对象求最大值
console.log(max)
```

3. bind() 方法
bind() 方法不会调用函数，但是能改变函数内部的this指向

```js
fun.bind(thisArg, arg1, arg2)

// 具体的用法
var o = {
    name: 'everast'
}

function fn() {
    console.log(this)
}

var f = fn.bind(o) // 不会调用函数，只能使用另一个方法来接收

console.log(f,'this的指向是哪个函数')

// 1. 不会调用原来的函数，可以改变原来函数内部的this指向
// 2. 返回的是原函数改变this之后产生的新函数
// 3. 如果有的函数不需要立即调用，但是又想改变这个函数内部的this指向
// 4. 我们有一个按钮，当我们点击之后，就禁用这个按钮，3秒钟之后开启这个按钮
```

* thisArg：在fun 函数运行时指定的this
* arg1, arg2 传递的其他参数
* 返回由指定的this值和初始化参数改造的原函数拷贝

需求：我们有一个按钮，当我们点击之后，就禁用这个按钮，3秒钟之后开启这个按钮

```js
var btn = document.querySelector('button');
btn.onclick = function() {
    this.disabled = true
    setTimeout((function() {
        this.disabled = false // 定时器中的this指向的是window的,使用bind()改变this的指向问题
    }.bind(this),3000)) // 这里的this指向的是btn这个方法的
}
```

## call(),apply(),bind() 总结

* 相同点：

都可以改变函数内部的this指向 

* 区别点：
1. call() 和 apply() 会调用函数，并且改变函数内部的this指向
2. call() 和 apply() 传递的参数不一样，call() 传递参数 arg1,arg2 形式，apply() 必须数组形式[arg]
3. bind() 不会调用函数，可以改变函数内部的this指向