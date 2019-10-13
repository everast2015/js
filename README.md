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
