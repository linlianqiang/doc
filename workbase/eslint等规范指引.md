## husky 

#### husky - git hooks工具

- 对git执行的一些命令，通过对应的hooks钩子触发，执行自定义的脚本程序

#### pre-commit

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

代码格式化工具。将代码变的更好看。与eslint的区别：

* eslint的主要功能在于检查：代码质量、代码风格（分号，单引号等）。
* prittier更专注代码格式，提供一些配置项，帮我们处理好美化。

## stylelint

样式格式化工具

```json

```

