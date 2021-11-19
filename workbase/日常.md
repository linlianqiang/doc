## 进程/端口

#### 查看PID

```
netstat -aon|findstr "8081"
//查看具体哪个y
tasklist|findstr "9088"
```

#### 结束进程

```
taskkill /T /F /PID 9088 
```

## git

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

#### 撤回add

```js
git reset HEAD 如果后面什么都不跟的话 就是上一次add 里面的全部撤销了 
```

#### 删除远程分支

```js
git push origin --delete f
```



