## workspace

```json
{
  "files.autoSave": "onFocusChange",
  "files.exclude": {
    "**/.git": false
  },
  "eslint.validate": ["javascript", "vue"],
  "stylelint.validate": ["css", "scss", "less"],
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.fixAll.stylelint": true
  },
  // "editor.formatOnSave": true,
  "editor.tabSize": 2,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  // 强制表明JavaScript & vue使用Prettier去格式化
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  // 使用prettier格式化
  "[vue]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
  // 规定的文件类型 这里不是必要的
}

```

