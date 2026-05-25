# AutoGithubHosts

> 自动更新 GitHub Hosts — 轻量 · 易用 · 安全 · 零依赖 · 跨平台 · 多架构

## 声明

- 本仓库（`AutoGithubHosts_Release`）**仅用于分发预编译二进制文件**，不包含任何源代码。
- 任何人都可以**免费下载和使用**，但不得进行反编译、逆向工程或未经授权的二次分发。
- 本项目按"原样"提供，不提供任何明示或暗示的担保。使用本软件即表示您同意自行承担所有风险。

---

## 简介

AutoGithubHosts 是一个跨平台的 GitHub Hosts 自动更新工具，帮助用户解决 GitHub 访问不稳定、速度慢等问题。

### 核心特点

| 特点 | 说明 |
|------|------|
| 🪶 **轻量**   | 单文件二进制，体积 < 5MB                    |
| ✨ **易用**   | 运行即用，默认配置文件自动生成，无需人工干预      |
| 🔒 **安全**   | 仅修改 Hosts 文件中标记块，不触碰用户其他条目   |
| 📦 **零依赖** | 纯 Go 标准库实现，无需安装任何运行环境        |
| 🌍 **跨平台** | Windows / Linux / macOS              |
| 🖥️ **多架构** | amd64 / arm64                      |

---

## 快速开始

### 1. 下载

从 [Releases](https://github.com/Positive521/AutoGithubHosts_Release/releases) 页面下载对应平台的二进制文件或完整包。

| 平台 | 完整包格式 |
|------|-----------|
| Windows | `.zip`（含 `conf/config.json`） |
| Linux | `.tar.gz`（含 `conf/config.json`） |
| macOS | `.tar.gz`（含 `conf/config.json`） |

### 2. 运行

> **需要管理员/root 权限**（修改系统 Hosts 文件所需）

```bash
# Windows（以管理员身份运行）
AutoGithubHosts.exe

# Linux
sudo ./AutoGithubHosts

# macOS
sudo ./AutoGithubHosts
```

### 3. 验证

启动后控制台输出：

```
AutoGithubHosts v1.0.0
配置文件: /xxxx/conf/config.json
日志文件: /xxxx/log/AutoGithubHosts.log
更新间隔: 30m
后台守护进程已启动，PID: 12345
```

---

## 使用说明

```
AutoGithubHosts [选项]

  -c <path>    配置文件路径 (默认: conf/config.json)
  -once        单次更新后退出（前台运行）
  -v           显示版本信息
  -h, -help    显示帮助信息
```

### 常用场景

```bash
# 后台守护模式（默认，启动后立即转入后台）
sudo ./AutoGithubHosts

# 单次更新并退出（前台运行，可观察输出）
sudo ./AutoGithubHosts -once

# 查看版本
./AutoGithubHosts -v
```

### 停止守护进程

程序不占用终端，Ctrl+C 无效，需通过 PID 终止：

```bash
# Windows
taskkill /PID <PID> /F

# Linux / macOS
kill <PID>
```

> 启动时控制台会打印 PID。

---

## 目录结构

```
AutoGithubHosts/
├── AutoGithubHosts(.exe)     # 可执行文件
├── conf/
│   └── config.json           # 配置文件（首次运行自动生成）
└── log/
    └── AutoGithubHosts.log   # 运行日志
```

---

## 配置说明

首次运行自动生成 `conf/config.json`，可按需编辑：

```json
{
    "github_hosts_url": "https://raw.hellogithub.com/hosts",
    "update_interval": "30m",
    "auto_start": true
}
```

| 字段 | 说明 | 默认值 |
|------|------|--------|
| `github_hosts_url` | GitHub Hosts 远程源地址 | `https://raw.hellogithub.com/hosts` |
| `update_interval` | 自动更新间隔 | `30m`（支持 `1h`、`2h30m` 等） |
| `auto_start` | 是否开机自启动 | `true` |

### 开机自启动

通过 `auto_start` 配置项控制，程序启动时自动同步——设为 `true` 则注册，`false` 则注销。修改配置后重启程序即可生效。

---

## 文件校验

每次 Release 均附带 `SHA256SUMS.txt`，可通过以下命令验证下载文件的完整性：

```bash
sha256sum -c SHA256SUMS.txt          # Linux / macOS
certutil -hashfile xxx.exe SHA256    # Windows
```

---

## 关于本仓库

本仓库仅用于分发预编译的二进制文件，所有版本均由 GitHub Actions 自动构建并发布。

---

## 问题反馈

如遇到问题或有功能建议，欢迎通过以下方式联系：

| 方式 | 说明 |
|------|------|
| 📝 **GitHub Issue** | [提交 Issue](https://github.com/Positive521/AutoGithubHosts_Release/issues) |
| 📧 **邮件** | iii77989@hotmail.com |

> 提交 Issue 时请附带运行日志（`log/AutoGithubHosts.log`）和相关错误信息，以便快速定位问题。

---

## 免责声明

1. AutoGithubHosts 是一款**免费软件**，永久免费使用，无需付费。
2. 本项目出于安全考虑**无法开源**，源代码不公开，受版权法保护。禁止反编译、逆向工程、修改或未经授权的二次分发。
3. 本软件仅修改系统 Hosts 文件中的标记区域（`# AutoGithubHosts Start` ~ `# AutoGithubHosts End`），不会修改系统其他配置。
4. 使用者应遵守当地法律法规，本软件仅供学习和技术交流使用。
5. 开发者不承担因使用本软件造成的任何直接或间接损失。

