### Flexbox 的优点：

1，更好的性能优化方案

2，容器有能力决定子元素的大小，排序，对齐方式，间隔等。

### html：

```css
<div class="flex-box">
            <div class="flex-item flex-item1">flex item1</div>
            <div class="flex-item flex-item2">flex-item2</div>
            <div class="flex-item flex-item3">flex-item3</div>
            <div class="flex-item flex-item4">flex-item4</div>
          </div>
```

### css：

```css
  .flex-box {
    width: 800px;
    display: flex;              // 弹性伸缩盒。父级为块
    display: inline-flex;    // 内联块级弹性伸缩盒。父级为内联块

    // flex-direction： 子元素在父容器中的位置 
    // flex-direction: row;             // 左对齐（默认）
    // flex-direction: row-reverse;     // 右对齐
    // flex-direction: column;          // 纵向，子元素块级展示
    // flex-direction: column-reverse;  // 纵向倒序

    // flex-wrap：子元素超出父容器时，是否换行
    // flex-wrap: nowrap;               // 不换行。子元素自动缩小
    // flex-wrap: wrap;                 // 换行
    // flex-wrap: wrap-reverse;         // 反转 wrap 排列

    // 复合属性
    // flex-flow: row nowrap;           // flex-direction  flex-wrap

    // justify-content:   子元素在主轴（横轴，主轴也有可能是竖轴）方向上的对齐方式
    // justify-content: flex-start;     // 左对齐
    // justify-content: flex-end;       // 右对齐
    // justify-content: center;         // 居中
    // justify-content: space-between;  // 空隙居中
    // justify-content: space-around;   // 均分，两端保留子元素与子元素之间间距大小的一半

    // align-items：    单个子元素在 纵轴方向上的对齐方式。并不是多个元素的垂直（块）对齐方式       
    // align-items: flex-start;         // 上对齐
    // align-items: flex-end;           // 下对齐
    // align-items: stretch;            // 如果侧轴大小为'auto'，则其值会使项目的边距盒的尺寸接近所在行的尺寸，同时会遵照'min/max-width/height'限制
    // align-items: baseline;           // 如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐
    // align-items: center;             // 居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）

    // align-content:     子元素堆叠伸缩 行  的对齐方式。横轴方向。
    //  flex-start | flex-end | center | space-between | space-around | stretch
  }
  .flex-item {
    // margin: 10px;
    // width: 100px;


    // order: 1;                          // 整数值来定义排列顺序
    // flex-grow: 1;                      // 扩展比例。默认 0
    // flex-shrink: 1;                    // 收缩比例。默认 1。超出的部分，按比例进行消化。没有超出父级则无效
    // flex-basis: 2;                     // 伸缩基准值。可设置子元素基准宽度，其他剩余均分，配合flex-grow。默认 auto。不允许负值。 可设置px，百分比。
    // flex：none                         // 复合属性
    // flex:  flex-grow  flex-shrink   flex-basis  0 1 100px
    // align-self:                        // 子元素自身在侧轴（纵轴）方向上的对齐方式。单个。属性值同上 align-items
  }
```

