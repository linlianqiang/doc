# HTML规范

## 命名
* HTML标签名、类名、标签属性和大部分属性值统一用小写。
* id 采用驼峰式命名。
* 单词之间统一使用中划线 “-” 连接。
* 命名应直观反映用途，避免难以理解的缩写，如.font-weight或者.header-menu，不推荐.ft-wt或.hd-mn(抽象出的有合理注释的全局样式除外)
    ```html
    <div class="header-menu"></div>
    ```
* meta标签某些属性等内容可大小写混合
    ```html
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
    ```
## 元素属性

* 元素属性值使用双引号语法
* 元素属性值可以写上的都写上
  
    ```html
    <input type="text">
    <input type="radio" name="name" checked="checked" >
    ```
## 代码：缩进、嵌套
* 统一使用四个空格进行代码缩进，使得各编辑器表现一致
* 元素嵌套规范：每个块状元素独立一行，内联元素可选
  
    ```html
    <div>
        <h1></h1>
        <p></p>
    </div>	
    <p><span></span><span></span></p>
    ```
## 注释规范
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
## HTML 文件模板
* PC端
  
    ```html
    <!DOCTYPE html>
        <html lang="zh-CN">
        <head>
        <meta charset="UTF-8">
        <meta name="keywords" content="your keywords">
        <meta name="description" content="your description">
        <meta name="author" content="author,email address">
        <meta name="robots" content="index,follow">
        <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
        <meta name="renderer" content="ie-stand">
        <title>PC端HTML模版</title>
        ​
        <!-- S DNS预解析 --> 
        <link rel="dns-prefetch" href="">
        <!-- E DNS预解析 --> 
        ​
        ​
        </head>
        <body>
        ​
        </body>
        </html>
    ```
* 移动端
    * width – viewport的宽度
    * height – viewport的高度
    * initial-scale – 初始的缩放比例
    * minimum-scale – 允许用户缩放到的最小比例
    * maximum-scale – 允许用户缩放到的最大比例
    * user-scalable – 是否允许用户缩放

    ```html
    <!DOCTYPE html>
    <html lang="zh-CN">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, shrink-to-fit=no" >
            <meta name="format-detection" content="telephone=no" >
            <title>移动端HTML模版</title>
                
            <!-- S DNS预解析 -->
            <link rel="dns-prefetch" href="">
            <!-- E DNS预解析 --> 
            ​
            <link rel="stylesheet" href="http://srcPath/index.css" rel="external nofollow" target="_blank"  rel="external nofollow" target="_blank"  >
            <!-- /开发机调试方式 -->
            <!-- E 本地调试 -->
        ​
        </head>
        <body>
        ​
        </body>
    </html>
    ```


