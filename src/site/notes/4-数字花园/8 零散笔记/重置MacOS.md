---
{"dg-publish":true,"permalink":"/4-数字花园/8 零散笔记/重置MacOS/","created":"2024-08-17","updated":"2024-08-17"}
---


## 一台老 MacBook Pro

手上的是一台大约在 2017 年购入的 MacBook Pro，带指纹解锁和 bar 的那种。这台设备在使用了多年后系统内部混杂不堪，大约在半年前自己购入了一台 零刻的 Windows 迷你主机 EQ59 把玩，玩着玩着发现现在 Windows 系统也已经搞的还不错了，同时因为当时要用的一些软件，在 MacOS 系统下支持不是很好，于是慢慢的主力设备居然变成了这台千元的 EQ59 上了。而当初万元购入的 MacBook Pro 居然闲置在那里，只有需要翻阅部分旧资料，或者偶尔躺床上看个电影时才会拿出来用一下。

而最近那款 MacOS 下支持不是很好的软件使用频率极低了，而且外出办公的频率增加，EQ59 虽然很小巧带出门也很方便，目的地也总有显示器使用，但总归还是自带屏幕的设备更适合外出办公一些。于是就想着把这台尘封已久的 MacBook Pro 收拾一下。同时在那几年使用了苹果全家桶，所以基本上家里的照片、视频等等也都存储在 iCloud 里，200G 每个月费用 21。实际上自己也老早有将那些照片转移到对象存储的想法，一来使用方便灵活，二来同样的费用可以搭建好几套备份了。毕竟 iCloud 的服务么，总归还是不太信任...（踩过坑）

## 重置系统

得益于自己多年良好的文件存储习惯，绝大多数需要保存的文件，都存储在 iCloud 或者已另有存储了。所以不需要花太多时间备份，只是检查了一遍 App 清单。

搜索到 [Apple 官方的重置 MacOS 教程](https://support.apple.com/zh-cn/guide/mac-help/mh27903/13.0/mac/13.0)：
1. 重启 & 按住 Command+R
2. 进入磁盘工具，选择宗卷并点击抹掉
3. 格式选择 `APFS`，确认抹掉（切记备份好数据）
4. 待抹掉进程完成后，叉掉磁盘工具，重新连接 Wifi
5. 选择重新安装 MacOS，点击继续，就开始下载并安装新系统了
6. 下载时间取决于网速，完成后就和新配置一台 MacOS 一样了

## 配置系统

新系统安装好后，第一件事就是将系统配置调整为自己习惯的方式。过了一遍系统设置选项，毕竟有大半年没有把 MacOS 当做主力机使用了，一些使用习惯也已经忘记，目前只调整了以下两项：

1. 外观设置为自动模式
2. 桌面与程序坞的右下触发角改为调度中心

## 安装应用

先安装一波常用的 App，当然也有一些以前常用的优秀 App，等到需要使用的时候再去安装就行。

### 下载 dmg 安装

- [AppCleaner](https://freemacsoft.net/appcleaner/) 软件卸载
- [Chrome](https://www.google.com/intl/zh-CN/chrome/) 浏览器
- [Obsidian](https://obsidian.md/) 笔记软件
- 一款 C 开头的能大幅提升网络冲浪体验的软件
- 坚果云

### App Store 安装

- 微信
- QQ
- Pixiu

## 开发环境

作为一个编程菜鸟，启用新设备了当然要搭建一套符合自己需求的开发环境。
- [VScode](https://code.visualstudio.com/) 代码编辑器
- [Git](https://git-scm.com/) 版本控制系统
- [Github Desktop ](https://desktop.github.com/) Github 客户端
- [Python](https://www.python.org/) 人生苦短，我用 Python
- [Homebrew](https://brew.sh/zh-cn/) 包管理器