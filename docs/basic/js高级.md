## typeof
* 可以比较：undefined, string,number,boolern
* object (数组、null都是object)
* function 函数 
## 类型转换
* 强制： parseInt、parseFloat，toString
* 隐式： 逻辑转换、==、 ‘+’、if
## promise的三种状态
状态：Pending，Resolved，Rejected。
特性：
只有异步才能改变状态。
resolved：走then
rejected：走catch
then走完，不报错，状态变为resolved
catch走完，不报错，状态变为resolved
* 基础： https://www.cnblogs.com/maoli-demo/articles/14001217.html
* 进阶： https://www.cnblogs.com/maoli-demo/articles/13842120.html
#### 宏任务和微任务
* 微任务：promise，async，await
* 宏任务：setTimeout，setInterval，ajax，DOM事件。
微任务 是ES6规定的规范。如promise
宏任务 是W3C（webAPI）定的规范。如setTimeout
* <img src="/../media/micro.awebp" style="zoom: 70%" />
  
#### 事件轮训如上图 （与DOM事件的关系，与DOM渲染的关系）
<img src="/../media/eventloop.awebp" style="zoom: 60%" />

* 微任务队列 micro task queue 与 回调callback Queue 存放的是webAPI。
* DOM click事件也会立即放到 webAPI，等触发的时候执行。

###### DOM渲染和js共用一个进程。DOM渲染指的是页面上能看到元素为止。也许js节点长度是3，但DOM还未渲染。过程：
* call stack执行完毕后（同步代码执行完毕后，DOM操作是同步）
* 先执行微任务队列，再
* 尝试DOM渲染，最后，
* 执行eventLoop（callback queue）
#### 跨域
1，原因：同源策略：ip，端口，协议三者必须一致。
2，方案：
    后端头部设置CORS
    ng
    jsonp（script标签可以绕过同源策略，后端可以返回任意符合的拼接内容）
八，this
this的取值，取决于使用的时候，而不是定义的时候。
1，计时器中的使用（指向window，不是调用的对象）
2，class中的使用（实例）
3，箭头函数的使用（箭头函数所在的作用域）
4，call，apply，bind中的使用
5，全局下的this
九，闭包
0，即函数定义和函数表达式位于另一个函数的函数体内。
而且，这些内部函数可以访问它们所在的外部函数中声明的所有局部变量、参数和声明的其他内部函数。
** 当其中一个这样的内部函数在包含它们的外部函数之外被调用时，就会形成闭包。所以并不是函数套函数。
1，闭包是函数作用域的特殊应用：函数作为返回值、函数作为参数。
2，闭包内的变量在函数执行完会保存在内存中。
3，场景：防抖，节流、react-hook、composition API。
// 作为返回值
function fn() {
  const a = 100 
  return function() {
    console.log(a)
  }
}
const a = 200
const fx = fn()
fx()

// 作为参数
function print(fn) {
  const b = 400
  fn()
}
const b = 300
function fw() {
  console.log(b)
}
print(fw)//  自由变量的查找，是在函数定义的地方往上查找，不是在函数执行的地方 ！！！
十，call，apply，bind
1，改变this指向。bind返回新函数。call，apply立即调用
2，apply()方法 接收两个参数，一个是函数运行的作用域（this），另一个是参数数组。
3，call()方法 第一个参数和apply()方法的一样，但是传递给函数的参数必须列举出来。
十一，Http
协议常用：http1.1 / http2（必须在https的安全证书下使用）
状态码：
1XX 服务器接收到请求
2XX 请求成功 eg：200
3XX 重定向   301 永久重定向 ；302 临时重定向
4XX 客户端错误 404
5XX 服务端错误 500，504网关超时。

methods：get、post、patch、put、delete

Headers：
req headers：
1，connection：keep-alive （长链接，短链接）
2，cookie
3，user-Agent：携带浏览器信息
4，Content-Type：application / json 请求数据格式
5，Accept: //浏览器可接收的数据格式
6，Accept-Encoding: //传输压缩，浏览器可接收的压缩算法，如gzip
7，Accept-Languange: //浏览器可接收的语言。如zh-ZN

res headers
1，Content-Type：返回的数据格式
2，set-cookie
3，content-Length：返回的数据大小
4，content-encoding：返回数据的压缩算法
（缓存相关）
Etag：资源的唯一标识
Cache-control：资源失效日期
LastModified：资源最后被修改的时间。
十三，数组API：纯函数与非纯函数
1，纯函数不改变原数组：concat，map，filter
slice（）：函数的截取
2，非纯函数：push，pop，shift，unshift，
splice（）
十四，map
题目：[10,
20,30].map(parseInt) 
//解构 - parseInt API 的规则
[10,20,30].map( (item , index) => {
    return parseInt(item,index)
} )
十五、Object.create()
Object.create() : 可以给对象指定原型。
const a = {age: 24} // 等同 new Object()
const b = Object.create(a)
b.__proto__ === a // true

### 原型，原型链
1，原型对象 包括显示原型 prototype 和 隐式原型__proto__（指向clss的显示原型）。    
每个class 都有显示原型。每个实例都有隐式原型。（class只是语法糖，本质上是Function）
2， 实例查找自身属性或者方法时，如果没找到，会不断的向上一级的原型对象查找，这个过程形成原型链。
3，实例可以通过原型链共享原型对象上的方法。继承的本质
```js
class People {}
class Student extends People {}
const xialuo = new Student()
// Student.prototype.__proto__ == People.prototype 
//instance 就是基于原型链实现的，在原型链上的对象都为true


 String.prototype.__proto__ === Object.prototype
// 因为： String.prototype : chatAt， indexOf....
// 所以：'abc'.indexOf()
```
### hasOwnProperty
why?
### 设计模式
设计模式，通常是先有设计，再有模式。模式都是遵循设计原则。
比如：开放封闭原则、单一职责原则。
* 工厂模式
    描述：就是通过new关键字，不断实例化一个个产品。
    场景：jq的$符实现原理
* 单例模式
    描述：系统中被唯一使用，只实例化（new）一次。
    场景：前端使用较少。
* 适配器模式
    描述：为旧接口提供中间转换器，以适应新功能。旧的已不满足使用
    场景1：老旧系统中的jq，在弃用的时候，使用axios替代.
    场景2: vue中的computed属性，当旧有的data不满足需求。
* 装饰器模式
    描述：装饰原有的方法，保留原有功能。
    场景：ts就提供了装饰器。vue2.0为了使用ts，vue-property-decorator，提供了很多装饰器
* 代理模式
    描述：通过代理的方式，访问另一个对象。
    场景：ES6的Proxy
* 观察者模式
    描述：一对多的关系，所有依赖的都将改变。发布和订阅。
    场景1：vue中的watch，或生命周期。
    场景2: Promise的多个then连接

## 异步加载js脚本的方式有哪些
* script标签加 async 或者 defer
    defer：等页面在内存中全部渲染结束，（DOM结构生成，其他js脚本执行完毕）加载。
        但是在window.onload前执行。
        多个defer会按顺序加载。
    async：一旦加载完该js，页面会中断渲染，等该js执行完毕，再继续渲染。
        多个async，不会按顺序执行

* 动态生成script标签。
* 异步ajax加载js文件。
## 防抖debounce
介绍：用于频繁操作，频繁触发的场景。如keyup事件，监听input输入框的change事件。
（等操作结束后，再触发回调）
代码。
## 节流throttle
介绍：用于频繁操作的场景。如鼠标拖拽，scroll事件。频繁操作可以指定触发的间隔。
代码。


## 装饰器

