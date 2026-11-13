# 安全与隐私说明

## 支持版本

| 版本 | 支持 |
|---|---|
| 0.1.x | ✅ |
| < 0.1 | ❌ |

## 项目边界

- 不重新分发 Codex 桌面应用本体（见二进制包内 `THIRD_PARTY_NOTICES.txt`）。
- 按 `SKILL.md` 的工作流约束，不读取或上传账号、令牌、对话内容或项目文件，不修改 `app.asar`。
- 本仓库只提供文档与 Skill 描述；实际执行逻辑在 Release 附件的脚本中，**请在运行前自行审阅** `Codex-Zh-Installer.ps1` 与 `Codex-Zh-Tool.ps1`。

## 安装器会做什么

1. 备份后写入 `%USERPROFILE%\.codex\config.toml` 的 `[desktop] localeOverride = "zh-CN"`。
2. 修改 Codex 的 LevelDB 缓存以启用内置 `enable_i18n`。
3. 安装过程中关闭并重启 Codex / ChatGPT 桌面进程。

## 使用建议

- 只从本仓库 Releases 下载附件，并校验 `SHA256SUMS.txt`；不要使用第三方镜像。
- 保留 `backups/` 目录，直到确认界面与功能正常。
- 若客户端版本更新后出现异常，停止自动修复，按 `SKILL.md` 的失败处理流程从备份恢复。

## 报告问题

请勿在公开 issue 中粘贴令牌、账号、完整本机路径或对话内容。日志请先脱敏，仅保留错误码与首个失败点；涉及隐私的内容可通过 GitHub 私密渠道联系维护者。
