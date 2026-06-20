# 枢子 AgentBot 公开发布仓库

这是枢子 AgentBot 的公开发布仓库，用于向用户提供安装包、便携包、更新清单、签名文件和校验和文件。

本仓库面向最终用户下载和客户端自动更新，不承载源码开发、Issue 跟踪或功能分支协作内容。

## 产品简介

枢子 AgentBot 是一个面向 Windows 用户的 AI 工具安装、配置与管理助手。它的目标不是让用户手动到处找安装包、命令和教程，而是把常用 AI 工具的检测、安装引导、配置检查、更新提醒和日志排障放到同一个桌面软件里。

核心能力包括：

- 检测本机基础环境，例如 Node.js、npm、Git、Python、PowerShell、Windows 相关组件。
- 识别已安装的 AI 工具，并在软件内展示当前状态。
- 对 CLI 类稳定工具提供自动安装或半自动安装能力。
- 对 Desktop、WSL 等不稳定或强依赖系统环境的工具提供明确提示、手动安装入口和失败原因说明。
- 提供安装日志、失败提示、手动教程入口，便于用户按步骤排查。
- 提供更新提醒和更新内容说明，方便已安装用户及时拿到新版本。
- 支持安装包签名更新清单，供客户端进行版本检查和更新校验。

## 下载地址

请从 Releases 页面下载最新版本：

[https://github.com/id100w/shuziai-agent/releases](https://github.com/id100w/shuziai-agent/releases)

Windows 用户优先下载：

- `ShuziAgentBot-vX.Y.Z-Windows-Setup.exe`：标准安装包，推荐普通用户使用。
- `ShuziAgentBot-vX.Y.Z-Windows-Portable.zip`：便携包，适合不想走安装流程或需要临时测试的用户。
- `SHA256SUMS.txt`：文件 SHA256 校验和，用于确认下载文件未损坏。
- `latest.json`：客户端更新清单，供软件内更新功能使用。
- `ShuziAgentBot-vX.Y.Z-Windows-Setup.exe.sig`：安装包更新签名文件，供 updater 校验使用。

## 推荐安装方式

1. 打开 Releases 页面。
2. 选择最新版本。
3. 下载 `Windows-Setup.exe` 安装包。
4. 双击安装包并按提示完成安装。
5. 首次启动后，根据软件内向导完成授权、模型和工具配置。

如果安装失败，建议优先查看软件内日志和手动安装教程入口。安装失败通常与 Microsoft Store 登录状态、网络访问、系统权限、代理、杀毒软件拦截或本机环境缺失有关。

手动安装教程：

[https://ivjyskqhcs1.feishu.cn/wiki/Bx0YwVqlRiQnPJkCEqZcL9lPngc](https://ivjyskqhcs1.feishu.cn/wiki/Bx0YwVqlRiQnPJkCEqZcL9lPngc)

## 更新机制

客户端会从本仓库读取更新信息：

- 最新 Release API：`https://api.github.com/repos/id100w/shuziai-agent/releases/latest`
- Tauri updater manifest：`https://github.com/id100w/shuziai-agent/releases/latest/download/latest.json`

当有新版本发布时，客户端会根据更新清单显示版本号、更新内容和可用安装包。带签名的安装包会配套 `.sig` 文件，供更新流程进行校验。

如果旧版本无法自动弹出更新，请手动下载最新安装包覆盖安装一次。完成后，后续版本会继续走新的公开发布仓库检查更新。

## 文件校验

下载完成后，可以使用 `SHA256SUMS.txt` 校验文件完整性。

PowerShell 示例：

```powershell
Get-FileHash .\ShuziAgentBot-vX.Y.Z-Windows-Setup.exe -Algorithm SHA256
```

将输出的哈希值与 Release 附件中的 `SHA256SUMS.txt` 对比即可。

## 常见问题

### 1. 安装包下载很慢

可能是 GitHub 网络访问不稳定。可以稍后重试，或使用项目提供的手动安装教程。

### 2. 安装 Desktop 工具失败

部分 Desktop 工具依赖 Microsoft Store、官方安装源、系统登录状态或外部网络访问。软件会尽量自动尝试，但这类工具不保证所有环境都能一键成功。遇到失败时，请优先查看日志提示和手动教程。

### 3. CLI 工具安装失败

CLI 工具通常更适合自动安装，但仍可能受网络、npm registry、权限、代理或杀毒软件影响。建议先确认网络连通、终端权限和本机 Node.js/npm 状态。

### 4. 更新弹窗没有出现

请确认当前版本是否已经接入本公开发布仓库。如果是较早版本，可能仍指向旧更新源，需要手动安装一次新版本。

### 5. 安装包被安全软件拦截

请先确认下载来源是本仓库 Releases 页面，并核对 SHA256。不同安全软件策略不同，如仍被拦截，可先使用便携包进行测试。

## 发布内容说明

每个正式版本通常包含：

- Windows 安装包
- Windows 便携包
- SHA256 校验文件
- updater 签名文件
- updater 更新清单
- 本次版本更新说明

版本号采用 `vX.Y.Z` 格式。建议普通用户始终使用最新正式版本。
