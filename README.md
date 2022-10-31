# git tutorial
- git 简明指南: https://www.runoob.com/manual/git-guide/
- git tutorial: https://www.runoob.com/git/git-tutorial.html
- git command docs: https://git-scm.com/docs
- https://github.com/git-guides/git-init
- https://zhuanlan.zhihu.com/p/539150842

![img.png](https://www.runoob.com/wp-content/uploads/2015/02/git-command.jpg)

# git command
```


```

- git add 'fpath'
- git status
- git config
  - git config 本地仓库配置在.git/config下
  - git config --list, 查看当前的git配置信息
  - git config --global user.name, 查看或设置仓库用户名
  - git config --global user.email
  - git config -e, 编辑本地配置文件
- git commit -m 'msg'
- git --help <command>, 打开<command>的帮助页面
- git reset, 重置暂存区
- git checkout, 签出, 重置工作区

# git远程相关
- git remote add <name> <server>, 添加远程仓库
  -  git remote add origin git@github.com:hhqx/git-learn.git
- git remote rm <name>, 删除远程仓库
- git remote show <name>, 显示远程仓库<name>
  - git remote -v show, 显示远程仓库详情
- git fetch
  - git fetch, 拉取远程仓库到本地副本(本地仓库不变)
- git pull
  - git pull submodule url name, 
  - git 
- git push
- git remote add origin <server>

# git 权限相关
- git credential-osxkeychain erase, 擦除本地缓存的https凭证
- git push/pull 有https和ssh两种方式, https方式需要在github上生成指定token并在push/pull时输入, ssh方式需要把公钥添加到github授权中

- git config --global core.safecrlf false, set auto convert crlf to false.

# git 分支相关
- git checkout -b <branch-name>
- git checkout master
- git branch -d <branch-name>
- git push 
  - git push --set-upstream origin master, push时设定当前分支默认推送的远程仓库及分支

- git branch –delete dev, 删除已经合并的分支

1. 当执行 git reset HEAD 命令时，暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。

2. 当执行 git rm --cached <file> 命令时，会直接从暂存区删除文件，工作区则不做出改变。

3. 当执行 git checkout . 或者 git checkout -- <file> 命令时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区中的改动。

4. 当执行 git checkout HEAD . 或者 git checkout HEAD <file> 命令时，会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。



# pycharm 同步配置
