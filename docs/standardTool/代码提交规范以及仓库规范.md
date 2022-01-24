## commit 提交规范

目前，社区有多种 commit message 的写法规范。[Angular 规范 ](https://link.jianshu.com/?t=https%3A%2F%2Fdocs.google.com%2Fdocument%2Fd%2F1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y%2Fedit%23heading%3Dh.greljkmo14y0)是目前使用最广的写法，比较合理和系统化，并且有配套的工具。

关于 commit message 的规范和介绍：[Commit message 和 Change log 编写指南](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)



type：

- feat：新增一个功能
- fix：修复 bug
- docs：仅仅修改了文档，比如 README, CHANGELOG, CONTRIBUTE 等等
- style：仅仅修改了空格、格式缩进等等，不改变代码逻辑
- refactor：代码重构，没有加新功能或者修复 bug
- perf：优化相关，比如提升性能、体验
- test：测试用例，包括增加缺失用例或者修正测试用例



推荐插件工具使用：

- [commitizen](https://www.npmjs.com/package/commitizen)：是一个撰写合格`commit message`的工具，用于代替`git commit` 指令
- [cz-conventional-changelog](https://www.npmjs.com/package/cz-conventional-changelog)：适配器提供 [conventional-changelog ](https://link.zhihu.com/?target=https%3A//github.com/conventional-changelog/conventional-changelog)标准（约定式提交标准）。基于不同需求，也可以使用不同适配器。



## gitlab 仓库规范

- Group：在 gitlab 中，Group 应该是多个具有关联关系或者相同属性的 Project 的集合

- Projcet：在 gitlab 中，Projcet 的定义也是每个细化的工程，也就是相当于一个代码仓库的概念

> 是否采用 Group 建立一个小组内部的前端群组，下分其他群组分别管理其他项目 Projcet？



项目仓库创建步骤：

1. 管理员在对应群组创建主仓库

   - 创建要求
     + 仓库的命名要有统一的规则
     + 主仓库固定分支（master、release）
     + 所有开发人员不允许在主仓库创建分支（如果有特殊情况，可以商讨）

2. 开发人员从主仓库 fork 代码到私人仓库

   - 进入主仓库 fork 到自己的仓库
   - fork 后自己的仓库可选地创建自己的开发分支
   - clone 自己的仓库到本地开发环境

3. 代码开发提交合并流程

   - 代码开发完成后提交到自己的仓库分支

     + 使用规范的 commit message 的提交形式（可借助工具 `commitizen`）

       ```bash
       git add *
       git commit -m ""
       git push origin master
       ```

   - 登陆gitlab，进入自己的仓库

   - 发起MR请求

4. 代码开发拉起其他人代码合并到本地流程：同步所 fork 的主仓库代码

   - 把想要同步的 fork 主仓库关联到本地

     ```bash
     git remote add (name) (SSH路径)
     ```

   - 查看状态确认是否配置成功

     ```bash
     remote -v
     ```

   - 拉取仓库下所有分支

     ```bash
     git fetch (name)
     ```

   - 把上游的远程代码合并到本地的 master 分支

     ```bash
     git checkout master
     git merge upstream/master 
     ```

   - 现在你的本地 master 就同步到所 fork 的主仓库最新版了，执行 `git push` 推送到自己的远程仓库，再提交一个 MR

5. 管理员合并 MR 请求

   - 管理员审核代码，并合并请求
   - 代码冲突没办法自动合并的，管理员需要手动合并
   - 部署代码到公测环境并进行测试

6. 代码发布上线

   - master测试通过，发起MR请求到release
   - 添加发布tag内容
     + 每个大版本更新到 release 发布到线上环境，需要打 Tag，详情介绍更新内容
   - 线上回归测试



















