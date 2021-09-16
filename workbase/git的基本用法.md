#### 使用习惯

* 本地develop只能合并远程的develop
* 功能或者bug等，都要在develop上新建分支

#### 将某个文件回退到某个版本

```js
// 查看日志
git log /path/fileName
// 回退到某个版本
git checkout 7b284360171220563b8c497378ff579369655cee path/fileN
```

