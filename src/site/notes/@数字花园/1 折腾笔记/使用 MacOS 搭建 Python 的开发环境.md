---
{"dg-publish":true,"dg-path":"1 折腾笔记/使用 MacOS 搭建 Python 的开发环境.md","permalink":"/1 折腾笔记/使用 MacOS 搭建 Python 的开发环境/","created":"2025-07-28","updated":"2025-07-29"}
---


## 安装 Git（MacPorts）

> MacOS 12.x 版本已不受 [Homebrew](https://brew.sh/zh-cn/) 官方支持

### 安装 MacPorts

1. 安装命令行工具：终端执行 `xcode-select --install` 进行安装
2. 在 [MacPorts](https://www.macports.org/) 找到想要安装的 MacPorts 版本（[macOS Monterey v12](https://www.macports.org/install.php)），下载后直接安装

### 安装 Git

```bash
sudo port install git
```

### 验证

```bash
git --version  # 应输出 git version 2.50.1
which git      # 应输出 /opt/local/bin/git（MacPorts安装的路径）
```

### 配置 Git

```bash
git config --global user.name "你的名字"       # 必须
git config --global user.email "你的邮箱"      # 必须
git config --global core.editor "code --wait"  # 使用 VS Code 作为默认编辑器
git config --global color.ui auto              # 开启颜色提示
git config --global core.autocrlf input        # 避免换行符问题（macOS）
git config --global core.quotepath false       # 避免中文乱码
git config --global init.defaultBranch main    # 设置默认使用的 main 分支名（新项目）
```

### 补充：MacPorts 常用命令

```bash
# 查找与查看
port list                      # 列出所有可用软件包
port search <关键词>           # 搜索软件包（支持模糊匹配）
port installed                 # 查看已安装的软件包
port outdated                  # 查看可升级的软件包

# 安装、升级与卸载
sudo port install <软件名>      # 安装软件包（自动处理依赖）
sudo port upgrade <软件名>      # 升级指定软件包
sudo port upgrade outdated      # 升级所有可更新的软件包
sudo port uninstall <软件名>    # 卸载软件包

# 清理与维护
sudo port clean --all <软件名>  # 清除编译产生的临时文件
port echo leaves                # 列出不再被依赖的孤立软件包
sudo port uninstall leaves      # 删除孤立软件包
port installed inactive         # 列出已安装但未激活的旧版本
sudo port uninstall inactive    # 删除未激活的旧版本

# 更新、同步与帮助
sudo port selfupdate            # 更新 MacPorts 自身及软件索引
sudo port sync                  # 仅同步软件索引（不更新 MacPorts 本身）
port help <命令>                # 查看某个命令的帮助说明，如 port help install，按 q 退出
```

## 安装 Python

### 下载安装包

在 [Python官网](https://www.python.org/) 找到想要安装的 Python 版本（[v3.12.10](https://www.python.org/downloads/release/python-31210/)），下载后直接安装

### 验证

```bash
which -a python3

# 输出
/usr/local/bin/python3   # 官网安装包安装的 Python
/usr/bin/python3         # MacOS 系统自带的 Python
```

### 设置为默认

```bash
bash -c '
# 1) 确保 /usr/local/bin 排在最前
echo '\''export PATH="/usr/local/bin:$PATH"'\'' >> ~/.zshrc

# 2) 追加别名
cat >> ~/.zshrc <<'\''EOF'\''

# --- Python 3.12 统一别名 ---
alias python=/usr/local/bin/python3
alias python3=/usr/local/bin/python3
alias pip=/usr/local/bin/pip3
alias pip3=/usr/local/bin/pip3
EOF

# 3) 立即生效
source ~/.zshrc
'
```

### 验证

```bash
python --version    # 应显示 Python 3.12.x
python3 --version   # 应显示 Python 3.12.x
pip --version       # 应显示 pip 25.x (Python 3.12)
pip3 --version      # 应显示 pip 25.x (Python 3.12)
```

### 配置国内镜像源

```bash
# 配置（清华大学镜像源）
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
pip config set install.trusted-host pypi.tuna.tsinghua.edu.cn

# 验证
pip config list

# 重置
pip config unset global.index-url
```
