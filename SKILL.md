---
name: multi-agent-handoff
description: |
  Prevents context loss and project incoherence when switching between AI coding tools (Claude Code, Codex, Cursor, Windsurf, etc.) or between different AI models mid-project. Use this skill whenever the user mentions switching tools, switching models, starting a new session on an ongoing project, resuming work, handing off to another AI, or noticing inconsistencies in their codebase. Also trigger when the user asks to "summarize project state", "prepare a handoff", "create a project brief", "update CLAUDE.md", or "sync context". This skill is essential for multi-tool workflows — trigger it proactively even if the user just says "I'm switching to Codex now" or "continue in a new chat".
---

# Multi-Agent Handoff Skill

Maintains project coherence when switching between AI coding assistants (Claude Code ↔ Codex ↔ Cursor etc.) or between sessions. Creates and maintains a living `PROJECT_BRAIN.md` file that any AI can read to instantly restore full context.

## Why This Matters

Each AI tool starts with zero memory. Without a handoff document:
- New model doesn't know *why* decisions were made (only *what*)
- Architecture choices get second-guessed and reversed
- Code style drifts (naming, comments, structure)
- Completed work gets duplicated
- Half-finished features are unknown landmines
- Environment assumptions diverge silently

---

## Core Workflow

| User says | Action |
|-----------|--------|
| "I'm switching to Codex / Cursor / etc." | Run **Pre-Switch Snapshot** |
| "Starting fresh session", "new chat" | Run **Session Onboarding** |
| "Resume my project" | Run **Session Onboarding** |
| "Update the project brief" | Run **Snapshot Update** |
| "Things feel inconsistent" | Run **Drift Audit** |
| "Prepare handoff" | Run **Full Handoff Package** |

---

## Mode 1: Pre-Switch Snapshot

```
1. Read current PROJECT_BRAIN.md (if exists)
2. Ask user 3 quick questions:
   a. What did we accomplish this session?
   b. What's in progress / half-done?
   c. Any decisions or constraints the next AI must know?
3. Update PROJECT_BRAIN.md
4. Confirm: "Ready to switch. Tell the next tool: 'Read PROJECT_BRAIN.md first'"
```

## Mode 2: Session Onboarding

```
1. Check for PROJECT_BRAIN.md in project root
2. If found: read it, summarize to user, ask "Anything changed since this was written?"
3. If not found: scan codebase, infer state, ask user to validate
4. Set session working assumptions (style, language, constraints)
5. Confirm understanding before writing any code
```

## Mode 3: Snapshot Update

```
1. Read existing PROJECT_BRAIN.md
2. Update only changed sections
3. Append to DECISION_LOG with timestamp
4. Do NOT rewrite everything — preserve history
```

## Mode 4: Drift Audit

Scan for divergence signs:
- [ ] Naming convention conflicts (camelCase vs snake_case mixed)
- [ ] Duplicate utility functions
- [ ] Import style inconsistencies
- [ ] TODO comments from different sessions contradicting each other

## Mode 5: Full Handoff Package

Produces:
1. Updated `PROJECT_BRAIN.md`
2. `HANDOFF_NOTES.md` — session-specific, can be deleted after reading
3. Optional: `KNOWN_ISSUES.md` update

---

## Installation Instructions

### Claude Code — `~/.claude/CLAUDE.md` or project `CLAUDE.md`
```
## AI Session Protocol
At the start of every session, read PROJECT_BRAIN.md if it exists.
At the end of every session (or before the user switches tools), update PROJECT_BRAIN.md.
Follow all constraints listed in PROJECT_BRAIN.md without exception.
```

### Codex — `~/.codex/instructions.md`
```
IMPORTANT: Read PROJECT_BRAIN.md at session start. Update it before ending.
```

### Cursor / Windsurf — `.cursorrules` or `.windsurfrules`
```
Always read PROJECT_BRAIN.md first. Maintain it across sessions.
```

---

## Quick Reference

```
🔴 SWITCHING TOOLS?  → Update PROJECT_BRAIN.md first
🟡 NEW SESSION?      → Read PROJECT_BRAIN.md first, summarize to user
🟢 MAJOR DECISION?   → Append to Decision Log immediately
```

## See Also
- `references/risk-matrix.md` — Full risk analysis table
- `references/tool-configs.md` — Config snippets for each AI tool
- `templates/PROJECT_BRAIN.md` — Copy-paste template
