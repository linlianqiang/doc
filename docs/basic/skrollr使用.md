## skrollr

####  注意事项

* 需要在onload之后，初始化。

* skrollr会自动html标签添加class="skrollr"并且会移除 class="no-skrollr"（如果存在的话）。

* 还会根据设备检测结果，给html标签添加class="skrollr-desktop"或者class="skrollr-mobile"以表明运行的平台

* skrollr会给关键帧添加 class ="skrollable-before" , class ="skrollable-between" 或者class ="skrollable-after" 。

  

#### 使用



```js
// 安装 npm install skrollr --save
// 使用：
import skrollr from 'skroll';
mounted() {
    this.skrollr = skrollr.init()
}
```

|  属性 | 值 | 描述 |
|  ----  | ----  |  ----  |
| smoothScrolling | boolean | 滚动条停止的时候动画是否停止，默认true， 不停止，存在过渡 |
|  |  |  |
| smoothScrollingDuration | 500 | 设置滚动条停止后，动画的过渡时间 单位ms |
| constants: { stepnum1: 100 } |  | 定义标签上的data-_stepnum1  变量 |
| forceHeight | boolean | 是否允许动画脚本改变页面高度，以便适配触发时机， 默认true 允许改变高度 |
| mobileDeceleration | 0.01 | 设置惯性参数，在移动设备上，通过这个参数，设置用户松开手指之后，滑动停止的有多块或者有多慢 |
| edgeStrategy | set / reset | 滚动条超过所定义的关键帧范围之外的时候，定义元素的状态 |
| render | function | 完成一次渲染的回调 |
| easing | 动画函数 |  |

```html
<div data-0="height:50px; bottom[WTF]:10%;" data-_stepnum1="height:100px; bottom[WTF]:50%;"></div>
```

##### 方法

```js
var s = skrollr.init();
s.getScrollTop()  		//获取当前的scrollTop
s.getMaxScrollTop()  	//获取最大scrollTop
s.isMobile() 			//返回是否运行在移动端
s.setScrollTop(100,force = true);  //到达设置的scrollTop, 如果设置force=true,那么没有动画，否则有动画（默认有动画）
//控制滚动条从当前位置移动到我们通过top设置的位置，而且是有过渡动画的
s.animateTo(100, {'duration': 500, "easing": 'linear', "done": function(){
    console.log("动画执行完毕");
}});
s.stopAnimateTo();  //停止上面提到的滚动条移动动画
s.on('beforerender',function(){  console.log("渲染页面之前"); })  // 页面渲染之前，执行函数
s.on('render',function(){ console.log("渲染页面之后");  });    // 页面渲染之后，执行函数
s.off('render');  //移除了render的事件侦听函数
```

###### 特性一：根据样式名后加特效名来指定过渡特效。

- begin
- end
- linear
- quadratic
- cubic
- swing
- sqrt
- outCubic
- bounce

```js
// 可以通过初始化实力时自定义过渡动画
skrollr.init({
        easing: {
            sin: function(p) {
                return (Math.sin(p * Math.PI * 2 - Math.PI/2) + 1) / 2;
            },
            cos: function(p) {
                return (Math.cos(p * Math.PI * 2 - Math.PI/2) + 1) / 2;
            },
        }
    });
```

###### 特性二：动画的禁用: 在样式前加！的方式来禁用动画了

```html
<div  data-0="background-image:!url(kitten1.jpg);" data-100="background-image:!url(kitten2.jpg)">
</div>
```

###### 特性三：相对滚动模式

滚动特效除了指定滚动固定的px之外，还有相对模式的概念，
相对模式即为相对与某个锚点进行特效的变化



```html
 --选择的元素
  data-anchor-target="#bacons" 
  --目标元素 顶部 在可视范围 底部 时的样式
  data-bottom-top="transform: translate3d(0px, -80%, 0px);" 
  --目标元素 底部 在可视范围 顶部 时的样式
  data-top-bottom="transform: translate3d(0px, 80%, 0px);"
```

