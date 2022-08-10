## 安装

```js
cnpm install husky lint-staged prettier --save-dev
cnpm install stylelint stylelint-config-standard stylelint-order stylelint-config- --save-dev
```



## husky 7

#### husky - git hooks工具

- 对git执行的一些命令，通过对应的hooks钩子触发，执行自定义的脚本程序
- 一旦commit失败，不会修改任何文件。

```json
// package
"husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
}
```



## lint-staged

检测文件的插件。只检测暂存区的文件，(即git add .) 所以速度更快。

```json
// package.json  对不同的文件做不同的处理
"lint-staged": {
    "*.md": "prettier --write",
    "*.{ts,tsx,js,vue,scss}": "prettier --write",
    "*.{ts,tsx,js,vue}": "eslint --fix",
    "*.{vue,css,scss}": "stylelint --fix"
  }
```

## prettier

需同时安装vscode本地插件

快捷键：shift + alt+ f

代码格式化工具。将代码变的更好看。与eslint的区别：

* eslint的主要功能在于检查：代码质量、代码风格（分号，单引号等）。

* prittier更专注代码格式，提供一些配置项，帮我们处理好美化。

```json
{
    // 一行最多120 字符
  "printWidth": 120, 
    // 行尾需要有分号
  "semi": true,
    // 使用单引号
  "singleQuote": true,
    // 使用默认的折行标准
  "proseWrap": "never",
  "arrowParens": "avoid",
    // 末尾不需要有逗号
  "trailingComma": "none"
}
```



## stylelint

样式格式化工具。需同时安装vscode本地插件

http://stylelint.docschina.org/user-guide/

```js
.stylelintrc.js
module.exports = {
  extends: [
    'stylelint-config-standard',
    'stylelint-config-standard-scss',
    'stylelint-config-recess-order',
    'stylelint-config-prettier',
  ],
  plugins: ["stylelint-order"], // stylelint-order是CSS属性排序插件lint工具
  ignoreFiles: ['node_modules/**', 'dist/**', 'lib/**', 'src/assets/fonts/**', 'src/assets/style/reset.css'],
  rules: {
    'scss/at-import-partial-extension': null,
    'no-descending-specificity': null,
    'selector-pseudo-element-no-unknown': [
      true,
      {
        ignorePseudoElements: ['v-deep']
      }
    ],
    'selector-pseudo-class-no-unknown': [
      true,
      {
        ignorePseudoClasses: ['deep']
      }
    ],
    'font-family-no-missing-generic-family-keyword': null,
    'selector-class-pattern': null,
    'at-rule-no-unknown': null,
    'keyframes-name-pattern': null
  }
};
```

```
// .stylelintignore
node_modules
dist
lib

```

### 在vue中单独配置 

* ```
  npm install --save-dev stylelint-config-recommended-scss
  npm install --save-dev postcss-html stylelint-config-recommended-vue
  ```

## eslint

需同时安装vscode本地插件

如何处理eslint 与 prettier 的冲突。使用 eslint-config-prettier.

* 禁用所有与prettire冲突的规则
* 将所有prettier的规则和修改导入eslint中，需要在eslint中显示这些错误

```json
// eslintrc.js 
{
  "extends": [
    "some-other-config-you-use",
    // 放在底部，覆盖其他规则
    "prettier"
  ]
}
"plugins": ["prettier"],
// 在eslint中显示这些错误
 rules: {
    "prettier/prettier": "error",
  }
```

## babel



## vscode

```json
{
  "eslint.validate": ["javascript", "javascriptreact", "vue", "typescript", "typescriptreact"],
  "stylelint.validate": ["css", "scss", "less", "vue"],
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.fixAll.stylelint": true
    // "source.fixAll.markdownlint": true
  },
  "vetur.validation.script": false,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  // 强制表明JavaScript & vue使用Prettier去格式化
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[vue]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "prettier.requireConfig": true
}


```
