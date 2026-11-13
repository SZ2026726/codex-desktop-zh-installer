# codex-desktop-zh-installer

> 为 Windows 版 Codex Desktop 安装、校验与修复简体中文界面的 Skill 与脚本说明。
> Skill and scripts for enabling the built-in Simplified Chinese UI of Codex Desktop on Windows.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 非官方声明 / Disclaimer

本项目与 OpenAI、Microsoft 无任何关联，也未经其授权或认可。`Codex`、`OpenAI` 为各自权利人的商标，本仓库仅作指代性使用。

本项目**不包含、也不重新分发 Codex 桌面应用本体**；它会修改本机已安装客户端的两处状态（见下）。使用前请自行确认该操作不违反你所适用的软件条款，风险由使用者承担。

## 仓库内容

| 路径 | 说明 |
|---|---|
| `SKILL.md` | 供 AI 代理使用的安装 / 排障工作流 |
| `agents/openai.yaml` | Skill 的展示名称与简介 |
| `assets/SHA256SUMS.txt` | Release 附件的 SHA-256 校验值 |
| `docs/RELEASE-NOTES.md` | Release 说明与附件上传步骤 |
| `Codex-Desktop-Zh-Portable.zip` | **不在仓库内**，请从 Releases 下载 |

二进制包（约 37 MB）作为 GitHub Release 附件单独提供，内含：

- 自写的 PowerShell / JavaScript 安装与排障脚本
- 便携版 Node.js 运行时（`runtime/node.exe`）及 npm 依赖（classic-level 等）
- `THIRD_PARTY_NOTICES.txt` 与 `runtime/NODE-LICENSE.txt`

各第三方组件保留其原始许可证。本仓库的 MIT 许可证**仅覆盖仓库内的原创文档与 Skill 描述，不覆盖上述第三方二进制**。

## 适用范围

- Windows 10 / 11，**Microsoft Store 版** Codex Desktop
- 主要验证版本：`OpenAI.Codex 26.1106.6628.0`
- 不适用于 macOS、Linux，也不用于修改 ChatGPT 网页版语言

## 它会改动什么

按 `SKILL.md` 的描述，安装前先备份，然后修改两处本机状态：

1. `%USERPROFILE%\.codex\config.toml` 中的 `[desktop] localeOverride = "zh-CN"`
2. Codex 自身的 LevelDB 缓存，用于启用内置的 `enable_i18n`

安装器会**关闭正在运行的 ChatGPT / Codex 桌面进程**，请先保存工作。工作流约束要求不读取或上传账号、令牌、对话或项目内容，也不修改 `app.asar`；运行前请自行审阅脚本。

## 快速开始

1. 到 Releases 下载 `Codex-Desktop-Zh-Portable.zip` 与 `SHA256SUMS.txt`。
2. 校验完整性：

   ```powershell
   Get-FileHash .\Codex-Desktop-Zh-Portable.zip -Algorithm SHA256
   ```

   与 `assets/SHA256SUMS.txt` 中的值比对。
3. 在 Windows 上解压到本地目录。
4. **若当前对话正运行在 Codex Desktop 内**：不要让代理直接启动安装器（会关闭进程、中断会话），请在文件资源管理器中双击 `Codex-一键汉化.cmd`。
5. 其他情况可执行：

   ```powershell
   powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\Codex-Zh-Installer.ps1
   ```

6. 日志出现 `[OK] 注入完成，自检通过` 即成功；失败处理见 `SKILL.md`。

> 供 AI 代理使用时：将 `SKILL.md`、`agents/openai.yaml` 放入对应 Skill 目录，并把解压得到的 `Codex-Desktop-Zh-Portable.zip` 放到 `assets/` 下。

## 已知问题

- 压缩包内部分中文文件名在部分解压工具下显示为乱码；若找不到 `Codex-一键汉化.cmd`，直接运行 `Codex-Zh-Installer.ps1`。
- 压缩包内路径使用 Windows 反斜杠分隔符，在非 Windows 工具中可能显示为单个长文件名，建议在 Windows 上解压。
- Codex 客户端版本更新后，LevelDB 结构或内置中文资源可能变化；脚本会停止自动修复并报告日志中的首个失败点。

## 隐私与安全

详见 [SECURITY.md](SECURITY.md)。提交 issue 时请勿粘贴含个人信息、令牌或完整本机路径的日志。

## 贡献

见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 许可证

[MIT](LICENSE) © 2026 `SZ2026726`。第三方组件许可证见二进制包内 `THIRD_PARTY_NOTICES.txt`。

---

**English (short):** Unofficial, MIT-licensed Skill and scripts that enable the built-in Simplified Chinese UI of the Microsoft Store version of Codex Desktop on Windows 10/11. The desktop application itself is **not** redistributed. The portable binary bundle (Node.js runtime + scripts) is published separately as a GitHub Release asset. It modifies local `config.toml` and LevelDB state after taking backups — review the scripts and use at your own risk.
