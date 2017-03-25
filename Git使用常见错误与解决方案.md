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