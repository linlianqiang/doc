## 1. 背景

网页的加载快慢与哪些因素有关系？

* 用户本身的宽带有关系
* 用户自身的电脑（内存，cpu）自身有关系
* 网站服务器有关系（cdn）
* 网页资源的下载及资源渲染
* ...

结论：

* 如果CPU，内存占用很低，网页依然打开缓慢。可排除自身电脑的因素。
* 网页是基于http（TCP：三次又三次）发起请求，服务器响应资源，如果宽带慢或出现问题，在请求网页资源时，浏览器得不到响应（>3s），那么浏览器会认为他之前发的请求被丢了。会重发请求。所以宽带肯定有影响。
* 性能优化没有最佳结果，每一次的数据有可能受宽带等因素的影响。所以性能是不断持续优化的过程，我们要做的是把能做好的那部分做好。

## 2. web性能指标

* speed Index （lighthouse提供）：页面的速度指数：4s
* 交互的响应：1s / 60 帧（帧数（FPS）：浏览器不动时，为0）
* 首次内容出现的时间：first contentFull paint
* 网页的某个内容出现时间：1s（不是指每个请求的资源）。
* 服务端的处理（TTFB）：
* 网页加载完成并可交互（time to interactive）：5s
* 动画：10ms/1帧

有些指标是某些模型（工具）提出来的（比如：speed Index），并没有具体的含义，其背后有复杂的计算逻辑。可作为一个参考值。

## 3. web性能检测工具

### chrome devtool

<img src="F:\doc\local_doc\web_docs\media\devtool-network.png" alt="指标" style="zoom:80%;" />

* requests ：请求数
* resources：请求资源大小
* DOMContentLoaded ( $(document).ready() )：dom下载时间
* Load( window.onload )： 页面资源（图片，js，css..）下载时间

<img src="G:\思维\local_doc\web_docs\media\chrome_devtool_2.png" alt="指标" style="zoom:60%;" />

资源时间表及持续时间：

* queueing：排队时间
* stalled：被挂起（如果请求一直在pending...，可查看chrome网络日志）
* DNS Lookup：DNS查找
* Initial connection： 建立链接（TCP）
* SSL（https）SSL协商
* Request sent：请求发送
* Waiting（TTFB）：后端响应资源的时间（后台处理能力）、网络回路
* Content Download：网站资源下载

<img src="G:\思维\local_doc\web_docs\media\chrome_devtool_3.png" alt="img" style="zoom:70%;" />





## nginx

## webpack 构建优化

