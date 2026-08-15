# exeify-web2exe-skill（网页打包成 exe 的 AI 技能）

一个符合 **[Agent Skills 开放标准](https://agentskills.io)** 的技能：让 AI 助手把
「一个本地网页文件夹（HTML/CSS/JS）」或「一个在线网址」**一键打包成独立的 Windows `.exe`**，
双击即运行、免安装（用系统自带的 WebView2 渲染）。

底层由 [**Exeify**](https://github.com/44886/Exeify) 驱动，`exeify.exe` 已内置在本仓库中，
装好后离线即可用。

> **仅 Windows。** 内置的 `exeify.exe` 是 Windows 程序；产物依赖 WebView2（Win10/11 通常已内置）。

## 能做什么

跟你的 AI 助手说，比如：

- “把这个网页文件夹打包成 exe”
- “把 https://example.com 做成一个桌面程序，全屏启动”
- “把这个 HTML 文件夹做成带我图标的 Windows 应用”

AI 会自动调用 `exeify.exe pack ...`，产出一个自包含的 `.exe`。

## 安装（Claude Code）

把本仓库 clone 到你的 skills 目录，目录名用 `exeify-packer`：

```bash
git clone https://github.com/44886/exeify-web2exe-skill.git ~/.claude/skills/exeify-packer
```

Windows（PowerShell）：

```powershell
git clone https://github.com/44886/exeify-web2exe-skill.git "$env:USERPROFILE\.claude\skills\exeify-packer"
```

重启 Claude Code，技能 `exeify-packer` 即生效，当你要求“把网页/网址打包成 exe”时会自动加载。
（项目级安装：clone 到 `.claude/skills/exeify-packer`。）

## 安装（其它支持 Agent Skills 的 AI 工具）

这是标准的 Agent Skills 技能（一个 `SKILL.md` + 支持文件）。把本目录放到该工具发现技能的位置即可。

## 参数速查

AI 会自动拼命令。底层 CLI：

```
exeify.exe pack --local <目录> [--entry index.html] --out <app.exe> [选项...]
exeify.exe pack --url <网址>   --out <app.exe> [选项...]
```

选项：`--title 标题 --width 宽 --height 高 --window normal|maximized|fullscreen --no-resizable
--icon 图标(ico/png) --splash 启动图 --splash-bg #rrggbb --splash-sec 秒 --no-protect`。
`exeify.exe pack --help` 打印完整用法。成功打印 `OK: <路径>`（返回码 0）。

完整说明见 `SKILL.md`。

## 目录内容

| 文件 | 用途 |
|---|---|
| `SKILL.md` | 技能定义（Agent Skills frontmatter + 指令） |
| `exeify.exe` | 内置的 Exeify 打包器（Windows），技能调用的 CLI |
| `README.md` / `README.zh.md` | 英文 / 中文说明 |
| `LICENSE` | Apache-2.0 |

## 更新

Exeify 发新版后，用 [Exeify releases](https://github.com/44886/Exeify/releases) 的最新
`exeify.exe` 替换本目录里的即可。CLI 契约稳定（`exeify pack ...` → `OK: <路径>`）。

## 许可证

Apache-2.0。Exeify © 不坑老师 · https://github.com/44886/Exeify
