# Git - 常见错误与解决方案

 1. [error: The following untracked working tree files would be overwritten by checkout:](http://www.druhosting.com/content/git-error-following-untracked-working-tree-files-would-be-overwritten-checkout)

 ```
 $ git clean -d -fx ""
$ git checkout -f another-branch
 ```
 
 2. [fatal: Unable to create 'xxx/xxx/.git/index.lock': File exists.](http://www.java123.net/412734.html)

 ```
 # 解决办法：直接删除 index.lock 文件
$ rm xxx/xxx/.git/index.lock
 ```
 

# Git - 回滚到指定commit
### 方法一：reset

```
git reset --hard commit-id
git push origin HEAD --force
``` 

### 方法二：revert
```
git revert commit-id
```
如果 Git revert 的时候出现下面错误

```
error: Commit 7ec5362d47014deab2d1a3603c0e110caxxxxe06 is a merge but no -m option was given.
fatal: revert failed
```
这是因为`revert`的那个`commit`是一个`merge commit`，它有两个`parent`, Git 不知道`base`是选哪个`parent`，就没法`diff`

```
git revert commit-id -m 1
```
* 1 - 表示当前分支
* 2 - 表示 merge 过来的那个分支

# Git - 恢复被误删除分支

* 通过以下命令查看操作日志，获取需要恢复的递交`<sha>`

```
$ git log -g
```

* 通过以下命令恢复分支<branch>

```
$ git checkout -b <branch> <sha>
```

eg: 如需要恢复`<sha>(35787c7e277f13277aa493dbe053a70fbf47ebd3)` 至 `<branch>(recover_branch)` ,执行命令如下

```
$ git log -g
commit 35787c7e277f13277aa493dbe053a70fbf47ebd3
...

$ git checkout -b recover_branch 35787c7e277f13277aa493dbe053a70fbf47ebd3
```

# Git - 把指定 commit 合并到当前分支
### 1. 命令行方式
将 commit-id 的递交应用至当前分支

```
git cherry-pick commit-id
```

### 2. SourceTree
选中想要合并至当前分支 -> 右键点击 -> 选择遴选 -> 确认

# 从版本库中彻底删除某个文件，不再显示在历史记录中（例如：账号/密码）

```
git filter-branch -f --tree-filter 'rm -rf vendor/gems' HEAD
git push origin --force
```