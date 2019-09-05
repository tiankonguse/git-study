# git 使用笔记

* [简介](git.md)
* [忽略文件](gitignore.md)  
  如果你不想让项目的某些文件或者目录上传到git, 就可以把相对路径加到这个文件中
* [gitkeey](gitkeep.md)
  默认空目录时不会被git上传的，如果你想上传，就在这个目录放一个`.gitkeep`文件。  
* [tag使用说明](tag.md)
* [github fork](fork.md)
* [github 创建项目](start.md)


## 常见命令



0. 设置账号信息  




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


1. 忽略mode  


有时候重装操作系统，用户会修改，所有文件的 mode 修被修改了，git 都会认为是文件做了修改。  
这里就需要忽略 mode 了。  


```
git config --add core.filemode false  
```


2. 缓存密码  


如果频繁的向仓库中心提交代码时，就会遇到每次都需要输入用户名和密码的问题。  
可以把缓存密码的开关打开。  


```
git config --global credential.helper store  
git config --global credential.helper 'cache --timeout=3600'  
```


3. git diff 乱码


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

4. 显示各认知的 commit id

```
# --oneline 将每个提交放在一行显示
# --simplify-by-decoration 只展示分支或标签引用的提交
# --graph 查看各分支之间的关系
# --all 展示所有的提交
git log --oneline --simplify-by-decoration --graph --all
```


