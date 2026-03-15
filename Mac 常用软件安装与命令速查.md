# Homebrew 安装
## 一、官方安装
Homebrew 是 macOS/Linux 缺失的软件包管理器，官方提供了一键安装命令，同时也有 `.pkg` 安装器可选，具体操作如下：
1. 打开终端，粘贴并执行以下官方安装脚本，脚本执行前会暂停并说明操作内容：
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
2. 若使用 macOS，也可选择官方最新 GitHub 发行版的 `.pkg` 安装器，下载地址：[https://brew.sh/zh-cn/](https://brew.sh/zh-cn/)

## 二、国内安装（清华源）
国内推荐使用清华大学镜像源安装 Homebrew，可解决官方源访问慢、连接失败等问题，镜像帮助文档地址：[https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)
（注：该镜像文档暂因网页解析问题无法获取具体内容，可直接访问上述链接查看清华源的安装、换源完整步骤）

# 三、查看本地网络代理
在终端中执行以下命令，可查看当前 macOS 系统的网络代理配置信息，排查 Homebrew 安装时的网络连接问题：
```bash
scutil --proxy
```

### 补充说明
Homebrew 核心特性：
- 安装软件包：`brew install 软件名`（如 `brew install wget`），安装 macOS 应用可使用 `brew install --cask 应用名`（如 `brew install --cask firefox`）
- 软件包会安装至独立目录，并软链接到 `/opt/homebrew`，不污染系统默认目录
- 基于 Git 和 Ruby 开发，支持自定义、修改软件包配方，可通过 `man brew` 查看完整官方文档
