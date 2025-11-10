---
{"dg-publish":true,"permalink":"/4-数字花园/8 零散笔记/解决 Gitihub 报错 Failed to connect to github.com port 443/","created":"2024-08-20","updated":"2024-08-20"}
---


## 问题与解决

通常是代理的网络连接不上

在网页可以打开 Github 时，说明命令行在拉取/推送代码时没有使用代理

以 Clash for Windows 为例，端口号 7890，设置全局代理即可解决问题：

```bash
# 设置全局代理
git config --global http.proxy http://127.0.0.1:7890 
git config --global https.proxy http://127.0.0.1:7890
```

## 其他相关指令

```bash
# 查看全局代理
git config --global --get http.proxy
git config --global --get https.proxy
```

```bash
# 取消全局代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```

## 参考资料

[Git报错： Failed to connect to github.com port 443 解决方案-CSDN博客](https://blog.csdn.net/zpf1813763637/article/details/128340109)