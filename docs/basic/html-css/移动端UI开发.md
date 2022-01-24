## 相关概念

屏幕分辨率（px）, 尺寸相同，分辨率越高，字号越小。一个像素占一个格子。2*2的像素，占4个格子。

css像素 就是 逻辑像素。

iphone 6 : 物理像素是 750。逻辑像素是375。dpr = 2;

* iPhone Xs Max 和 iPone XR：

  * CSS像素是414 * 896；

  * 实际渲染的物理像素是1242 * 2688； iPhone Xs Max是3倍屏。

  * 每个css像素对应9个物理像素。

*  物理像素（设备像素）dp：设备不能改变的，一生产出来就确定的。一张图 300 * 300，说的是物理像素。

*  逻辑像素（设备独立像素）dip，可时刻改变的。规定在电子设备上呈现的图片等，采用逻辑像素表示。

   （一台设备，出厂时规定好逻辑像素比。dpr = 2，将物理像素放大了一倍）

* **dpr ( device pixel ratio)**：设备像素比，即设备物理像素与逻辑像素(css像素)的比例。

  ```js
  window.devicePixelRatio
  ```


* 物理像素：

* 逻辑像素：

* 移动端视口概念（pc的视口是浏览器窗口区域）：

  * visual viewport 视觉视口：移动设备屏幕的区域（window.innerWidth）

  * layout viewport 布局视口（document.documentElement.clientWidth）。网页布局的基准窗口，在pc上就是浏览器大小，手机上会有默认值980px，保证pc的网页能在手机上呈现，但是很小。
  * ideal viewport 理想视口 ( screen.width )。网站页面在移动端展示的理想大小。使页面的宽度跟设备宽度一致

```
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
width=device-width：表示让 布局视口 的宽度等于设备宽度（视觉视口）；
```

* rem（相对html）

  <img src="G:\doc\media\rem.awebp" alt="img" style="zoom:60%;float: left" />