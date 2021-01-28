## 提交 commit 规范 

每次提交，Commit message 包括必选的Header，可选的Body和Footer。

```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

Header部分只有一行，包括三个字段：type（必需）、scope（可选）和subject（必需）。

- 【必选】type用于说明 commit 的类别，只允许使用下面7个标识。
  * feat：新功能（feature）
  * fix：修补bug
  * docs：文档（documentation）
  * style： 格式（不影响代码运行的变动）
  * refactor：重构（即不是新增功能，也不是修改bug的代码变动）
  * test：增加测试
  * chore：构建过程或辅助工具的变动
- 【可选】scope用于指定 commit 影响的范围，比如数据层、控制层、视图层等等，或者具体所属package。
- 【必选】subject是 commit 目的的简短描述。包含如下部分：

```
commit简短描述 (--task=12345678|--bug=12345678|--task=12345678) 可选的单标题
```

- 【可选】Body部分是对本次 commit 的详细描述。

- 【可选】Footer部分关闭 Issue。

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。

