# git 使用笔记

* [简介](git.md)
* [忽略文件](gitignore.md)  
  如果你不想让项目的某些文件或者目录上传到git, 就可以把相对路径加到这个文件中
* [gitkeey](gitkeep.md)
  默认空目录时不会被git上传的，如果你想上传，就在这个目录放一个`.gitkeep`文件。  
* [tag使用说明](tag.md)
* [github fork](fork.md)
* [github 创建项目](start.md)

[toc]
[[toc]]



## 0. 设置账号信息  




``` 
git config --global user.name "tiankonguse" // 配置提交用户名
git config --global user.email "i@tiankonguse.com" // 配置e-mail信息
git config --global core.editor vim // 配置默认文本编辑器，当Git 需要你输入信息时会调用它
git config --global alias.st status // 为status配置别名st，这样git status就可以写成git st
git config --list // 查看当前仓库的所有配置信息（包括分支相关的信息）
git config user.name // 查看当前仓库的用户名信息
git config -e --global // 编辑全局配置文件
git config -e // 编辑当前仓库的配置文件  
```


## 1. 忽略mode  


有时候重装操作系统，用户会修改，所有文件的 mode 修被修改了，git 都会认为是文件做了修改。  
这里就需要忽略 mode 了。  


```
git config --add core.filemode false  
```


## 2. 缓存密码  


如果频繁的向仓库中心提交代码时，就会遇到每次都需要输入用户名和密码的问题。  
可以把缓存密码的开关打开。  


```
git config --global credential.helper store  
git config --global credential.helper 'cache --timeout=3600'  
```


## 3. git diff 乱码


显示为 

```
<E9><94><99><E8><AF><AF><E4><BF><A1><E6><81><AF>
```

修复方法：  

```
git config --global i18n.commitencoding utf-8
git config --global i18n.logoutputencoding utf-8
export LESSCHARSET=utf-8
```

## 4. 显示各认知的 commit id

```
# --oneline 将每个提交放在一行显示
# --simplify-by-decoration 只展示分支或标签引用的提交
# --graph 查看各分支之间的关系
# --all 展示所有的提交
git log --oneline --simplify-by-decoration --graph --all
```


## 5. 同步 fork 的代码


```
#设置远程项目地址
git remote add upstream https://github.com/tiankonguse/leetcode-solutions.git  
#拉去最新数据
git fetch upstream master  
git merge upstream/master  #合并  
git push origin master #推送到 github  
```


## 6. CRLF 与 LF 警告问题  


UNIX/Linux  上换行符是 `0x0A（LF）`
Mac OS 上的换行符是`0x0D（CR）`  
windos 上的换行符是`0x0D0A（CRLF）`


所以面对换行符问题，`git`有几个配置可以选择。  


```
# 提交时转换为LF，检出时转换为CRLF
git config --global core.autocrlf true

# 提交时转换为LF，检出时不转换
git config --global core.autocrlf input

# 提交检出均不转换
git config --global core.autocrlf false

# 拒绝提交包含混合换行符的文件
git config --global core.safecrlf true

# 允许提交包含混合换行符的文件
git config --global core.safecrlf false

# 提交包含混合换行符的文件时给出警告
git config --global core.safecrlf warn

```


建议大家选择自动转换为`LF`，但是禁止文件混合多种换行符。  


```
git config --global core.autocrlf input
git config --global core.safecrlf true
```


## 7. 更新子模块  


```
# 添加子模块
git submodule add url name

#默认展示子模块的状态
git config --global diff.submodule log

#更新子模块：
git submodule update --remote
```

## 8. git 回滚


回滚没有 `git add`的文件 


```
git checkout -- <file>
```

回滚 `git add` 但没有 `git commit`的文件

```
git reset HEAD <file>
```


`git commit` 已运行，只能按照版本回滚


```
使用git log命令，查看分支提交历史，确认需要回退的版本
使用git reset --hard commit_id命令，进行版本回退
使用git push origin命令，推送至远程分支
```

回滚到上一次提交


```
git reset --hard HEAD^ 
```


## 9. 修改提交记录

参考文档：https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E5%86%99%E5%8E%86%E5%8F%B2  


如果只修改最后一次提交记录，使用下面命令直接修改。  


如果最后一次 commit 已经推送到远端，不建议进行修改提交信息。  
一定要修改的话，可以拉一个新的分支，在新的分支上修改。  

```
git commit --amend
```

如果要修改多个信息，就需要使用 `rebase` 来变基提交了。  


```
git rebase -i HEAD~2^
git rebase -i HEAD~3
git rebase -i HEAD~3..HEAD  #最近三次提交
```

## 10、合并多个提交记录

第一个提交保留为 `pick`，之后的提交进行`squash` 即可。  

```
git rebase -i  [startpoint]  [endpoint]
```

## 11、OpenSSL SSL_read: Connection was reset, errno 10054  


一般情况下，这个是网络不稳定，连接超时导致的。  
经常遇到的话，可以关闭 ssl 。  


```
git config --global http.sslVerify "false"
```


## 12、tag 相关操作


查看本地 tag


```
git tag
git tag -l "v1.*"
```



拉取远程 tag 到本地

```
git pull --tags
git pull upstream --tags
```


创建 tag

```
git tag -a v1.2
git tag -a v1.2 -m "commit myssh v1.0"
```


为历史提交增加 tag


```
git tag -a v0.1 44a59b780cbec4b585fa400d72f789c2a51fdc61
```


推送 tag 


```
git push origin v0.1
git push origin --tags 
```


## 13、fatal: unable to access Failed to connect to github.com port 443: Timed out


出现这个的原因是 git 被设置了代理

```
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy http://127.0.0.1:1080
```

清空代理即可重试即可

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```


## 14、版本管理   


A successful Git branching model : https://nvie.com/posts/a-successful-git-branching-model/
A Branching and Releasing Strategy That Fits GitHub Flow : https://hackernoon.com/a-branching-and-releasing-strategy-that-fits-github-flow-be1b6c48eca2
git版本管理规范： https://chjw.gammainfo.com/2018/06/08/git%E7%89%88%E6%9C%AC%E7%AE%A1%E7%90%86%E8%A7%84%E8%8C%83/
git分支管理规范： https://github.com/ecomfe/edp/issues/283

```
master分支：存放随时可供在生产环境中部署的代码
develop分支: 每次迭代版本的开发分支,保存当前最新开发成果的分支，从最新的master分支派生，开发完成后合并到 release 分支，并要求打一个alpha级的Tag
release分支: 从develop分支派生，允许做缺陷修正、准备发布版本所需的各项说明信息，但不新增功能，当发布成功时要打一个发布beta Tag，并将代码合并到 master 分支
hotfix分支: 在master分支发现bug时，在master的分支上派生出一个hotfixes分支
feature分支: 从develop分支发起feature分支，通常是在开发一项新的软件功能的时候使用，最终合并回develop分支
```


```
alpha 表示内部测试版本，不建议任何非参与开发人员所在团队使用，在alpha版本期间会不断增加新的功能并修复已有BUG
beta 表示公开测试版本，不建议稳定项目使用，在beta版本期间会酌情增加新功能，修复已知BUG
rc 表示发布候选版本，推荐各项目使用，在rc期间不得增加任何新功能，仅修复BUG。如果rc版本未发现任何BUG，则此版本直接转为正式发布版
GA：正式发布版本，真正的release版本
```

## 15、 git diff 




默认与当前 hash 对比

```
git diff HEAD~2
```

指定两个 hash 对比

```
git diff HEAD~2 HEAD~3
```

与 tag 对比

```
git diff v1.0.1
```

与分支对比

```
git diff feature/xxxx
```


与 hash 对比
一般来说，通过 hash 串的前 4～6 位就可以区分

```
git diff b45ba47d1b297217e3ec6a3ab0f61716a8d6ecbc c244d0bf06d56ec86aaedeefa5dcd84dd9febc60
git diff b45b 355e
```


diff 显示文件列表

```
git diff HEAD~2 --name-status
git diff HEAD~2 --stat
```



