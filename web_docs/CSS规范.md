# 通用CSS规范

## 代码格式化
* 样式书写一般有两种：紧凑格式 、展开格式。
* 不使用无具体语义定义的标签选择器
* 统一使用四个空格进行代码缩进
* 每个属性声明末尾都要加分号；
* 左括号与类名之间一个空格，冒号与属性值之间一个空格
* 为单个 css 选择器或新申明开启新行
* css 属性值需要用到引号时，统一使用单引号
* margin、padding、border 非特殊情况用缩写。

  ```css
  /* 推荐：展开格式 */
    .jdc {
        display: block;
        font-size: 24px;
        font-family: 'Hiragino Sans GB';
    }
    /* 为单个 css 选择器或新申明开启新行 */
    .jdc, 
    .jdc_logo, 
    .jdc_hd {
        color: #ff0;
    }
  ```
## 选择器
* 尽量少用通用选择器 *
* 不使用 ID 选择器
* 在未充分语义化的代码中，css 选择器中应避免使用标签名,虽然这能省下取类名的时间，但对后续代码变动、维护都会带来额外工作量
* 应优先使用直接子选择器，避免使用后代选择器，当HTML嵌套较深时，后代选择器会消耗大量性能。推荐：.content > .title {}， 不推荐：.content .title {}
## 注释
* 单行注释：注释内容第一个字符和最后一个字符都是一个空格字符，单独占一行，行与行之间相隔一行。（如上所示）
* 文件信息注释：每个文件标明：描述、作者、日期
  
  ```css
  @charset "UTF-8";
    /**
    * @desc File Info
    * @author Author Name
    * @date 2015-10-10
    */
  ```

## css重置样式
* 
    ```css
    html, body, div, h1, h2, h3, h4, h5, h6, p, dl, dt, dd, ol, ul, li, fieldset, form, label, input, legend, table, caption, tbody, tfoot, thead, tr, th, td, textarea, article, aside, audio, canvas, figure, footer, header, mark, menu, nav, section, time, video { margin: 0; padding: 0; -webkit-tap-highlight-color: transparent;  }
    h1, h2, h3, h4, h5, h6 { font-size: 100%; font-weight: normal }
    article, aside, dialog, figure, footer, header, hgroup, nav, section, blockquote { display: block; }
    ul, ol { list-style: none; }
    img { border: 0 none; vertical-align: top; }
    blockquote, q { quotes: none; }
    blockquote:before, blockquote:after, q:before, q:after { content: none; }
    table { border-collapse: collapse; border-spacing: 0; }
    strong, em, i { font-style: normal; font-weight: normal; }
    ins { text-decoration: underline; }
    del { text-decoration: line-through; }
    mark { background: none; }
    input::-ms-clear { display: none !important; }
    body { font: 12px/1.5 \5FAE\8F6F\96C5\9ED1, \5B8B\4F53, "Hiragino Sans GB", STHeiti, "WenQuanYi Micro Hei", "Droid Sans Fallback", SimSun, sans-serif; background: #fff; }
    a { text-decoration: none; color: #333; }
    a:hover { text-decoration: underline; }
    textarea { -webkit-appearance: none; -moz-appearance: none; appearance: none; }
    ```
