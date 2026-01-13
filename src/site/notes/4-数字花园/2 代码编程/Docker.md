---
{"dg-publish":true,"dg-path":"2 代码编程/Docker.md","permalink":"/2 代码编程/Docker/","created":"2024-12-01","updated":"2025-05-10"}
---


## 常用命令

> 仅列出目前自己常用的，更多命令可参考 [Docker 命令大全 \| 菜鸟教程](https://www.runoob.com/docker/docker-command-manual.html)

- `docker ps` 列出 docker 容器，客获取**获取容器的 ID 和名称**
- `docker stats` 实时显示 docker 容器的**资源使用情况**
- `docker logs -f --tail 100 <容器ID或名称>` 实时显示的 100 条**容器日志**
- `docker compose up -d` 在当前目录下以后台模式运行 `docker-compose.yml` 内定义的容器

## 核心概念

- 镜像（Image）：镜像是 Docker 中的一个模板。
- 容器（Container）：容器是镜像运行时的实例。
- 仓库（Repository）：仓库用来存储镜像。

## 配置文件

- `Dockerfile` 定义如何构建一个镜像 [Docker Dockerfile \| 菜鸟教程](https://www.runoob.com/docker/docker-dockerfile.html)
- `docker-compose.yml` 定义和管理一个或多个容器 [Docker Compose \| 菜鸟教程](https://www.runoob.com/docker/docker-compose.html)

## 重启策略

- `restart: no` 
	- 容器不会自动重启。
	- 适用于不需要自动重启的容器，例如一次性任务或调试环境。
	- 是未指定时的默认策略。
- `restart: always` 
	- 无论容器退出状态如何，都会自动重启。
	- 适用于需要持续运行的服务，如 Web 服务器、数据库服务等。
- `restart: on-failure` 
	- 仅在容器以非零状态退出时自动重启。
	- 适用于那些在正常运行时会以零状态退出，但在遇到错误时会以非零状态退出的容器。
	- 可选参数：指定最大重启次数 `restart: on-failure:5`
- `restart: unless-stopped` 
	- 容器会自动重启，除非它被手动停止或 Docker 本身被停止。
	- 适用于需要持续运行的服务，但希望在手动停止后不会自动重启。
- 不同策略之间区别：

	| 情况                   | no  | always | on-failure | unless-stopped |
	| -------------------- | --- | ------ | ---------- | -------------- |
	| 容器正常退出 (0 状态)        | 不重启 | 重启     | 不重启        | 重启             |
	| 容器非正常退出 (非 0 状态)     | 不重启 | 重启     | 重启         | 重启             |
	| 手动停止 (`docker stop`) | 不重启 | 不重启    | 不重启        | 不重启            |
	| Docker 服务重启 (如系统重启)  | 不重启 | 重启     | 不重启        | 不重启            |
