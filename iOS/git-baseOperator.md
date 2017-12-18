# Git基本操作 及 分支管理



## 常用命令及几个专有名词的概念

### 日常工作中只需记住下图6个命令就可以了。

![command](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015120901.png)





### 更多命令

![](https://img.w3cschool.cn/attachments/image/20170206/1486348362884912.jpg)



### 几个专有名词解释

- Workspace：工作区
- Index / Stage：暂存区
- Repository：仓库区（或本地仓库）
- Remote：远程仓库



## ssh key生成

SSH 公钥默认储存在账户的主目录下的 `~/.ssh` 目录 进入到该目录 `cd ~/.ssh`,然后查看 是否存在ssh key，如没有 用如下命令生成 ssh key

`ssh-keygen -t rsa -C "example@xxx.com"`



## Git项目（包含SVN项目）迁移Gitlab流程

1. 登陆gitlab账户 在自己所属账户对应的group下 新建Project，记住对应的 repo地址 ，如图所示![git-project](/Users/yongfeng/Desktop/git-project.png)
2. 命令行终端切 准备迁入的项目 根目录下 `cd projectPath`
3. 执行 `git remote -v` 查看当前repo管理的远程remote是什么 记录名称
4. 执行`git remote rm remoteName` 移除跟之前remote的关联
5. 执行`git remote add origin repoURL` 关联新的remote地址（push和pull时默认 remote是origin）
6. 执行`git push -u origin [master]` 将本地repo推送到远程remote
7. 其他同事 执行 `git clone repoURL` clone代码 进行开发



## 日常开发git使用流程及分支管理

### 日常开发流程

1. 每天上班第一件事 执行 `git pull` 同步更新同事的代码修改到本地
2. 开发修改具体代码完成后 执行`git add filePath`(更多用`git add .`) 将需要提交的修改提交到暂存区（Index/Stage）
3. 执行 `git commit -m 'commit message'` 将暂存区提交到本地仓库
4. 如果需要立即推送到远程 执行`git push`, 如果要继续开发后一起提交 重复 2、3两步，最后再执行`git push`

> 注意事项：
>
> 1. 项目及文件夹 文件尽量不要用中文命名，可考虑 拼音
> 2. git 提交的 颗粒度问题 和 提交的原子性问题
> 3. commit message 规范
> 4. 分支 合并 merge 和 rebase的 区别 （自行研究）



### git 分支管理

详细解释 [Git 工作流程](http://www.ruanyifeng.com/blog/2015/12/git-workflow.html)

这里 主要介绍 git flow ，对其他想了解的可以找我交流

### git flow

![git flow](http://nvie.com/img/git-model@2x.png)

1. 项目 owner或master 分出 master 和 devlop分支
2. 项目组开发人员 clone 代码后 `git checkout develop` 进行开发
3. 如果是 新的 feature，开发人员直接在 gitlab远程 创建对应 feature分支 然后 本地`git pull`后执行`git checkout feature`
4. 然后进行 开发修改代码，完成后 按照 日常开发流程中的。2、3、4这4步进行操作
5. 整个feature开发完成后 在gitlab页面 发起 merge reuqest
6. 由owner 或 master 进行代码审核，通过后合并进去对应分支
7. 功能需求开发 完成时 在gitlab 远程 分出 release 分支 如 release-1.0.0, 此时进入<font color=red>***需求冻结期*** </font> ***（不在进行新需求开发，新需求放到下一版本规划）***
8. 由测试团队进行 release代码 测试验证（1-2轮）如通过，此时 合并到 master ：`git checkout master` `git merge feature``git push` 合并完成后 进入 ***代码冻结期（此时非致命bug延后到下一版本处理）***， 开始回归测试（1-2轮）测试通过后开始 进行发版 代码打tag `git tag -a V1.0.0` `git push —tags`
9. 发版完成后 将 feature 合并到 develop分支，然后删除 对应的 feature