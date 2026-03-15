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


以下是 Mac 上主流网络抓包工具的完整集合，包含**安装步骤、核心功能、优缺点、适用场景**与**横向对比表**，覆盖 GUI 代理、命令行、底层协议、移动端专用四大类。

---

## 一、HTTP/HTTPS 代理抓包（Web/APP/小程序首选）
### 1. Proxyman（macOS 原生，现代 GUI）
- **安装**
  ```bash
  brew install --cask proxyman
  ```
- **核心功能**
  - 原生 Apple Silicon 优化、界面流畅
  - HTTPS 解密、断点、重写、Mock、重放
  - iOS USB 直连抓包、自动证书配置
  - 瀑布图、性能分析、多标签管理
- **优缺点**
  - ✅ 免费版够用、原生体验好、证书配置简单
  - ❌ 仅 macOS、高级功能需订阅
- **适用**：macOS 日常 HTTP/HTTPS 调试、iOS 开发

### 2. Charles（经典跨平台，稳定可靠）
- **安装**
  ```bash
  brew install --cask charles
  ```
- **核心功能**
  - 跨平台（macOS/Windows/Linux）
  - HTTPS 解密、断点、Map Local/Remote、弱网模拟
  - 手机抓包友好、生态成熟
- **优缺点**
  - ✅ 稳定、功能全、社区资料多
  - ❌ 收费（约 $50）、界面旧、内存占用高
- **适用**：跨平台开发、需要稳定 Mock/重写

### 3. Fiddler Everywhere（微软出品，免费基础版）
- **安装**
  ```bash
  brew install --cask fiddler-everywhere
  ```
- **核心功能**
  - 免费版够用、界面现代
  - 规则配置、HTTPS 解密、请求重放
  - 跨平台、新手友好
- **优缺点**
  - ✅ 免费、微软背书、上手快
  - ❌ 高级功能付费、性能一般
- **适用**：新手、免费需求、跨平台统一工具

### 4. mitmproxy（命令行+脚本，开发者向）
- **安装**
  ```bash
  brew install mitmproxy
  ```
- **核心功能**
  - 完全开源免费、Python 脚本自定义流量
  - 命令行（mitmproxy）+ Web UI（mitmweb）
  - 支持 HTTPS、WebSocket、批量修改
- **优缺点**
  - ✅ 脚本化、自动化、无 GUI 环境可用
  - ❌ 学习成本高、证书/代理配置繁琐
- **适用**：自动化测试、批量处理、服务器抓包

---

## 二、底层协议抓包（网络层/传输层，深度排查）
### 1. Wireshark（全能开源，底层抓包之王）
- **安装**
  ```bash
  brew install wireshark
  ```
- **核心功能**
  - 免费开源、支持所有协议（TCP/UDP/HTTP/HTTPS/DNS/WebSocket）
  - 全系统流量捕获、深度数据包解析
  - 强大过滤、着色规则、导出分析
- **优缺点**
  - ✅ 全协议、免费、跨平台
  - ❌ HTTPS 默认不解密（需 SSLKEYLOG）、界面复杂
- **适用**：网络故障排查、协议学习、非 HTTP 流量分析

### 2. tcpdump（命令行底层抓包，服务器必备）
- **安装**：macOS 内置，无需安装
- **核心功能**
  - 轻量无 GUI、远程服务器抓包
  - 强大过滤语法、保存为 pcap 供 Wireshark 分析
- **常用命令**
  ```bash
  # 抓 en0 网卡 8080 端口
  sudo tcpdump -i en0 port 8080 -w capture.pcap
  ```
- **优缺点**
  - ✅ 轻量、内置、适合无 GUI 环境
  - ❌ 无图形界面、需命令行操作
- **适用**：服务器抓包、快速捕获、无桌面环境

---

## 三、移动端专用抓包（iOS/Android）
### 1. iOS：Thor / Stream
- **Thor**：功能强大、重写/Mock、付费
- **Stream**：免费、基础抓包、新手友好
- **安装**：App Store 搜索安装

### 2. Android：HttpCanary（小黄鸟）
- **安装**：官网/应用商店下载
- **功能**：无需 root、HTTPS 解密、界面友好
- **适用**：安卓 APP 本地调试

---

## 四、功能对比总表（Mac 场景）
| 工具 | 类型 | 平台 | 价格 | HTTPS 解密 | 脚本/自动化 | 移动端抓包 | 核心亮点 | 适合场景 |
|---|---|---|---|---|---|---|---|---|
| Proxyman | GUI 代理 | macOS | 免费+订阅 | 简单 | 有限 | iOS USB | 原生流畅、Apple Silicon | macOS 日常调试 |
| Charles | GUI 代理 | 全平台 | 付费 | 中等 | 有限 | 优秀 | 稳定、生态成熟 | 跨平台、Mock/重写 |
| Fiddler Everywhere | GUI 代理 | 全平台 | 免费+付费 | 简单 | 有限 | 良好 | 免费、界面现代 | 新手、免费需求 |
| mitmproxy | 命令行+Web | 全平台 | 开源免费 | 中等 | 极强 | 一般 | 脚本化、自动化 | 开发者、批量处理 |
| Wireshark | 底层协议 | 全平台 | 开源免费 | 需配置 | 有限 | 一般 | 全协议、深度解析 | 网络排查、协议分析 |
| tcpdump | 命令行底层 | macOS/Linux | 免费 | 不支持 | 脚本 | 无 | 轻量、服务器 | 远程抓包、无 GUI |
| Thor/Stream | iOS 专用 | iOS | 免费+付费 | 简单 | 有限 | 极强 | iOS 原生 | iOS APP 调试 |
| HttpCanary | Android 专用 | Android | 免费+付费 | 简单 | 有限 | 极强 | 无需 root | 安卓 APP 调试 |

---

## 五、安装与 HTTPS 配置要点（通用）
### 1. 代理抓包工具（Proxyman/Charles/Fiddler/mitmproxy）
1. 安装工具并启动
2. 工具会自动配置系统代理（或手动设为 `127.0.0.1:8888`）
3. 安装根证书：工具内导出证书 → 双击安装到钥匙串 → 设为**始终信任**
4. 移动端：连接同一 Wi-Fi → 手动代理 → 安装证书并信任

### 2. Wireshark HTTPS 解密
1. 浏览器/客户端导出 `SSLKEYLOGFILE`
2. Wireshark → 偏好设置 → Protocols → TLS → 导入密钥日志文件

---

## 六、推荐组合（Mac 开发）
- **日常 HTTP/APP 抓包**：Proxyman（免费版）或 Charles
- **自动化/脚本化**：mitmproxy
- **底层网络排查**：Wireshark + tcpdump
- **移动端**：iOS 用 Thor/Stream，Android 用 HttpCanary
