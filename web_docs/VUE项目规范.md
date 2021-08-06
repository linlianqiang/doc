# VUE项目规范

## 文件命名
* 常规文件名（pages、views、utils...）采用小驼峰
* 组件名应以2-4单词组成，且命名规范应为大驼峰，如CocosHeader,CocosHeaderMenuItem
  
## 文件注释
* 每一个文件（.vue文件、.js文件等），都该注释其功能、作者、时间等。
  ```html
    <!--
    * @Descripttion: (对该文件的信息描述)
    * @Author: (作者)
    * @Date: (文件创建时间)
    --> 
    <template>
        ...
    </template>
    <script>
        ...
    </script>
  ```

## 结构
* 组件内标签顺序应为： template > script > style
* script 标签内部顺序：components > props > data > computed > watch > filter > 钩子函数（钩子函数按其执行顺序） > methods

## 公共组件
* 主框架公共组件应以Cocos开头，如CocosHeaderMenu
* 子项目公共组件应以项目名称或名称简写开头，如AccountHeaderMenu

## Template
* 标签内若有属性数量若超过一个，则应该换行 如:
  ```html
   <el-button v-if="a === 1">按钮</el-button> 
   <el-button  
    v-if="a === 1"  
    round 
  > 
    按钮 
  </el-button>

  ```
* 标签内应不可使用复杂表达式，若有需要进行复杂判断，应提取至计算属性
### Script
* 因Vue版本为2.X,因此不推荐在vue组件中使用TypeScript
### Style
* 应使用scoped避免样式污染

## eslint配置
...