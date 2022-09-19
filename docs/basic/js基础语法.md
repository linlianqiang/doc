# 基础语法


## 数组

### filter
 是过滤器，可以return符合条件的集合集合。无匹配则返回空数组 []
### find
 是返回满足条件的第一个值，无则undefind
### map 
  * 必须return原数组长度的内容
  * map不会修改原数组。前提是不修改对象的值（引用类型）。
### foreach
可以有相对复杂操作。 return 不会得到一个数组结果



## 前端模块化

* https://juejin.cn/post/6844903576309858318

### CommonJS

* 语法：exports、require。 node语法中使用

  ```js
  module.exports = {}
  ```

### AMD

* AMD规范采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。这里介绍用require.js实现AMD规范的模块化：用`require.config()`指定引用路径等，用`define()`定义模块，用`require()`加载模块。
* AMD规范在2010由requireJS提出，CommonJS规范主要是弥补服务端的模块化机制，不像服务器加载速度很快，客户端加载时需要等待，可能存在假死情况

### CMD

CMD规范在2011年由seaJS提出，CMD规范和AMD规范类似，主要区别是CMD规范是就近加载依赖，延迟执行，只有到require时依赖才执行。

### ES6 Module

export 、export

## Object.create()

可以给对象指定原型? 指定的是隐式原型。
```js
  const a = {age: 24} // 等同 new Object()
  const b = Object.create(a)
  b.__proto__ === a // true
```

