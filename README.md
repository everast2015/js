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