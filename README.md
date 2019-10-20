# javascript 高级

1. `object.defineProperty` 属性

```js
Object.defineProperty(obj,'num', {
    value: '中华',
    writable: false, // 只读属性，默认是false
    enumerable: false, // 是否可枚举，如果值为false,则不允许遍历
    configurable: false, // 如果值是false,则不允许删除这个属性，默认值为false
})
```

## 函数的定义方式

1. 自定义函数（命名函数）

```js
function fn() {
    // code
}
```

2. 函数表达式（匿名函数）

```js
var fn = function () {
    // code
}
```

3. 利用 new 构造函数定义参数

```js
var fn = new Function() {
    // code
}

```

## 函数的调用方法

1. 普通函数

```js
// 在普通函数中，`this` 指向的是window对象
function fn() {
    console.log('普通函数' + this)
}

fn()  fn().call()

```
2. 对象的方法

```js
// 在对象函数中，`this` 指向的是`object` 对象
var o = {
    hello: function() {
       console.log('对象方法' + this)
    }
}

o.hello(); // 调用方法

```
3. 构造函数

```js
// 这里的是构造函数，构造函数的首字母大写
// 在构造函数中，`this` 指向的是引用当前实例的对象，原型对象里面的`this` 也是当前引用实例的对象
function Hello() {
    console.log('构造函数+' + this)
}
new Hello() // 构造函数的调用方法

```
4. 绑定事件函数

```js
// 绑定事件函数 `this`指向的是函数的调用者
btn.onClick = function () {
    // 点击了按钮就可以调用这个函数
    console.log('绑定事件函数' + this)
}

```
5. 定时器函数

```js
// 定时器函数，`this` 指向的是window 对象
setInterval(function() {
    // 这个函数是定时器自动一秒钟调用一次
    console.log('定时器函数' + this)
}, 1000)

```
6. 立即执行函数

```js
// 立即执行函数，`this` 指向的是window对象
(function() {
    // 这个立即执行函数，不需要调用，自己就会自动执行
    console.log('立即执行函数' + this)
})()

```

## this 的指向问题

 函数内的`this` 指向，是当我们调用函数的时候确定的，调用当时的不同决定了`this` 的指向不同，一般指向我们的调用者


调用方式 | this 指向 |
---------|----------|
 普通函数调用 | window |
 构造函数调用 | 实例对象，原型对象里面的方法也指向实例对象 | 
 对象方法调用 | 该方法所属对象 | 
 事件绑定调用 | 绑定事件对象 | 
 定时器函数   | window | 
 立即执行函数 | window | 

 ## 改变函数内部`this` 指向

 `javascript` 为我们专门提供了一些函数方法来帮我们更优雅的处理函数内部`this`的指向问题，常用的有`bind()`、`call()`、`apply()` 三种方法

 1. `call()` 

```js
 
 var o = {
     name: '当燃'
 }

 function fn(a, b) {
     console.log(this)
     console.log(a + b)
 }

 fn.call(0, 1, 2) 
//  call 第一个可以调用函数，第二个可以改变函数内的this指向
```

2. `apply` 方法

`apply()` 方法调用一个函数，简单理解为调用函数的方式，


```js
apply(this, [paramArray])
// 其中第一个参数表示的是需要改变this指向的函数或者方法，第二个参数表示的是传递的参数，参数必须是以数组的形式


var o = {
    name: '当燃'
}

function fn() {
    console.log(this)
}

fn.apply(o) // 最终控制台输出的是 object
```

## `bind` 方法

`bind()` 方法不会调用函数，但是能改变函数内部`this` 指向

```js

fun.bind(thisArg, arg1, arg2)

// thisArg： 在函数内部运行时指定的this的值
// arg1，arg2 ：传递的其他参数
// 返回由指定的this值和初始参数改造的原函数拷贝

var o = {
    name: '念沉'
}
function fn() {
    console.log(this);
}

var f = fn.bind(o);

f();

/*
    1.不会调用原来的函数，可以改变原来函数的内部的`this`指向
    2. 返回的是原函数改变this之后产生的新函数
*/

```

## call apply bind 总结

相同点：

都可以改变函数内部的this指向
 
区别点：

1. call 和 apply 会调用函数，并且函数内部this指向
2. call 和 apply 传递的参数不一样，call 传递参数arg1,arg2 形式，apply 必须数组形式 [arg]

主要应用场景：

1. call 经常做继承
2. apply 经常和数组有关系，比如借助于数学对象实现数组最大值和最小值
3. bind 不调用函数，但是还想改变this指向，不如改变定时器内部的this指向

## js 严格模式

1. js 开启严格模式

```js

"use strict "
// 开启严格模式的方法

// 此时只为function 开启严格模式
function fn() {
    'use strict'
}

function fun() {
    // 里面的还是按照普通的模式执行
}

```

2. 严格模式的变化

```js

// 1. 变量名必须先声明再使用
num = 10;
console.log(num) // 语法错误，变量需先声明后使用

// 2. 不能随意删除已声明的变量
delete num

// 3. 严格模式下this指向问题
// 以前在全局作用域函数中this指向window对象
// 严格模式下全局作用域中函数中this是undefined

function fn() {
    console.log(this);
}

// 4. 在严格模式下，如果构造函数不加new调用，this会报错

function Star() {
    this.sex = '女'
}

Star();

// 5. 定时器指向的this还是window 
setTimeout(function() {
    console.log(this);
})

// 6. 严格模式下函数里面的参数不允许有重名
function fn(a, a) {
    console.log( a + a)
}
```

## 高阶函数

> 高阶函数是对其他函数进行操作的函数，它接受函数作为参数或将函数作为返回值输出

```js
    // 1.接受函数作为参数
    function fn(callback) {
        callback && callback();
    }

    fn(function() {
      alert('i know you now have a good day')
    })

    // 2. 将函数作为返回值输出
    function fn() {
        return function () {

        }
    }
```

## 闭包

### 变量作用域

变量根据作用域的不同，分为两种：全局变量和局部变量

1. 在函数内部可以使用全局变量
2. 在函数外部不可以使用局部变量
3. 当函数执行完毕，本作用域内的局部变量会销毁

### 什么是闭包

> 闭包是有权访问另一个函数作用域中变量的函数

```js

function fn() {
    var num = 10;
    function fun() {
        console.log(num)
    }
    fun()
}

fn()

```

闭包的主要作用：延伸了变量的作用范围


## 浅拷贝

1. 浅拷贝只是拷贝一层，更深层次对象级别的只拷贝引用

方法一：

es6 提供了一个浅拷贝的方法，`Object.assign('拷贝给的对象', '拷贝的对象')`

```js
var o = {};
var man = {
    name: '沉年',
    age: '20'
}

Object.assign(o,man)

```

方法二：使用`for` 循环的方式

```js

var o = {}
var obj = {
    name: '念沉',
    age: '20'
}

for(var k in obj) {
    // 其中 k 是属性名，obj是属性值
    o[k] = obj[k]
}

console.log(o)
```


2. 深拷贝拷贝多层，每一级别的数据都会拷贝

```js
var obj = {
    id: 1,
    name: '念沉',
    msg: {
        age: 18
    }
}

```
