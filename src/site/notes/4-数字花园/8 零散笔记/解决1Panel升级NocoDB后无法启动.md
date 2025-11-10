---
{"dg-publish":true,"permalink":"/4-数字花园/8 零散笔记/解决1Panel升级NocoDB后无法启动/","created":"2025-05-29","updated":"2025-05-29"}
---


相关链接：

- [升级nocodb后，无法启动，看日志是说mysql没找到，请问下怎么办？ - 1Panel - 社区论坛 - FIT2CLOUD 飞致云](https://bbs.fit2cloud.com/t/topic/9374)
- [\[BUG\] NOCODB 应用数据库参数配置错误 · Issue #6345 · 1Panel-dev/1Panel](https://github.com/1Panel-dev/1Panel/issues/6345)
- [Server does not start, error installing mysql · Issue #164 · nocodb/nocodb](https://github.com/nocodb/nocodb/issues/164)

日志报错：

```shell
Cannot find module 'mysql
```

解决方案：
1. 进入应用安装目录，找到环境变量文件 `.env`
2. 将 `PANEL_DB_TYPE="mysql"` 修改为 `PANEL_DB_TYPE="mysql2"`
3. 重建应用