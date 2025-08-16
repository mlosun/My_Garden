---
{"dg-publish":true,"dg-path":"8 零散笔记/删除 Github 仓库全部的 commit 记录.md","permalink":"/8 零散笔记/删除 Github 仓库全部的 commit 记录/","created":"2025-04-06","updated":"2025-04-06"}
---


当过去 commit 记录中包含隐私信息后，想删除全部的 commit 记录，但是又不想删除并重新建立仓库（有 Star），可以将仓库 clone 到本地后使用以下方法：

以 main 分支为例：

```git
# 新建一个空白分支
git checkout --orphan latest_branch

# 添加所有文件
git add -A

# 强制删除所有分支，如果是main
git branch -D main

# 将当前分支命名为main
git branch -m main

# 提交commit
git commit -m "Initial commit"

# 强制推送到远程仓库
git push -f origin main
```

参考来源：[删除github上的commit记录 - 老卫同学 - 博客园](https://www.cnblogs.com/oldweipro/p/16634523.html)