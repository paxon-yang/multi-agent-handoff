<div align="center">

# 🧠 multi-agent-handoff

**Stop losing context every time you switch AI tools.**
**在不同 AI 工具之间切换时，再也不丢失上下文。**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Works with Claude Code](https://img.shields.io/badge/Works%20with-Claude%20Code-blue)](https://claude.ai)
[![Works with Codex](https://img.shields.io/badge/Works%20with-OpenAI%20Codex-green)](https://openai.com/codex)
[![Works with Cursor](https://img.shields.io/badge/Works%20with-Cursor-purple)](https://cursor.so)
[![Works with Windsurf](https://img.shields.io/badge/Works%20with-Windsurf-teal)](https://codeium.com/windsurf)

</div>

---

## The Problem 问题

You are mid-feature in Claude Code. You switch to Codex. It rewrites everything differently.
你在 Claude Code 里写到一半，换到 Codex，它把代码风格全改了。

You start a new session tomorrow. You spend 20 minutes re-explaining the architecture.
第二天开新会话，花了 20 分钟重新解释项目架构。

You hand off to a teammate's AI. It reverses a decision you made for good reason, and breaks everything.
交给同事的 AI 接手，它把深思熟虑的架构决定推翻了，然后一切崩了。

**Every AI starts with zero memory. This fixes that.**
**每个 AI 启动时记忆为零。这个工具解决这个问题。**

---

## The Solution 解决方案

A single file — `PROJECT_BRAIN.md` — lives in your project root.
项目根目录里放一个文件 `PROJECT_BRAIN.md`。

Every AI tool reads it at session start. Every AI tool updates it before you switch.
每个 AI 工具在会话开始时读它，切换前更新它。

No servers. No plugins. No sync. Just a markdown file.
不需要服务器、插件或同步。只是一个 Markdown 文件。

```
Claude Code ──┐
              ├──► PROJECT_BRAIN.md ◄──► Any AI, Any Session
Codex ────────┤
Cursor ───────┤
Windsurf ─────┘
```

---

## Quick Start 快速开始

### Step 1 — Install the protocol 安装协议

**Claude Code** — add to `~/.claude/CLAUDE.md` (global) or `CLAUDE.md` (project):
```markdown
## AI Session Protocol
At the start of every session, read PROJECT_BRAIN.md if it exists.
At the end of every session (or before switching tools), update PROJECT_BRAIN.md.
Follow all constraints listed in PROJECT_BRAIN.md without exception.
```

**Codex** — add to `~/.codex/instructions.md`:
```
IMPORTANT: Read PROJECT_BRAIN.md at session start. Update it before ending.
```

**Cursor** — add to `.cursorrules`:
```
Always read PROJECT_BRAIN.md first. Maintain it across sessions.
```

**Windsurf** — add to `.windsurfrules`:
```
Always read PROJECT_BRAIN.md first. Maintain it across sessions.
```

Full config snippets for all tools: [`tool-configs/`](tool-configs/)

### Step 2 — Create PROJECT_BRAIN.md 创建项目大脑文件

Copy the template: [`templates/PROJECT_BRAIN.md`](templates/PROJECT_BRAIN.md)

Or tell your AI at the start of a new project:
> "Create a PROJECT_BRAIN.md for this project."

### Step 3 — Switch freely 自由切换

Before switching tools:
> "I am switching to [Codex/Cursor/etc.]. Please update PROJECT_BRAIN.md first."

When starting in a new tool:
> "Read PROJECT_BRAIN.md and tell me where we left off."

---

## What Gets Preserved 保存哪些内容

| Category | Example | Why It Matters |
|----------|---------|----------------|
| **Architecture Decisions** | "We use REST not GraphQL because X" | Prevents costly reversals |
| **Code Style Contract** | camelCase, 2-space indent, English comments | Prevents style drift |
| **Current State** | What is done, in progress, broken | Prevents duplicate work |
| **Constraints** | "Do not touch auth.js — fragile edge case" | Prevents regressions |
| **Key Files Map** | "utils/parser.js is the core pipeline" | Prevents misunderstanding |
| **Decision Log** | Timestamped history of every major choice | Full audit trail |

---

## Tool Compatibility 工具兼容性

| Tool | Config File | Status |
|------|-------------|--------|
| Claude Code | `CLAUDE.md` or `~/.claude/CLAUDE.md` | ✅ Tested |
| OpenAI Codex | `~/.codex/instructions.md` | ✅ Tested |
| Cursor | `.cursorrules` | ✅ Tested |
| Windsurf | `.windsurfrules` | ✅ Tested |
| GitHub Copilot | `.github/copilot-instructions.md` | ✅ Supported |
| Any LLM (manual) | Paste universal prompt | ✅ Universal |

---

## Who This Is For 适合谁用

- 🧑‍💻 Developers who use multiple AI tools on the same project — 同时使用多个 AI 工具的开发者
- 👥 Teams where different members use different AI assistants — 成员使用不同 AI 助手的团队
- 🔄 Anyone who hates re-explaining context every session — 讨厌每次重新解释上下文的开发者
- 🏃 Rapid prototypers making lots of decisions that need to survive tool switches

---

## Contributing 贡献

PRs welcome for new tool configs, framework-specific templates, and translations.

## License

MIT — use freely, improve openly.

---

<div align="center">
<b>If this saved you time, a ⭐ star helps others find it.</b><br>
<b>如果这帮助了你，点个 ⭐ Star 让更多人发现它。</b>
</div>
