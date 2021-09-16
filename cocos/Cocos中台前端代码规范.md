## 1. 通用规范

### 1.1 命名

* 文件：一般文件（pages、views、utils...）采用小驼峰式命名。组件文件（components文件下）采用大驼峰命名。
* HTML：标签名、类名、标签属性统一用小写，单词之间统一使用中划线 “-” 连接。
* id 采用小驼峰式命名。
* 命名应直观反映用途，避免难以理解的缩写，如.font-weight或者.header-menu，不推荐.ft-wt或.hd-mn(抽象出的有合理注释的全局样式除外)

#### 1.1.1 js 命名

* 方法名、参数名、成员变量、局部变量都统一使用 【小驼峰】 命名。
* method中的方法必须是 动词+名词 的形式 如submitForm() getDetailInfo
* 常量命名全部大写，单词间用下划线隔开，力求语义表达完整清楚。 如MAX_PRODUCT_COUNT

### 1.2 注释

* 每一个文件（.vue文件、.js文件等），都该注释其功能、作者等。

    ```html
      <!--
      * @Descripttion: (对该文件的信息描述)
      * @Author: 
      --> 
      <template>
          ...
      </template>
      <script>
          ...
      </script>
    ```

## 2. html

### 2.1 代码规范

* 元素属性值使用双引号语法

* 元素属性值可以写上的都写上。如：

   ```html
   <input type="radio" name="name" checked="checked" >
   ```
* 元素嵌套规范：每个块状元素独立一行，内联元素可选
  
    ```html
    <div>
        <h1></h1>
        <p></p>
    </div>	
    <p><span></span><span></span></p>
    ```
### 2.2 注释规范
* 单行注释，独占一行。注释内容前后各一个空格字符
  
    ```html
    <!-- Comment Text -->
    <div>...</div>
    ```
* 模块注释，用于描述模块的名称以及模块开始与结束的位置
    ```html
    <!-- S Comment Text A -->   
    <div class="mod_a">
        ...
    </div>
    <!-- E Comment Text A -->
    ```
* 当模块注释内再出现模块注释的时候，为了突出主要模块，嵌套模块不再使用.改用：
    ```html
    <!-- S Comment Text A -->
    <div class="mod_a">
            
        <div class="mod_b">
            ...
        </div>
        <!-- /mod_b -->
            
        <div class="mod_c">
            ...
        </div>
        <!-- /mod_c -->
            
    </div>
    <!-- E Comment Text A -->
    ```

## 3. css

### 3.1 代码规范
* 样式书写一般有两种：紧凑格式 、展开格式。
* 左括号与类名之间一个空格，冒号与属性值之间一个空格。
* 为单个 css 选择器或新申明开启新行。
* css 属性值需要用到引号时，统一使用单引号。
* margin、padding、border 非特殊情况用缩写。

  ```css
  /* 推荐：展开格式 */
    .jdc {
        display: block;
        font-size: 24px;
        font-family: 'Hiragino Sans GB';
    }
    /* 为单个 css 选择器（并集）或新申明开启新行 */
    .jdc, 
    .jdc_logo, 
    .jdc_hd {
        color: #ff0;
    }
  ```
### 3.2 选择器
* 尽量少用通用选择器 *

* 不使用 ID 选择器

* 在未充分语义化的代码中，css 选择器中应避免使用标签名,虽然这能省下取类名的时间，但对后续代码变动、维护都会带来额外工作量。

* 应优先使用直接子选择器，避免使用后代选择器，当HTML嵌套较深时，后代选择器会消耗大量性能。

  ```css
  /* 推荐：*/
  .content > .title { }
  /* 不推荐：*/
  .content .title { }
  ```
### 3.3 注释
* 单行注释：注释内容第一个字符和最后一个字符都是一个空格字符，单独占一行，行与行之间相隔一行。（如上  3.1  所示）

### 3.4 reset.css

```css
html, body, div, span, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
abbr, address, cite, code,
del, dfn, em, img, ins, kbd, q, samp,
small, strong, sub, sup, var,
b, i,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section, summary,
time, mark, audio, video {
    margin:0;
    padding:0;
    border:0;
    outline:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}
body {
    line-height:1;
}
:focus {
	outline: 1;
}
article,aside,canvas,details,figcaption,figure,
footer,header,hgroup,menu,nav,section,summary { 
    display:block;
}
nav ul {
    list-style:none;
}
blockquote, q {
    quotes:none;
}
blockquote:before, blockquote:after,
q:before, q:after {
    content:'';
    content:none;
}
a {
    margin:0;
    padding:0;
    border:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}
ins {
    background-color:#ff9;
    color:#000;
    text-decoration:none;
}
mark {
    background-color:#ff9;
    color:#000; 
    font-style:italic;
    font-weight:bold;
}
del {
    text-decoration: line-through;
}
abbr[title], dfn[title] {
    border-bottom:1px dotted #000;
    cursor:help;
}
table {
    border-collapse:collapse;
    border-spacing:0;
}
hr {
    display:block;
    height:1px;
    border:0;   
    border-top:1px solid #cccccc;
    margin:1em 0;
    padding:0;
}
input, select {
    vertical-align:middle;
}
```



## 4. js

### 4.1 注释规范
* 注释的目的是告诉阅读者不宜察觉或者不易获取到的信息，而不是一目了然的东西。
    ```js
    // 声明一个变量timer  ----- 一目了然
    let timer=null;
    ```

* 单行注释： // 斜杠后面要增加一个空格
* 单行注释：注释的缩进需要与所注释的代码一致，且要位于被注释代码的上面。
#### 4.1.1 多行注释
* 推荐在函数中使用多行注释。
* 对有包含业务功能的函数、工具函数（utils），一定要使用多行注释(描述 + 参数 + 返回值说明)
  
    ```js
    /*
    *@desc 描述    --必填
    *@method 方法名
    *@for 所属类名
    *@param{参数类型}参数名 参数说明   --必填
    *@return {返回值类型} 返回值说明   --必填(如有)
    */
    function func() {
        // 用来存储定时器函数标识
        let flag = null;
    }
    ```



## 5. eslint

```js
	// 基于 @vue/airbnb 的eslint配置
	'no-console': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
 
    "vue/singleline-html-element-content-newline": "off", //vue 的单个属性不需要另起一行
    "@typescript-eslint/no-this-alias": [
        "error",
        {
          "allowDestructuring": true, // Allow `const { props, state } = this`; false by default
          "allowedNames": ["_this"] // aribnb 不允许直接使用this。用 _this 别名
        }
    ]
```

