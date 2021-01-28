## 分支名称

分支名称应该符合正则表达式 ^(feature\/.+|bugfix\/.+|master)，即只允许有如下几种分支类型：

* master 默认的主干分支
* `feature/${title}[_${storyID}]` 个人需求分支，其中`_${storyID}`是可选的，例如：
* `bugfix/${title}[_${bugID}]` bugfix分支，其中`_${bugID}`是可选的

