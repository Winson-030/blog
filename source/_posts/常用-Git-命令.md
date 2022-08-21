---
title: 常用 Git 命令
date: 2022-08-20 16:14:30
tags: Git
---

> 建议在电脑端浏览，手机端浏览代码会有越界问题

------

`Merge`和`rebase`都是合并历史记录，但是各自的特征不同。

-   **merge**保持修改内容的历史记录，但是历史记录会很复杂。
-   **rebase**历史记录简单，是在原有提交的基础上将差异内容反映进去。因此，可能导致原本的提交内容无法正常运行。

您可以根据开发团队的需要分别使用merge和rebase。例如，想简化历史记录，

-   在`topic`分支中更新`merge`分支的最新代码，请使用`rebase`。
-   向merge分支导入`topic`分支的话，先使用`rebase`，再使用`merge`。

一般的仓库分支

主分支有两种：**master分支**和**develop分支**

-   **master**分支只负责管理发布的状态。在提交时使用标签记录发布版本号。
-   **develop**分支是针对发布的日常开发分支。刚才我们已经讲解过有合并分支的功用。

特性分支就是我们在前面讲解过的**topic分支**的功用。

这个分支是针对新功能的开发，在bug修正的时候从develop分支分叉出来的。基本上不需要共享特性分支的操作，所以不需要远端控制。完成开发后，把分支合并回develop分支后发布。

**release分支**是为release做准备的。通常会在分支名称的最前面加上release-。release前需要在这个分支进行最后的调整，而且为了下一版release开发用develop分支的上游分支。

一般的开发是在develop分支上进行的，到了可以发布的状态时再创建release分支，为release做最后的bug修正。

- 到了可以release的状态时，把release分支合并到master分支，并且在合并提交里添加release版本号的标签。

要导入在release分支所作的修改，也要合并回develop分支。

- **hotFix分支**是在发布的产品需要紧急修正时，从master分支创建的分支。通常会在分支名称的最前面加上 hotfix-。

例如，在develop分支上的开发还不完整时，需要紧急修改。这个时候在develop分支创建可以发布的版本要花许多的时间，所以最好选择从master分支直接创建分支进行修改，然后合并分支。

修改时创建的hotFix分支要合并回develop分支。


----------------

**一个重点**
将拉取回来的Git repo 从通过 https 提交改为通过 ssh 提交
1. 进入本地仓库
2. 编辑 .git 隐藏文件夹的config 配置文件

```shell
vim .git/config
-------------
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[submodule]
        active = .
[remote "origin"]
        #url = https://github.com/Winson-030/123.git
        #直接将https 链接更换为 git链接
        #记得提前配置好ssh 访问
        url = git@github.com:Winson-030/123.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
        remote = origin
        merge = refs/heads/main
[lfs]
        repositoryformatversion = 0
```



----------------



```shell
#确认项目目录的状态 
git status 

#将修改过的文件添加到索引 
	git add <file> 

#将当前文件夹修改过的所有文件添加到索引
git add . 

#提交修改过的文件 
git commit -m "提交修改过的文件123" 

#查看提交记录 
git log git log --graph --oneline 

#将修改文件推送到远程数据库 
git push git push -u origin master #需要输入仓库的账户密码 

#克隆远程数据库 
git clone <link> 

#添加远程数据库 
git remote add <name> <link> 

#从远程数据库拉取新数据 
git pull git pull origin master 

#新建仓库分支 
git branch <name> 

#显示仓库分支列表 
git branch 

#切换分支 
git checkout <branchName> 

#创建并切换分支 
git checkout -b <branchName> 

#合并 issue1 分支到master 分支上 
git checkout master git merge issue1 git 

#删除分支 
git branch -d <branchName> 

##并行操作分支 
$ git branch issue2 
$ git branch issue3  
$ git checkout issue2 
Switched to branch 'issue2' 
$ git branch 
* issue2 
  issue3 
  master 

#合并冲突处理
git merge issues2 

#手动修改冲突 
git add <file> 
git commit -m "sss" 

#取消最新的合并 
git reset --hard HEAD～ 

#使用rebase 合并 
git rebase issues2 

#修改冲突，添加rebase 说明 
git add <file> 
git rebase --continue 

#确认本地数据库与远程数据库的历史记录 
会临时生成 FETCH_HEAD ，
可以通过合并FETCH_HEAD或者重新pull 将远程内容合并到本地数据库 
git fetch 

#给提交增加标签和注解 
git tag <tagName> 

#显示包含标签的历史记录 
git log --decorate 

#添加注解标签 
git tag -a <tagName> 

#在HEAD指向的提交里添加名为banana的标签 
git tag -am "注解" <tagName> 

#显示标签的列表和注解 
git tag -n 

#删除标签 
git tag -d <tagName> 

#修改最近的提交 指定amend选项执行提交的话，可以修改同一个分支最近的提交内容和注解。 
git add <file> git commit --amend 

#取消过去的提交 在revert可以取消指定的提交内容。 
使用后面要提到的rebase -i或reset也可以删除提交。 
但是，不能随便删除已经发布的提交， 这时需要通过revert创建要否定的提交 
git revert <commitID> 

#遗弃提交 在reset可以遗弃不再使用的提交。
执行遗弃时，需要根据影响的范围而指定不同的模式， 
可以指定是否复原索引或工作树的内容。 
git reset --hard <commitID> 
git reset --hard HEAD~~ 
git reset --hard ORIG_HEAD #reset 错了可以回滚 

#提取提交 在cherry-pick，
您可以从其他分支复制指定的提交，然后导入到现在的分支。 
git cherry-pick <commitID> 

#如果发生冲突，修改冲突部分再提交 
git add <file> 
git commit 

#改写提交的历史记录 
合并两个commit 为一个commit 并提交
git rebase -i HEAD~~ 

#pick 改为 squash 修改提交 
git rebase -i HEAD～～ 

#pick 改为 edit 
git add <file> git rebase --continue 

#实际上，在rebase之前的提交会以ORIG_HEAD之名存留。 
如果rebase之后无法复原到原先的状态， 
可以用git reset --hard ORIG_HEAD 复原到rebase之前的状态。
git reset --hard ORIG_HEAD 

#从主分支汇合分支上的提交，然后一同合并到分支 
git checkout master git merge --squash <branchName> 

#冲突的时候要先修改冲突代码，再提交 
git add <file> git commit
```



--来自 [阮一峰的网络日志-常用 Git 命令清单](https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)

