# git分支操作

## 远程分支推送和拉取
### 场景: 
有时候我们开发需要开一个分支,这样可以有效的并行开发.

开分支有两种方式: 一种是在远程开好分支,本地直接拉下来;
一种是本地开好分支,推送到远程.

### 实例: 
- 远程先开好分支然后拉到本地
    ```
    git checkout -b feature-branch origin/feature-branch    //检出远程的feature-branch分支到本地
    ```
- 本地先开好分支然后推送到远程
    ```
    git checkout -b feature-branch    //创建并切换到分支feature-branch  
    git push origin feature-branch:feature-branch    //推送本地的feature-branch(冒号前面的)分支到远程origin的feature-branch(冒号后面的)分支(没有会自动创建)
    ```

## 删除远程分支


## 基本分支操作
1. 查看分支：	`git branch`
2. 创建分支：	`git branch`
3. 切换分支：	`git checkout` 或者 `git switch`
4. 创建+切换分支：	`git checkout -b` 或者 `git switch -c`
5. 合并某分支到当前分支：	`git merge`
6. 删除分支：	`git branch -d`

## 版本回退
1. `git revert` 通过添加一个新的提交, 把工作区文件还原到之前的状态,
2. `git checkout --hard` 直接撤销之前提交, 并把工作区文件还原到之前的状态 
3. `git reset`


方法一：如果我们确定远程的分支正好是我们需要的，而本地的分支上的修改比较陈旧或者不正确，那么可以直接丢弃本地分支内容，运行如下命令(看需要决定是否需要运行git fetch取得远程分支)：
  
  `git reset --hard origin/master` 或者 `git reset --hard ORIG_HEAD`

  解释：
  git-reset - Reset current HEAD to the specified state
  --hard Resets the index and working tree. Any changes to tracked files in the working tree since <commit> are discarded.

方法二：我们不能丢弃本地修改，因为其中的某些内容的确是我们需要的，此时需要对unmerged的文件进行手动修改，删掉其中冲突的部分，然后运行如下命令
  `git add filename`
  `git commit -m "message"`

方法三：如果我们觉得合并以后的文件内容比价混乱，想要废弃这次合并，回到合并之前的状态，那么可以运行如下命令：
  `git reset --hard HEAD`


# git 小游戏式学习式的网页: [url](https://learngitbranching.js.org/?demo=&locale=zh_CN), [nodemo](https://learngitbranching.js.org/?locale=zh_CN&NODEMO=)


1. git commit
2. git branch, git checkout <branch-name>
3. git merge b (a*), 把两个分支(b融合到a)的末端融合在一起, 添加一个新的提交
4. git rebase b (a*), 当前分支以分支b为基, 即把当前分支的提交附加到分支b的尾部

分离头
5. git checkout hashid-or-tag, 分离头, 让HEAD指针不再指向分支末尾
6. git checkout Name^, 向上(向根部)移动1个指针, Name可以是HEAD,分支名称, 哈希值, 或tag
6. git checkout Name~n, 向上移动多个指针, 其中n为数字1,2,3..,
7. git branch -f b1 Name, 将b1分支强制指向Name
8. Name^n 表示有多个父节点时移动到第n个父节点, 和~n可以级联: Name~1^2~2

撤销变更
git reset Name, 将当前分支重置回Name
git revert Commit, 重置Commit提交, 通过添加一个新的revert提交

整理提交记录, 记住最后更新main主分支的原则
- git cherrypick Name1 Name2 Name3, 将Name1, Name2, Name3 代表的提交依次附加到当前分支末尾
- git rebase -i Name~n, 利用GUI对Name前面n个进行rebase, 即重新创建一个指向Name~n根节点的分支
要在心里牢记 cherry-pick 可以将提交树上任何地方的提交记录取过来追加到 HEAD 上
（只要不是 HEAD 上游父级的提交就没问题）。
- git tag Tag Name, 给Name提交打上Tag

杂项
- 调试bug, 提交调试bug时可以把新建一个分支, 把调试语句和打印语句放到一个提交, 把修改bug的代码放到另一个提交, 
修复完成后再用cherry-pick把修复bug的提交添加到主分支中
- 修改历史提交中的某个提交, 可以用 rebase -i 或者 cherry-pick 调整想要的提交到最后, commit --amend

远程仓库
- 远程仓库并不复杂, 在如今的云计算盛行的世界很容易把远程仓库想象成一个富有魔力的东西, 
但实际上它们只是你的仓库在另个一台计算机上的拷贝。你可以通过因特网与这台计算机通信 
—— 也就是增加或是获取提交记录
- 远程分支, <remote-name>/<branch-name>, git checkout remote-branch 后会自动进入分离头状态
- git fetch, git fetch 实际上将本地仓库中的远程分支更新成了远程仓库相应分支最新的状态。
完成了仅有的但是很重要的两步:
  - 从远程仓库下载本地仓库中缺失的提交记录
  - 更新远程分支指针(如 o/main)
  - 不会改变你本地仓库的状态。它不会更新你的 main 分支，也不会修改你的工作区
- 像合并本地分支那样来合并远程分支。也就是说就是你可以执行以下命令:
  - git cherry-pick o/main
  - git rebase o/main, git rebase b1 b2, 以b1为基 rebase b2, 一个参数情况下默认rebase当前分支
  - git merge o/main 等等

- git push, git push 时如果有人已经提交了, push可能会自动merge失败, 解决办法是先git fetch,
再基于最新远程代码变基 git rebase origin/main, 本地处理完冲突后再push. 
这个过程有个简写: git pull --rebase
- 远程main locked, 需要pull request. 直接push到origin/main不被允许, 需要新建一个feature分支,
然后再把这个分支push到origin, 再申请pull request.
- git reset Name --hard某种意义上讲可以用git branch -f currant_branch Name来实现


### 合并特性分支
既然你应该很熟悉 fetch、pull、push 了，现在我们要通过一个新的工作流来测试你的这些技能。

在大型项目中开发人员通常会在（从 main 上分出来的）特性分支上工作，工作完成后只做一次集成。这跟前面课程的描述很相像（把 side 分支推送到远程仓库），不过本节我们会深入一些.

~~但是有些开发人员只在 main 上做 push、pull —— 这样的话 main 总是最新的，始终与远程分支 (o/main) 保持一致。~~

对于接下来这个工作流，我们集成了两个步骤：
将特性分支集成到 main 上, 推送并更新远程分支

### 关于 rebase 和 merge
在开发社区里，有许多关于 merge 与 rebase 的讨论。以下是关于 rebase 的优缺点：

优点:

Rebase 使你的提交树变得很干净, 所有的提交都在一条线上
缺点:

Rebase 修改了提交树的历史


### 其他
分支的远程跟踪, 
- git checkout -b totallyNotMain o/main, 创建分支并设置跟踪的远程分支
- git branch -u o/main foo, 设置跟踪的远程分支, 一个参数时默认设置当前分支的远程跟踪分支

- 推送修改远程分支
  - git push origin local_branch:remote_branch, 将本地的分支推送到远程, 本地留空表示删除, 
  这个branch可以是任何git的可识别地址, 如: HEAD^, main~2等
- 拉取远程分支
  - git fetch origin remote_source:local_source
- 拉取和合并 
  - git pull origin remote_source:local_source, 
  本地source不存在则会创建, 远程不存在则拉取一个空的分支

