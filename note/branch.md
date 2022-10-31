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