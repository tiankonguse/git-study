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
git config credential.helper store  
git config credential.helper 'cache --timeout=3600'  
```



