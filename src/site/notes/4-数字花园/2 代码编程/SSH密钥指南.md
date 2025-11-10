---
{"dg-publish":true,"permalink":"/4-数字花园/2 代码编程/SSH密钥指南/","created":"2025-08-30","updated":"2025-08-31"}
---


## 简介

SSH 密钥（SSH Key）是一种用于安全登录远程服务器的“钥匙”，它由一对**公钥**和**私钥**组成。与密码相比，SSH 密钥更安全，也更方便。

- **公钥**（Public Key）：放在远程服务器上，可以公开。
- **私钥**（Private Key）：保存在本地电脑，必须保密，不能泄露。

可以将其类比为钥匙（私钥）和锁芯（公钥），公钥放在远程服务器上，私钥保存在本地电脑里，相互配对才能正确打开。

## 生成密钥

在终端内执行：

- 使用 *ed25519* 算法（推荐）：`ssh-keygen -t ed25519 -C "备注"`
- 使用 *rsa* 算法（兼容性好）：`ssh-keygen -t rsa -b 4096 -C "备注"`

执行后，会让你确认密钥保存在哪里，是否需要再加一个密码。在一路回车的默认情况下，会在 `~/.ssh` 目录下生成两个文件：

- **id_ed25519** 或 *id_rsa* 即私钥
- **id_ed25519.pub** 或 *id_rsa.pub* 即公钥

然后将公钥与远程服务器绑定即可。

## 绑定公钥

- [GitHub-SSH and GPG keys](https://github.com/settings/keys)
- [腾讯轻量云服务器-SSH密钥](https://console.cloud.tencent.com/lighthouse/sshkey/index)

## 进阶指南

使用 `~/.ssh/config` 配置文件，实现更便捷的 SSH 体验。

TODO
