# 贡献指南

欢迎提交 issue 与 PR。请先看 [SECURITY.md](SECURITY.md) 中的隐私边界。

## 提交 issue

请包含：

- Codex Desktop 版本（`设置 → 关于`，或 Microsoft Store 应用版本）
- Windows 版本（10 / 11，具体内部版本号）
- 复现步骤
- `logs/i18n-*.log` 中**首个失败点**（脱敏后）

请勿粘贴：账号、令牌、对话内容、项目代码、含真实用户名的完整路径。

## 提交 PR

- 不要提交任何二进制文件（`.zip` / `.exe` / `.node`），Release 附件由维护者在网页端上传。
- 不要改动第三方依赖及其许可证文件。
- 修改 `SKILL.md` 的工作流时，同步更新 README 的对应章节。
- 涉及版本号变化时更新 `CHANGELOG.md`。
- 提交信息用简短中文或英文，说明「改了什么、为什么」。

## 本地检查

```powershell
# 校验 Release 附件的哈希
Get-FileHash .\Codex-Desktop-Zh-Portable.zip -Algorithm SHA256
```

## 行为准则

就事论事，不发布人身攻击、广告或与项目无关的内容。
