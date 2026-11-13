---
name: codex-desktop-zh-installer
description: Install or troubleshoot the built-in Simplified Chinese interface for Codex Desktop on Windows using a bundled, reversible package with config and LevelDB backups. Do not use for macOS, Linux, or ordinary ChatGPT web language settings.
---

# Codex Desktop 简体中文安装与排障

用于 Windows 10/11 上 Microsoft Store 版 Codex Desktop 的简体中文界面安装、修复和排障。只处理用户明确要求“汉化 Codex 桌面版界面”的情况；不要用于修改普通 ChatGPT 网页语言，也不要用于 macOS/Linux。

## 先说明影响

安装会修改两项本机状态：

- `%USERPROFILE%\.codex\config.toml` 中的 `[desktop] localeOverride = "zh-CN"`
- Codex 自己的 LevelDB 缓存，用于启用内置的 `enable_i18n`

安装前必须备份。不要修改或重新打包 Codex 的 `app.asar`，不要读取或上传账号、令牌、对话或项目内容。

## 关键限制

如果当前对话正运行在 Codex Desktop 内，不要让代理直接启动安装器：安装器会关闭 ChatGPT/Codex 桌面进程，从而中断当前会话。

此时应解压载具并让用户在文件资源管理器中双击：

```text
Codex-一键汉化.cmd
```

如果当前环境与 Codex Desktop 进程无关，才能直接执行：

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\Codex-Zh-Installer.ps1
```

## 工作流

1. 读取 `assets/Codex-Desktop-Zh-Portable.zip`，解压到临时目录。
2. 确认目标为 Microsoft Store 版 Codex Desktop，并记录版本。
3. 向用户说明脚本会关闭应用、备份配置和 LevelDB，然后重启应用；取得授权后再执行。
4. 优先让用户双击 `Codex-一键汉化.cmd`。不要从正在承载当前会话的 Codex 进程里直接运行。
5. 脚本成功后，日志应包含 `[OK] 注入完成，自检通过`。
6. 检查 config 中只有一处 `localeOverride = "zh-CN"`，并确认 Codex 已重新启动。

## 失败处理

先读取解压目录下最新的 `logs\i18n-*.log`，不要盲目重复执行。

- 找不到 stableID：确认脚本通过 LevelDB 历史数据读取 `statsig.stable_id`。
- 注入自检失败：从 `backups\leveldb.*` 恢复备份，不要继续写入。
- 界面仍为英文：先检查 config 和备份，再检查应用是否完全重启。
- 版本或界面结构明显变化：停止自动修复，报告版本和日志中的首个失败点。

## 适用范围

当前主要验证版本为 Microsoft Store 版 `OpenAI.Codex 26.1106.6628.0`。其他版本可以尝试，但必须先确认日志显示官方中文资源和 LevelDB 结构仍匹配。
