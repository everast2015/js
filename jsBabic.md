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

```