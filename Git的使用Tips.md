# Git 的基本使用命令
```
git init # 在当前项目目录中生成本地git管理,并建立一个隐藏.git目录
git add . # 添加当前目录中的所有文件到索引
git commit -m "first commit"  #提交到本地源码库，并附加提交注释
git remote add origin https://github.com/DeveloperLY/Test.git  # 添加到远程项目，别名为origin
git push -u origin master # 把本地源码库push到github 别名为origin的远程项目中，确认提交
git tag # 打开本地标签备份
git push —tags # 提交所有的本地标签
git tag -d 标签名 # 删除本地标签
git push origin:标签名 # 删除远程标签

```

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

# Git - 从版本库中彻底删除某个文件，不再显示在历史记录中（例如：账号/密码）

```
git filter-branch -f --tree-filter 'rm -rf vendor/gems' HEAD
git push origin --force
```

# 把旧项目提交到Git上，但是会有一些历史记录，这些历史记录中可能会有项目密码等敏感信息。如何删除这些历史记录，形成一个全新的仓库，并且保持代码不变
## 1.Checkout
```
   git checkout --orphan latest_branch
```
## 2. Add all the files
```
   git add -A
```
## 3. Commit the changes
```
   git commit -am "commit message"

```
## 4. Delete the branch
```
   git branch -D master
```
## 5.Rename the current branch to master
```
   git branch -m master
```
## 6.Finally, force update your repository
```
   git push -f origin master
```

# 如果标签已经推送到远程，要删除远程标签，先从本地删除：
```
# 先从本地删除
git tag -d v1.0
# 然后删除远程
git push origin :refs/tags/v1.0
```