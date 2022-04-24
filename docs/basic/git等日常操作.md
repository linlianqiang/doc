## git



#### 将某个文件回退到某个版本

```js
// 查看日志
git log /path/fileName
// 查看commit某个版本
git checkout 7b284360171220563b8c497378ff579369655cee path/fileN

// 本地回退
git reset --hard commitHash
// 线上回退
git push -f origin mast
```

#### 撤回add

```js
git reset HEAD 如果后面什么都不跟的话 就是上一次add 里面的全部撤销了 
```

#### 删除远程分支

```js
git push origin --delete f
```

#### commit 规范



![img](https://img2020.cnblogs.com/blog/2097780/202011/2097780-20201102201259796-600745321.png)







#### git status

查看本地代码是否干净，未commit之前。也可以查看commit之后，还未push的状态（有多少个commit）

　　　　在 git add .之后，变为绿色。commit之后，看不出修改。

　　　　![img](https://img2020.cnblogs.com/blog/2097780/202012/2097780-20201222094119342-1741048868.png)

 

#### git log

可以查看所有commit的状态 

#### git show

查看最近的一次commit，并且可以查看到修改的文件 （git show hashId，查看指定）

#### git commit --amend

可以重新commit，如果忽略了某些信息的话。

　　　　![img](https://img2020.cnblogs.com/blog/2097780/202012/2097780-20201222095354588-1956984737.png)

 

 

#### git reset HEAD <file> 

 如果提交了两个文件，实际只想提交一个。

　　　　![img](https://img2020.cnblogs.com/blog/2097780/202012/2097780-20201222095821708-1911481341.png)

 

 

####  git reset --soft HEAD^ :

撤回当前的commit操作，不会撤回本地的改变。

####  git diff

可以查看commit的 与 远程的比较不同，不是冲突代码。

####  git checkout -- <file>

 对本地做的任何修改都会被撤销，会回到git上提交的最后一个版本。

　　　　![img](https://img2020.cnblogs.com/blog/2097780/202012/2097780-20201222100203204-1254904140.png)

 

 

####  git checkout -b fear-login

创建分支开发新功能。



####   将远程分支拉到本地

git fetch origin dev



