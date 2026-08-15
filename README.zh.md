# exeify-web2exe-skill（网页打包成 exe 的 AI 技能）

<p align="center"><img src="doc/cover.png" width="620" alt="Exeify 网页转 exe" /></p>

一个符合 **[Agent Skills 开放标准](https://agentskills.io)** 的技能（并打包为 Claude Code 插件）：
让 AI 助手把「一个本地网页文件夹（HTML/CSS/JS）」或「一个在线网址」**一键打包成独立的
Windows `.exe`**，双击即运行、免安装（用系统自带的 WebView2 渲染）。

底层由 [**Exeify**](https://github.com/44886/Exeify) 驱动，`exeify.exe` 已内置，装好后离线即可用。

> **仅 Windows。** 内置的 `exeify.exe` 是 Windows 程序；产物依赖 WebView2（Win10/11 通常已内置）。

## 能做什么

直接跟你的 AI 助手说，比如：

- “把这个网页文件夹打包成 exe”
- “把 https://example.com 做成一个桌面程序，全屏启动”
- “把这个 HTML 文件夹做成带我图标的 Windows 应用”

AI 会自动调用 `exeify.exe pack ...`，产出一个自包含的 `.exe`。

## 安装 —— 一键（Claude Code）

把本仓库加为插件市场，再装插件：

```
/plugin marketplace add 44886/exeify-web2exe-skill
/plugin install exeify-web2exe@exeify
```

装好即可。之后你要求“把网页/网址打包成 exe”时，技能会自动加载。

<details>
<summary>备选：当作普通技能安装（任意支持 Agent Skills 的工具）</summary>

把技能目录复制到你的工具发现技能的位置。Claude Code：

```bash
git clone https://github.com/44886/exeify-web2exe-skill.git /tmp/exeify-skill
cp -r /tmp/exeify-skill/plugins/exeify-web2exe/skills/exeify-web2exe ~/.claude/skills/exeify-web2exe
```

技能就是标准的 `SKILL.md` + 内置 `exeify.exe`，任何支持
[Agent Skills](https://agentskills.io) 标准的工具都能加载。
</details>

## 参数速查

AI 会自动拼命令。底层 CLI：

```
exeify.exe pack --local <目录> [--entry index.html] --out <app.exe> [选项...]
exeify.exe pack --url <网址>   --out <app.exe> [选项...]
```

选项：`--title 标题 --width 宽 --height 高 --window normal|maximized|fullscreen --no-resizable
--icon 图标(ico/png) --splash 启动图 --splash-bg #rrggbb --splash-sec 秒 --no-protect`。
`exeify.exe pack --help` 打印完整用法。成功打印 `OK: <路径>`（返回码 0）。

## 目录结构

```
.claude-plugin/marketplace.json                 # 市场清单
plugins/exeify-web2exe/
├── .claude-plugin/plugin.json                  # 插件清单
└── skills/exeify-web2exe/
    ├── SKILL.md                                # 技能定义（给 AI 的指令）
    └── exeify.exe                              # 内置 Exeify 打包器（Windows）
doc/cover.png · README.md · README.zh.md · LICENSE
```

## 更新

Exeify 发新版后，用 [Exeify releases](https://github.com/44886/Exeify/releases) 最新的
`exeify.exe` 替换 `plugins/exeify-web2exe/skills/exeify-web2exe/exeify.exe` 即可。
CLI 契约稳定（`exeify pack ...` → `OK: <路径>`）。

## 许可证

Apache-2.0。Exeify © 不坑老师 · https://github.com/44886/Exeify
