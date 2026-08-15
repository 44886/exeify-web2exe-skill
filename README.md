# exeify-web2exe-skill

> 🇨🇳 中文说明见 **[README.zh.md](README.zh.md)**

An **[Agent Skills](https://agentskills.io)** skill that lets an AI assistant package a website —
a local HTML/CSS/JS folder **or** an online URL — into a **standalone Windows `.exe`** that
double-clicks to run with no install (renders via the system WebView2).

Powered by [**Exeify**](https://github.com/44886/Exeify). The Exeify CLI (`exeify.exe`) is bundled
in this repo, so the skill works offline once installed.

> **Windows only.** The bundled `exeify.exe` is a Windows executable; packed apps rely on WebView2,
> which is built into Windows 10/11.

## What it does

Ask your AI assistant something like:

- “把这个网页文件夹打包成 exe” / “package this website folder into an exe”
- “把 https://example.com 做成一个桌面程序，全屏启动”
- “turn this HTML folder into a Windows app with my icon”

The skill drives `exeify.exe pack ...` and produces a self-contained `.exe`.

## Install (Claude Code)

Clone this repo into your skills directory, naming the folder `exeify-packer`:

```bash
git clone https://github.com/44886/exeify-web2exe-skill.git ~/.claude/skills/exeify-packer
```

On Windows (PowerShell):

```powershell
git clone https://github.com/44886/exeify-web2exe-skill.git "$env:USERPROFILE\.claude\skills\exeify-packer"
```

Restart Claude Code. The skill `exeify-packer` is now available and loads automatically when you
ask to package a website into an exe. (Project-level install: clone into `.claude/skills/exeify-packer`.)

## Install (other Agent Skills tools)

This is a standard [Agent Skills](https://agentskills.io) skill — a `SKILL.md` plus supporting files.
Any tool that supports the standard can load it; place this directory where that tool discovers skills.

## Usage / CLI

The AI assembles the command for you. Under the hood:

```
exeify.exe pack --local <dir> [--entry index.html] --out <app.exe> [options]
exeify.exe pack --url <url>   --out <app.exe> [options]
```

Options: `--title --width --height --window normal|maximized|fullscreen --no-resizable
--icon <ico|png> --splash <img> --splash-bg <#rrggbb> --splash-sec <s> --no-protect`.
Run `exeify.exe pack --help` for the full list. Success prints `OK: <path>` (exit 0).

See `SKILL.md` for the full instructions the AI follows.

## Contents

| File | Purpose |
|---|---|
| `SKILL.md` | The skill definition (Agent Skills frontmatter + instructions) |
| `exeify.exe` | Bundled Exeify packer (Windows) — the CLI the skill calls |
| `LICENSE` | Apache-2.0 |

## Updating

When a new Exeify version ships, replace `exeify.exe` with the latest from
[Exeify releases](https://github.com/44886/Exeify/releases). The CLI contract is stable
(`exeify pack ...` → `OK: <path>`).

## License

Apache-2.0. Exeify © 不坑老师 · https://github.com/44886/Exeify
