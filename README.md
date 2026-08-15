# exeify-web2exe-skill

> 🇨🇳 中文说明见 **[README.zh.md](README.zh.md)**

<p align="center"><img src="doc/cover.png" width="620" alt="Exeify Web→exe" /></p>

An **[Agent Skills](https://agentskills.io)** skill (packaged as a Claude Code plugin) that lets an
AI assistant package a website — a local HTML/CSS/JS folder **or** an online URL — into a
**standalone Windows `.exe`** that double-clicks to run with no install (renders via the system WebView2).

Powered by [**Exeify**](https://github.com/44886/Exeify). The Exeify CLI (`exeify.exe`) is bundled,
so it works offline once installed.

> **Windows only.** The bundled `exeify.exe` is a Windows executable; packed apps rely on WebView2,
> which is built into Windows 10/11.

## What it does

Just ask your AI assistant, e.g.:

- “把这个网页文件夹打包成 exe” / “package this website folder into an exe”
- “把 https://example.com 做成一个桌面程序，全屏启动”
- “turn this HTML folder into a Windows app with my icon”

The skill drives `exeify.exe pack ...` and produces a self-contained `.exe`.

## Install — one click (Claude Code)

Add this repo as a plugin marketplace, then install the plugin:

```
/plugin marketplace add 44886/exeify-web2exe-skill
/plugin install exeify-web2exe@exeify
```

Done. The skill loads automatically when you ask to package a website into an exe.

<details>
<summary>Alternative: install as a plain skill (any Agent Skills tool)</summary>

Copy the skill directory into where your tool discovers skills. For Claude Code:

```bash
git clone https://github.com/44886/exeify-web2exe-skill.git /tmp/exeify-skill
cp -r /tmp/exeify-skill/plugins/exeify-web2exe/skills/exeify-web2exe ~/.claude/skills/exeify-web2exe
```

The skill is a standard `SKILL.md` + bundled `exeify.exe`, so any tool supporting the
[Agent Skills](https://agentskills.io) standard can load it.
</details>

## Usage / CLI

The AI assembles the command for you. Under the hood:

```
exeify.exe pack --local <dir> [--entry index.html] --out <app.exe> [options]
exeify.exe pack --url <url>   --out <app.exe> [options]
```

Options: `--title --width --height --window normal|maximized|fullscreen --no-resizable
--icon <ico|png> --splash <img> --splash-bg <#rrggbb> --splash-sec <s> --no-protect`.
Run `exeify.exe pack --help` for the full list. Success prints `OK: <path>` (exit 0).

## Layout

```
.claude-plugin/marketplace.json                 # marketplace manifest
plugins/exeify-web2exe/
├── .claude-plugin/plugin.json                  # plugin manifest
└── skills/exeify-web2exe/
    ├── SKILL.md                                # the skill (instructions for the AI)
    └── exeify.exe                              # bundled Exeify packer (Windows)
doc/cover.png · README.md · README.zh.md · LICENSE
```

## Updating

When a new Exeify version ships, replace `plugins/exeify-web2exe/skills/exeify-web2exe/exeify.exe`
with the latest from [Exeify releases](https://github.com/44886/Exeify/releases). The CLI contract
is stable (`exeify pack ...` → `OK: <path>`).

## License

Apache-2.0. Exeify © 不坑老师 · https://github.com/44886/Exeify
