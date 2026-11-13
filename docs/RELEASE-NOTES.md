# v0.1.0 Release 说明（草稿）

> 本文件供维护者发布 Release 时参考，不作为安装说明。

## 附件清单（需在网页端手动上传）

| 文件 | 大小（字节） | SHA-256 |
|---|---|---|
| `Codex-Desktop-Zh-Portable.zip` | 37,861,246 | `CE30BA83FEF9CA847FCAFB0C6FFB2BFDF6A327D72C0B2C21C762F74982B7DE7A` |
| `SHA256SUMS.txt` | 97 | — |

发布前请重新执行一次校验，确认与上表一致：

```powershell
Get-FileHash .\Codex-Desktop-Zh-Portable.zip -Algorithm SHA256
```

## 上传步骤

1. 仓库页面 → **Releases** → **Draft a new release**。
2. Tag 填 `v0.1.0`，Target 选 `main`。
3. Title 填 `v0.1.0 — 初始版本`。
4. 正文粘贴下方模板。
5. 在 **Attach binaries by dropping them here or selecting them** 处上传上述两个文件。
6. 确认可见性为 Public，点击 **Publish release**。

> 附件体积约 37 MB，GitHub 单个 Release 附件上限为 2 GB，可正常上传。

## Release 正文模板

```markdown
## 初始版本

为 Windows 10/11 上 Microsoft Store 版 Codex Desktop 启用内置简体中文界面。

**适用范围**
- 主要验证版本：OpenAI.Codex 26.1106.6628.0
- 不适用于 macOS / Linux / ChatGPT 网页版

**使用前**
- 下载后请先校验 SHA256SUMS.txt
- 安装会关闭并重启 Codex 桌面进程，请先保存工作
- 脚本会备份并修改 config.toml 与 LevelDB 缓存，运行前请自行审阅

**已知问题**
- 部分解压工具下中文文件名显示乱码，可直接运行 Codex-Zh-Installer.ps1
- 建议在 Windows 上解压（包内使用反斜杠路径）

本项目与 OpenAI / Microsoft 无关联，不重新分发 Codex 桌面应用本体。
```

## 上传前检查

- [ ] 二进制包内不含本机日志、备份、账号或令牌
- [ ] `THIRD_PARTY_NOTICES.txt` 与 `runtime/NODE-LICENSE.txt` 仍在包内
- [ ] 哈希值与 `assets/SHA256SUMS.txt` 一致
- [ ] 已确认有权公开分发所含的 Node.js 运行时与 npm 依赖
