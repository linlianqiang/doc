## 渐变 gradients

可以在两个或多个指定的颜色之间平稳的过渡。CSS3定义了两种类型的渐变：

* 线性渐变：Linear Gradients。以线条的形式，从左到右或从上到下

* 径向渐变：Radial Gradients。以中心点的方式进行发散

  <img src="..\media\渐变.png" alt="gradient" style="zoom:60%;float:left" />

### 线性渐变

* 创建线性渐变，必须定义至少两个色标。还可以设置起点和方向，或者角度以及渐变效果

```css
// 语法
background-image: linear-gradient(direction, color-stop1, color-stop2, ...);

// 从上到下
background-image: linear-gradient(red, yellow);
// 从左到右
background-image: linear-gradient(to right, red , yellow);
// 对角线
background-image: linear-gradient(to bottom right, red, yellow);
// 使用角度
```

* 使用角度。如果希望对渐变角度做更多的控制，您可以定义一个角度，来取代预定义的方向（向下、向上、向右、向左、向右下等等）。值 0deg 等于向上（to top）。值 90deg 等于向右（to right）。值 180deg 等于向下（to bottom）。

```css
// 语法
background-image: linear-gradient(angle, color-stop1, color-stop2);
background-image: linear-gradient(-90deg, red, yellow);

```

* 多个色标、透明度

  ```css
  background-image: linear-gradient(to right, red,orange,yellow,green,blue,indigo,violet); 
  background-image: linear-gradient(to right, rgba(255,0,0,0), rgba(255,0,0,1));
  ```

* 重复线性渐变：repeating-linear-gradient()

  ```css
  background-image: repeating-linear-gradient(red, yellow 10%, green 20%);
  ```

  

### 径向渐变

至少需要两个色标。默认地，*shape* 为椭圆形，*size* 为最远角，*position* 为中心。

```css
// 语法
// shape 参数定义形状。它可接受 circle 或 ellipse 值。默认值为 ellipse（椭圆）。
background-image: radial-gradient(shape size at position, start-color, ..., last-color);

// 均匀间隔的色标
background-image: radial-gradient(red, yellow, green);

// 不同间距的色标
background-image: radial-gradient(red 5%, yellow 15%, green 60%);

// 不同size
// closest-side
// farthest-side
// closest-corner
// farthest-corner
background-image: radial-gradient(closest-side at 60% 55%, red, yellow, black);

// 重复径向渐变
background-image: repeating-radial-gradient(red, yellow 10%, green 15%);
```

## 2D

### transform

单词是改变的意思，改变元素本身的性质

```css
// 先将坐标系旋转45度，再沿着新的坐标平移200px.
transform: rotate(45deg) translate(200px, 0);
```

其实，当旋转`45`度后，元素的整个坐标系都旋转了`45`度，如下图：

<img src="https://images.cnblogs.com/cnblogs_com/xljzlw/676183/o_QQ%e6%88%aa%e5%9b%be20151115171530.png" alt="img" style="zoom:50%;float:left;" />

```css
#red {
		background:red;
		transform: rotate(45deg) translate(100px, 100px);
	}
	#green {
		background:green;
		transform: translate(100px, 100px) rotate(45deg);
	}
```



<img src="https://images.cnblogs.com/cnblogs_com/xljzlw/676183/o_QQ%e6%88%aa%e5%9b%be20151115173609.png" alt="img" style="zoom:60%;float:left;" />



图中可以看到，值的顺序对元素位置的影响。通过上面的介绍知道，红框先旋转再平移，即先旋转坐标系再平移，而绿框先按正常的坐标系平移，再旋转，所以它们的位置就不同了。

我们可以举一反三，比如`3d`旋转等都可以按上面的方法去分析

#### translate 平移

从当前位置移动元素（x轴 和 y轴的参数）

```css
transform: translate(50px, 100px)
```

#### rotate 旋转

顺时针或逆时针旋转

```css
transform: rotate(20deg)
```

#### scale 缩放

根据给定的宽度和高度参数

* scaleX：缩放宽度。
* scaleY：缩放高度。

```css
// 宽两部，高三倍
transform: scale(2, 3)
transform: scaleX(0.5)
transform: scaleY(3)
```

#### skew 倾斜

* skewX：延X轴方向

* skewY ：延Y轴方向

```css
// 延X轴方向，逆时针 30
transform: skewX(30deg);
// 延Y轴方向，顺时针 30
transform: skewY(20deg);
```

分析：transform:skewX(30deg);表示元素沿x轴方向逆时针倾斜30°。如果把30°改为-30°，则元素会沿x轴方向顺时针倾斜30°，此时预览效果如下图所示。

![img](http://api.lvyestudy.com/upload/articles/889834f1c4d94fcbe3225292.png)

实际上，transform:skewX(30deg);其实可以等价于transform:skew(30deg, 0);，小伙伴们可以自行测试一下。此外在实际开发中，如果忘了究竟什么时候顺时针倾斜，什么时候逆时针倾斜，只需要稍微写一小段代码测试一下就知道了。

对于初学者来说，可能一时半会看不出skewX()方法是怎么一回事。其实skewX()方法的变形原理是这样的：由于元素限定了高度为100px，而skewX()方法是沿着x轴方向倾斜的。因此只要倾斜角度不超过180°，元素都会保持100px的高度，同时为了保持倾斜，元素只能沿着x轴方向拉长本身。

#### matrix 集合

```css
matrix(scaleX(),skewY(),skewX(),scaleY(),translateX(),translateY())
transform: matrix(1, -0.3, 0, 1, 0, 0);
```

### transform-origin 

允许改变转换元素的位置（原点）-- 以哪个为中心点进行转换。

* 2D 转换元素能够改变元素 x 和 y 轴。3D 转换元素还能改变其 Z 轴。

* 默认值：50% 50% 0

  ```css
  transform-origin: x-axis y-axis z-axis;
  // x-axis的取值：left、center、right、length、%
  // y-axis的取值：top、center，bottom，length，%
  // z-axis的取值：length
  ```

  

## 3D

同样是通过transform方法。3D是将2D的属性添加上X，Y，Z属性。

##### 圆点 transform-origin

（同上）

##### 旋转

* rotateX() - 绕X轴旋转给定角度
* rotateY() - 绕Y轴旋转给定 角度
* rotateZ() - 绕Z轴旋转给定角度
* rotate3d(*x*,*y*,*z*,*angle*)

##### 缩放

* scaleX(*x*)
* scaleY(*y*)
* scaleZ(*z*)
* scale3d(*x*,*y*,*z*)

##### 平移

* translateX(*x*)
* translateY(*y*)
* translateZ(*z*)
* translate3d(*x*,*y*,*z*)

##### transform-style

规定如何在3D空间中呈现被嵌套的元素。必须与transform一同使用。

##### perspective 

规定3D元素的透视效果

##### perspective-origin

 规定3D元素的底部位置

##### backface-visibilty 

定义元素在不面对屏幕时是否可见



## 过渡 transition

单词本意过渡，属性值到属性值的过渡。css过渡，允许你在给定的时间内平滑地改变属性值。

要创建过渡需明确两件事：

* 需要添加效果的CSS属性
* 效果的持续时间

#### transition-delay

延迟

#### transition-duration

总时长

#### transition-property

过渡属性

#### transition-timing-function

指定过渡的速度曲线

* ease：缓慢开始，加速，缓慢结束
* linear：匀速
* ease-in：缓慢开始
* ease-out: 缓慢结束

* ease-in-out：开始和结束较慢
* cubic-bezier(*n*,*n*,*n*,*n*) 在 cubic-bezier 函数中自己的值。可能的值是从 0 到 1 的数值。

```css
div {
  width: 100px;
  height: 100px;
  background: red;
  transition-property: width;
  transition-duration: 2s;
  transition-timing-function: linear;
  transition-delay: 1s;
    // transition: width 2s linear 1s, height 4s;
}
div:hover {
  width: 300px;
}
// 当光标从元素上移开时，它将逐渐变回其原始样式。
```



## 动画 animation

##### @keyframes 

词意是关键帧。规定动画模式。0% 是动画的开始时间，100% 动画的结束时间。为了获得最佳的浏览器支持，应该始终定义 0% 和 100% 选择器。

* 前面的值代表时间。如果是匀速，就要配合属性。0-50%是匀速。50%-100%是匀速。但是整体并非匀速。

```css
// from {
    //   background-color: red;
    // }
// to {
    //   background-color: yellow;
    // }
0% {
    width: 50px;
    background-color: red;
}
50% {
    width: 80px;
    background-color: yellow;
}
100% {
    width: 1800px;
    background-color: green;
}
```

##### animation-delay

延迟

##### animation-direction

规定动画是向前播放，向后播放还是交替播放。

* normal 默认值。向前正常播放
* alternate： 动画应该轮流反向播放。

##### animation-duration

一个周期应该花费的时间

##### animation-fill-mode

规定元素在不播放动画时的样式（在开始前，结束后，或两者同时）。

* none：不改变默认行为
* forwards：动画完成后，保持最后一个属性（在最后一个关键帧中定义）
* backwards：在 animation-delay 所指定的一段时间内，在动画显示之前，应用开始属性值（在第一个关键帧中定义）。
* both：forwards & backwards

##### animation-iteration-count

规定动画应播放的次数

* n： 次数
* infinite：无限播放

##### animation-name

规定 @keyframes 动画的名称

##### animation-play-state

规定动画是运行还是暂停。结合js使用。

*  paused / running

```css
.stop {
    animation-play-state: paused;
  }
```



##### animation-timing-function

规定动画的速度曲线。同过渡的动画曲线一致。

```css
// p

.ani-wrap {
    width: 100px;
    height: 100px;
    background:red;
  }
  // .ani-wrap,
  .ani {
    animation-name: example;
    animation-duration: 4s;
    animation-delay: 0s;
    animation-fill-mode: forwards;
    animation-timing-function: linear;
    animation-direction: alternate;
    animation-iteration-count: infinite;
  }
  .stop {
    animation-play-state: paused;
  }
```

