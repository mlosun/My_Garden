---
{"dg-publish":true,"dg-path":"9 Obsidian/使用Git同步Obsidian-iOS（a-Shell方案）.md","permalink":"/9 Obsidian/使用Git同步Obsidian-iOS（a-Shell方案）/","created":"2025-08-31","updated":"2025-08-31"}
---


## 简介

经过查询，目前在 iOS 设备上使用 Git 同步 Obsidian 主要有以下三种方案：
1. Working Copy，付费，图形化界面，操作难度低（[link](https://utgd.net/article/20315)）
2. a-Shell，免费，使用精简版 git，操作难度中（[link](https://forum-zh.obsidian.md/t/topic/52630)）
3. iSH，免费，使用完整版 git，操作难度高（[link](https://cason.work/2023/04/20/obsidian-git-ios-%E5%A4%9A%E5%B9%B3%E5%8F%B0%E5%90%8C%E6%AD%A5/)）

经过稍微尝试，决定使用第二种方案，现将过程记录在此。

> [!NOTE] a-Shell 注意事项
> 1. a-Shell 的原理相当于创建了一个容器，在容器中跑了一个类 linux 来运行“精简版 git”，所以需要将外部（即 iOS 系统里的目录映射进这个容器中）
> 2. a-Shell 的 `.ssh` 目录并不在 `~` 目录下，而是在 `~/Documents` 目录下。一般也不需要进入 `~` 目录，就在 `~/Documents` 和 `~/Documents/你的仓库` 目录下操作即可。
> 3. a-Shell 内置的“精简版 git” 叫 lg2，命令和 git 一样，将 git 替换为 lg2 即可，如：
> 	- git clone ➡️ lg2 clone
> 	- git pull ➡️ lg2 pull
> 	- git add ➡️ lg2 add
> 	- git commit ➡️ lg2 commit
> 	- git push ➡️ lg2 push

## 前期准备

- 网络工具自备
- 已在 AppStore 下载 a-Shell 应用
- 已在 AppStore 下载 obsidian 应用
- 已经将 Obsidian 同步到 Github 的私有仓库

## a-Shell 配置 Github 密钥

1. 生成 SSH 密钥

	```bash
	ssh-keygen -t ed25519 -C "From iPhone a-Shell"
	```

2. 查看并复制公钥

	```bash
	cat .ssh/id_ed25519.pub
	```

3. 将公钥添加到 [Github](https://github.com/settings/keys)

4. 检查密钥是否配置成功

	```bash
	ssh -T git@github.com
	```

	出现 `You’ve successfully authenticated...` 即成功。

## a-Shell 配置目录映射并 clone

1. 选择 `Obsidian` 目录并映射

	```bash
	pickFolder
	```

	如果 `我的iPhone` 里没有 `Obsidian` 目录，就先在 Obsidian App 里创建一个仓库，再重试。

2. 将仓库拉取到本地

	```bash
	lg2 clone git@git.com:用户名/仓库名
	```

	静静的等待 clone 完成，我约 500MB 仓库大概花了 10 多分钟。

3. clone 完毕后，设置仓库的用户名和密码

	```bash
	lg2 config user.name "用户名"
	lg2 config user.email "邮箱"
	```

4. 使用 Obsidian App 打开你的仓库即可。（记得在 Git 插件里勾选“在此设备上禁用”，否则 Obsidian App 会无限重启）

## 进阶：实现自动 pull & push

TODO