---
{"dg-publish":true,"dg-path":"8 零散笔记/解决Git commit 命令“失效”的异常情况.md","permalink":"/8 零散笔记/解决Git commit 命令“失效”的异常情况/","created":"2025-06-11","updated":"2025-06-11"}
---


> 最近一直在使用 [Cursor](https://www.cursor.com/cn) 敲代码，今早正常敲完代码后使用 Cursor 自带的源代码管理提交代码时，产生了报错。因为经常遇到 Git 报错，所以也没很在意，通常借助搜索引擎和 AI 都能很快搞定。可这次却足足搞了我一上午。

## 报错信息

- 在 Cursor 自带的源代码管理器报错：`Git：Failed to execute git`，以及一些 Git 日志再无其他可用信息。
- 使用终端手动执行 `git commit -m "提交代码"` 时，并无任何报错提示，但实质上代码并未提交（暂存时无异常）

## 问题检查

根据搜索和 AI 的反馈，做了 N 多检查和尝试：

- `git config user.name` 无问题
- `git config user.email` 无问题
- `git add .` 后，`git status` 检查已正常暂存代码
- `git commit -m "提交代码"` 后，`git status` 检查 commit 动作实际并未执行
- `git config list` 无异常
- 尝试本机其他仓库的提交，也出现类似情况
- 删除本地 `.git` 目录，重新初始化仓库，未解决
- 卸载本机 Git，重新下载安装 Git，未解决
- 按照 AI 反馈一步步执行各种检查、尝试的命令，均未解决

到这里基本上这里已经耗尽了我对 Git 的仅有认知。

## 问题解决

最后在反复询问各种 AI 后，终于在命令 `git commit -m "提交代码" --no-verify` 下提交成功了。并且经过重新复现问题：

- `git commit -m "提交代码"` 仍然无法提交
- `git commit -m "提交代码" --no-verify` 可以正常提交

经过向 AI 询问，`--no-verify` 参数的作用是跳过 Git 钩子（pre-commit 钩子），然后遵循 AI 反馈删除掉 `.git/hooks/pre-commit` 这个文件即可。

但是查询仓库的 `.git/hooks/pre-commit` 也并不存在。

思考了一下，使用 `git config list --global` 查询全局的配置，果然发现了一条:

```
core.hookspath=C:\Users\Administrator\AppData\Roaming\mkdocs-document-dates\hooks
```

进入其中后果然发现了 `pre-commit` 文件

删除掉后，解决问题。`git commit -m "提交代码"` 以及 Cursor 的源代码管理器均可正常提交了。

## 追根溯源

`mkdocs-document-dates` 是我维护 MkDocs 站点的一个插件，用于增加文档的创建和更新时间戳。查看其 README 得知：

> 采用了 Git Hooks 机制来自动触发缓存的存储（在每次执行 git commit 时），缓存文件也会随之自动提交。

看来应该是这里出了一些问题。这个应该也是插件的运行机制，但是为什么会出现在全局设置里就不得而知。

在我的使用场景下，MkDocs 推送到 Github 上去使用 Action 部署站点，只是很偶尔才会在本地运行检查，所以影响到不大。

已通过 [Issues](https://github.com/jaywhj/mkdocs-document-dates/issues/4) 反馈给插件作者，有后续将更新。