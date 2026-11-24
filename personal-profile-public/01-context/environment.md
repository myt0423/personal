# 01 · 环境（设备 / 系统 / 软件栈）

> 公开层版本：已去掉设备标识（主机名、账户名）、邮箱、社交账号 ID。
> 目的只是让 AI 知道**我有什么工具、没有什么工具**，别建议我先 `npm install`。

## 主力机

- **系统**：Windows 11（内核 10.0.26100），中文
- **权限**：管理员账户（装机、改系统级别的事能做）
- **工作目录**：`%USERPROFILE%\Documents\deepseek-harness\default-workspace`

## 已装工具

| 工具 | 版本 / 路径 | 备注 |
| --- | --- | --- |
| DeepSeek Harness（桌面） | 4.x，装在非系统盘 | `DSH_HOME=%USERPROFILE%\.dsh`，profile = `desktop` |
| dsh 插件 · Purge | `dsh-purge-community` 1.7.20 | 装在 `profiles\desktop\node_modules` |
| bun | 1.4.5，`%USERPROFILE%\.dsh\tools\bun-portable` | 当 JS 运行时用 |
| Electron 内置 node | v24.21.0（`ELECTRON_RUN_AS_NODE=1` 跑 Harness.exe） | 系统没有独立 node |
| 微信 | 4.2.1.8 | 仅桌面端 |

## 系统里**没有**的（别让我装，先想替代）

- `git` / `gh`：未安装 → 需要用 Git 时先装 Git for Windows 或用网页端
- 独立 `node` / `npm` / `pnpm`：未安装 → 跑 JS 用 bun 或 `ELECTRON_RUN_AS_NODE`
- `sqlite3` / `sqlcipher` / `openssl` 命令行：未安装 → 用 `winsqlite3.dll` 或 .NET
- `ffmpeg`：**未安装**（已实测）→ 需要转码/抽帧时先想替代方案

## 设备

| 设备 | 用途 | 同步方式 |
| --- | --- | --- |
| Windows 11 主机 | 主力，所有干活都在这 | 本地 |
| 安卓手机 · dsh-go | 远程连主机 / 手机本机引擎 | SSH 或 relay |

## 常用命令速查

```powershell
# DSH 会话环境
$env:DSH_HOME; $env:DSH_PROFILE

# 用 bun 跑 JS
& "$env:USERPROFILE\.dsh\tools\bun-portable\package\bin\bun.exe" script.js

# 用 Electron 当 node
$env:ELECTRON_RUN_AS_NODE="1"; & "<DSH 安装目录>\DeepSeek Harness.exe" script.js

# Purge 状态
& $bun "$env:DSH_HOME\profiles\desktop\node_modules\dsh-purge-community\bin\community.js" selfcheck
```
