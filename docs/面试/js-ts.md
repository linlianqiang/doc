## js

A、js
一，var 与let、const的区别
1，var存在变量提升，let，const没有
    console.log(a) //undefined . 如果是let报错。
    var a = 100; 
    等价：
    var a ;
    console.log(a)
    a = 100;

2，var、let定义变量，const定义常量
3，let，const有块级作用域。var没有。
    for(var i = 0; i < 2; i++) {..}
    console.log(var) //有值
二，typeof能比较哪些类型
1，undefined, string,number,boolern
2, object (数组、null都是object)
3，function 函数 
三，强制类型转换和隐式类型转换
1，parseInt、parseFloat，toString
2，逻辑转换、==、 ‘+’、if
四，promise的三种状态
状态：Pending，Resolved，Rejected。  看面试题！
特性：
只有异步才能改变状态。
resolved：走then
rejected：走catch
then走完，不报错，状态变为resolved
catch走完，不报错，状态变为resolved
五，宏任务和微任务
1，微任务：promise，async，await
2，宏任务：setTimeout，setInterval，ajax，DOM事件。
微任务 是ES6规定的规范。如promise
宏任务 是W3C（webAPI）定的规范。如setTimeout




六，事件轮训如上图 （与DOM事件的关系，与DOM渲染的关系）
1，微任务队列 micro task queue 与 回调callback Queue 存放的是webAPI。
3，DOM click事件也会立即放到 webAPI，等触发的时候执行。

DOM渲染和js共用一个进程。
DOM渲染指的是页面上能看到元素为止。也许js节点长度是3，但DOM还未渲染。过程：
1，call stack执行完毕后（同步代码执行完毕后，DOM操作是同步）
1.1，先执行微任务队列，再
2，尝试DOM渲染，最后，
3，执行eventLoop（callback queue）
七，跨域
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
十六、原型，原型链
1，原型对象 包括显示原型 prototype 和 隐式原型__proto__（指向clss的显示原型）。    
每个class 都有显示原型。每个实例都有隐式原型。（class只是语法糖，本质上是Function）
2， 实例查找自身属性或者方法时，如果没找到，会不断的向上一级的原型对象查找，这个过程形成原型链。
3，实例可以通过原型链共享原型对象上的方法。继承的本质
class People {}
class Student extends People {}
const xialuo = new Student()
// Student.prototype.__proto__ == People.prototype 
//instance 就是基于原型链实现的，在原型链上的对象都为true


十七、设计模式
设计模式，通常是先有设计，再有模式。模式都是遵循设计原则。
比如：开放封闭原则、单一职责原则。
1，工厂模式
    描述：就是通过new关键字，不断实例化一个个产品。
    场景：jq的$符实现原理
2，单例模式
    描述：系统中被唯一使用，只实例化（new）一次。
    场景：前端使用较少。
3，适配器模式
    描述：为旧接口提供中间转换器，以适应新功能。旧的已不满足使用
    场景1：老旧系统中的jq，在弃用的时候，使用axios替代.
    场景2: vue中的computed属性，当旧有的data不满足需求。
4，装饰器模式
    描述：装饰原有的方法，保留原有功能。
    场景：ts就提供了装饰器。vue2.0为了使用ts，vue-property-decorator，提供了很多装饰器
5，代理模式
    描述：通过代理的方式，访问另一个对象。
    场景：ES6的Proxy
6，观察者模式
    描述：一对多的关系，所有依赖的都将改变。发布和订阅。
    场景1：vue中的watch，或生命周期。
    场景2: Promise的多个then连接
十八、typescript
十九、异步加载js脚本的方式有哪些
1，script标签加 async 或者 defer
    defer：等页面在内存中全部渲染结束，（DOM结构生成，其他js脚本执行完毕）加载。
        但是在window.onload前执行。
        多个defer会按顺序加载。
    async：一旦加载完该js，页面会中断渲染，等该js执行完毕，再继续渲染。
        多个async，不会按顺序执行

2，动态生成script标签。
3，异步ajax加载js文件。
二十、防抖debounce
介绍：用于频繁操作，频繁触发的场景。如keyup事件，监听input输入框的change事件。
（等操作结束后，再触发回调）
代码。
二十一、节流throttle
介绍：用于频繁操作的场景。如鼠标拖拽，scroll事件。频繁操作可以指定触发的间隔。
代码。
二十二、常用es6
从如下几个点去回答（回答还是要体现出高级）
1，变量：const，let的区别
2，数据类型：Set，Map（快速查找二维数组）
3，操作数据的API：比如数组：map。filter，includes，keys
4，函数：参数可以传默认值，箭头函数（写法上更简介、没有arguments参数、this指向定义的地方，
不是被调用的时候，不能用作构造函数、不能使用new关键字）
5，异步：Promise，async，await
6，class
B、html、css
一，BFC
概念：
0，首先BFC指的是Block Fomatting Context，块级格式化上下文。是盒模型box的一种类型。
1，盒模型是css布局的基本单位，页面是有若干个盒模型组合成的。盒模型还有其他类型：
    IFC（inline formatter context），FFC（flex formatter context），GFC（grid...）
BFC的规则：
1，一块独立的区域，不影响外界。
2，BFC内部：margin重叠
形成条件：overflow：hidden。absolute、fixed。
运用场景：清浮动、块元素纵向边距重叠问题。
二，移动端解决方案
1，横向百分比，纵向rem。媒体查询做响应式会造成阶梯效果
2，vw，vh。视窗宽度。等分成100份。postcss.config.js可配置
三，inline-block的间隙问题
1，间隙：父级字体大小的 1/3.
2，解决方案：父级字体大小设置为0。
   标签写法合并。       
四，常用CSS3
border-radius
background-size,background-image,background-origin
渐变：grdient
阴影：box-shadow
flex-box
媒体查询
2d/3d：transform、translate、rotate，scale
C、性能优化
1，首屏优化方案
问题：加载慢，白屏久。

首先要知道指标：
1，First Content Paint (FCP) ，首次内容的绘制，让人知道这网站是否能用。控制在2秒（2-4）。
2，Largest Content Paint(LCP)，大内容的绘制，知道该网站的主要功能。控制在2.5秒（2.5-4）。
3, Time to Interective（TTI） 。可交互的时间。3.8秒（3.8-7.3）

其次是制定方案：
1，如果资源体积过大：
    a，资源压缩：在线压缩，webpack压缩
    b，传输压缩： gzip
    e，webpack的角度：代码拆分，tree shaking
    c，HTTP 2
    d，缓存
2，首页内容太多：
    a，懒加载
    b，SSR
    c, 骨架屏
3，加载顺序不合适：
    prefetch , preload
2, 回流与重绘
1，回流和重绘说的是浏览器的渲染。
2，通常浏览器的渲染路径是：js触发变化-style计算-layout布局-paint绘制-compositor复合。
（复合就是把dom分多层，互不影响，独立绘制，最终复合）
3，回流发生在layout过程，通常改变元素的大小或位置如offset，client，
    增加，删除节点，
    改变浏览器大小，
    会造成回流
4，重绘发生在paint过程，颜色background，透明度会造成重绘。
5，频繁回流和重绘，会造成页面卡顿抖动等问题。应尽量避免。
6，方案就是尽量进行复合，而不用回流和重绘
    用css3，放大，缩小。旋转等。
3，浏览器输入地址发生啥？
这个题目分为几个过程：一个是发生在浏览器的进程browser Process，一个是在页面中的渲染进程renderer Process
1，url分为几部分（协议，hostname,端口），DNS查找域名，得到IP。
2，设置UA浏览器信息，发送get请求，去服务端请求HTMl文本。
前端主要关注的还是页面的一个渲染过程：
3，边解析DOM，边加载子资源，遇到js将被阻塞。将文档构建成DomTree，将样式构建成CSSOM。

js触发DOm变化-style计算样式-layout布局树（将要在页面中画出来的，
集合了dom树和css树，如果是display：none，就不会出现在layout树中）-然后将layout绘制成图层树-最终将图层创建一个复合帧
渲染在页面中。这里就是一个浏览器的关键渲染路径，大概有5个步骤：
4，最终渲染页面。

网页渲染原理关键路径渲染
渲染两个模型：DOMTree，CSSOM，合成render tree（渲染树）

4，js是如何进行内存管理的，什么情况会造成内存泄漏？
1，变量创建，自动创建内存。不使用则自动释放。那如何确定不再需要使用的内存？
2，局部变量，如果没有闭包的引用，在函数执行完即释放。
4，全局变量在浏览器卸载页面时释放。
5，性能优化常见工具及指标
工具：
1，Google Devtool 2，lightHouse 3，webPageTest
指标：
RAIL测量模型：
1，处理事件，通常在50ms内
2，异步请求通常在1s内。如果没有就要loadding处理。
3，（loadding）加载要在5s内完成，并且可交互
关于首页：
3，First Content Paint  首次内容的出现，确保网站可用： 2秒。（2-4s）
4，Largest Content Paint(LCP)，大内容的绘制，知道该网站的主要功能。控制在2.5秒（2.5-4）。
5, Time to Interective（TTI） 。可交互的时间。3.8秒（3.8-7.3）
6，静态资源优化：
js，css，img：
0:图片可以转为base64，减少http请求
1，减少http请求
2，压缩资源。webpack：clean-css、html-minifier
图片：
jpg、png。
webP：google方案，比png更大大压缩比。ie兼容性
svg：移动端解决方案。比icon全部引入更好的方案。
iconFont
7，requestAnimationFrame 、 requestIdleCallback
备注：一帧的渲染周期： RAF - 解析HTML - style计算 - layout - paint - compositor- RIC
1，requestIdleCallback：在一帧16ms之后，剩余的时间内执行。（兼容性：ie，safari不兼容）
    在复合之后触发。--- 一帧之后执行
2，requestAnimationFrame 在layout之前触发。 ---   一帧之前执行。
3，react时间调度原理：利用 RAF 实现RIC：计算一帧剩余的时间。
8，如何优化资源的加载顺序
1，浏览器默认安排加载的优先级。
2，可以使用preload，prefetch调整优先级。
    eg：
    preload：提前加载较为重要，但是较晚出现的资源。
    <link ref = 'preload' href = './img/a.png' as = 'image'>
    prefetch：提前加载后面需要用到的资源，在空闲的时候。当前不太重要。
    需要用到的时候，直接从prefetch cache获取。
    <link ref= 'prefetch' href= './style.css' >
9，预渲染页面：react-snap
预渲染的作用：
1，大型单页应用的性能瓶颈：JS下载 + 解析 + 执行
2，SSR提升了 首次渲染，但是牺牲了TTFB的时间。实现复杂。
3，pre-rendering 预渲染 ，但是没有服务端的参与。
1, 将后序要加载的页面，提前加载到body中（eg：404，about）
2，
// package.json
“postbuilt”: "react-snap"
"reactSnap": {
    inlinecss: true
}
//main.js
const dom = document.getElementById('app')
if(app.hasChildNodes) {
    ReactDOM.hydrate(<App />, root)
} else {
    ReactDOM.render(<App/>,root)
 }
10, 电商首页列表优化：windowing
0，懒加载，上滑刷新。
1，只渲染视图中能见到的。
2，react：react-virtualized，react-window
小程序：recycle-view
vue：vue-virtual-scroll-list
原理：监听scroll事件，获取可视区域的起始和截止数据项。
11，使用骨架组件。防止布局抖动
1，骨架组件的作用就是占位：防止页面回流，布局移动。
2，提升用户体验，提前知道有内容在这。
3，react：react-placeholder
4，vue骨架屏方案：vue-content-placeholders
5，手动为每个页面写骨架屏
12，gzip 
资源传输方式 改变传输size的大小
nginx配置举例：（配置在http里）
gzip  on;
gzip_min_length 1k;
gzip_comp_level 6;
gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/xml text/javascript application/json;
gzip_static on;
gzip_vary on;
gzip_buffers 4 16k;
gzip_http_version 1.1;


13，keep-alive 。
持久的TCP连接。
什么是TCP连接：
为实现数据传输，在两个传输用户间建立的一种逻辑关系。有。。
http协议（应用层）　
　在HTTP/1.0中，默认使用的是短连接，浏览器和服务器每进行一次HTTP操作，就建立一次连接，但任务结束就中断连接。
　从 HTTP/1.1起，默认使用长连接，用以保持连接特性（keep-alive）。　　
  HTTP2: 多路复用（ MultPlexing）　　　　在https安全证书下，才能开启。　　
　单个连接，多次请求。http2一个域名只创建一次连接，而不是像http1.1那样建立6-8个连接。

1，nginx默认开启。在http里面配置
keepalive_timeout 65  //超时时间，超过65秒没用就关掉。0就不启用
keepalive_requests 100  //最多能发送100个请求。达到就关掉。
13.2 TCP
如何回答TCP相关内容？

1，TCP是传输层的协议，保证不同进程间的通信。还有UDP协议。
2，　
　http的长连接和短链接实际上 是TCP的长连接和短链接。　
　建立TCP连接，在客户端与服务端之间要建立三次连接。（三次握手）
  终止TCP连接，也需要客户端与服务端发送四次包，也就是4次挥手。　
　所以说每个连接都需要消耗资源和时间。
　tcp也有keep-alive作为tcp的连接机制。

14，Http缓存
缓存通常针对静态资源js，css、img缓存。
1，http缓存策略之 强制缓存 cache-Control：
    max-age：设置最大缓存过期时间
    no-cache：不需要强制缓存
    no-store: 不需要强制缓存，也不需要服务端缓存。比no-cache更彻底。

    Expires，也是设置缓存过期时间，被cache-control替代。
2，协商缓存（Last-modify 最后修改时间 ，Etag唯一标识）：
    服务端缓存策略，服务端判断资源是否改变，一致则返回304.否则返回200和最新的资源。

缓存流程：见图。
    1，首先看强制缓存是否过期。过期往下走
    2，然后看有无协商缓存。没有，则带信息直接请求。
    3，有协商缓存的话，带if-None-Match、if-Modified-Since请求。
    4，看是否返回304，或200新资源。

nginx配置（只针对当前网站，所以配置在location里）：

15，service workers
在客户端 和 服务端中间建立了一层 Service Worker（当然也是在客户端，缓存从这里获取）。
离线支持
加速重复访问
webpack 提供两个包支持
** 只能在localhost 或者 https使用。
如果是create-react-app 直接提供了：
//main.js
serviceWorker.register()
16，HTTP2
1，开启http2，需要在https的环境下
2，本地可以设置自签名https，开发使用
3，然后，nginx 配置 证书，开启http2

优势：大型网站，请求量大
二进制传输 http1 是基于文本。
多路复用 MultiFlexing ，同时请求多个资源。减少请求量。
service push 服务器预先推送资源

D、其他
一，安全
1，server端：sql注入
2，客户端：登录注册密码加密：md5
3，前端：XSS攻击。npm install xss 修改script标签。
4，XSRF。购买链接（get），跨站请求伪造。方案：post请求，支付密码等。
二，理解前端工程化，组件化
前端工程化：当前前端已由 过去的webPage （一个页面，引些jq插件。。） 转向 webApp，业务逐渐复杂，是一个独立的工程。
因此会产生一些问题：
1，如何进行高效的多人协作。
2，如何保证项目的可维护性
3，如何降低项目的生产风险：打包，部署。

可以从如下四方面理解：
a，模块化，组件化，规范化，自动化。
模块化：JS模块化，css模块化
规范化：前后端分离，编码规范。工程目录的规范，组件的规范等。
自动化：图片的合并，代码的合并。测试，打包，部署。都有专门工具来完成。
组件化：组件就是将一段UI样式和其对应的功能作为独立的整体去看待，为了增加复用性，灵活性，提高系统设计，
从而提高开发效率。而不仅仅是自以为的抽象，引用。

一个通用的，可扩展性高的组件，必然是有非常合理的命名的，类似list,data,content,name,key,callback,className等名词，绝对不会出现我们系统中的业务名词。
这些名词和任一产品和应用都无关，它与自身抽象的组件有关，只表明组件内部的数据含义，偶尔也会代表其结构，所以只有这样，才能让用户通用。
我们在组件化时，也需要遵循这种设计原则，库往往是想让广大开发者通用，而我们可以降低scope，做到在整个app内通用即可。好的组件化必然有好的设计思维和用户体验。


## ts

