# GIT 分支


```
# 本地创建远程分支同名的分支
git checkout -b newBranchName origin/remoteBranchBame

# 本地基于同名 tag 创建分支
git checkout -b newBranchName tagName

# 切换分支
git checkout master 


# 显示所有分支
git branch -a 

# 只查看远程分支
git branch -r 

# 查看远程分支的具体信息
git remote show origin 

# 删除远程不存在的分支
git remote prune origin 
```


