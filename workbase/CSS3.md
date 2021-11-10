## 渐变 gradients

可以在两个或多个指定的颜色之间平稳的过渡。CSS3定义了两种类型的渐变：

* 线性渐变：Linear Gradients。以线条的形式，从左到右或从上到下

* 径向渐变：Radial Gradients。以中心点的方式进行发散

  <img src="G:\doc\media\渐变.png" alt="gradient" style="zoom:60%;float:left" />

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

规定动画模式

##### animation-delay

延迟

##### animation-direction

规定动画是向前播放，向后播放还是交替播放

##### animation-duration

一个周期应该花费的时间

##### animation-fill-mode

规定元素在不播放动画时的样式（在开始前，结束后，或两者同时）

##### animation-iteration-count

规定动画应播放的次数

##### animation-name

规定 @keyframes 动画的名称

##### animation-play-state

规定动画是运行还是暂停

##### animation-timing-function

规定动画的速度曲线。同过渡的动画曲线一致。
