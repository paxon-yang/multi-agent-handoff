# AI Tool Configuration Snippets

## Claude Code — CLAUDE.md

```markdown
## AI Session Protocol (Multi-Tool Project)

### Session Start (REQUIRED)
1. Read `PROJECT_BRAIN.md` if it exists in project root
2. Summarize current state to user: "Based on PROJECT_BRAIN.md, here's where we are: [summary]"
3. Ask: "Does this match your current understanding? Anything changed?"
4. Only then proceed with the user's request

### During Session
- Append to `PROJECT_BRAIN.md → Decision Log` for any architectural decision
- Mark features as "in progress" in PROJECT_BRAIN.md if you start but don't finish
- Follow Code Style Contract without deviation

### Session End / Before Tool Switch (REQUIRED)
1. Update `PROJECT_BRAIN.md → Current State` section
2. Append session summary to `Session History`
3. Tell user: "PROJECT_BRAIN.md updated. Safe to switch tools."

### Hard Rules
- NEVER reverse decisions in `Architecture Decisions` without explicit user approval
- NEVER assume "in progress" items are complete
- NEVER introduce new dependencies without adding to PROJECT_BRAIN.md
```

---

## Codex — ~/.codex/instructions.md

```
SESSION PROTOCOL: This is a multi-tool project.
1. Read PROJECT_BRAIN.md before writing any code
2. Follow all constraints in "Constraints & Non-Negotiables"
3. Match "Code Style Contract" exactly
4. Update PROJECT_BRAIN.md Decision Log for any new architectural choice
5. Update Current State before ending session
```

---

## Cursor — .cursorrules

```
# Multi-Tool Project Protocol
- Read PROJECT_BRAIN.md at session start
- Respect all Architecture Decisions (do not reverse)
- Follow Code Style Contract
- Update PROJECT_BRAIN.md before user switches tools
- Append to Decision Log for architectural choices
```

---

## Windsurf — .windsurfrules

```
# Session Protocol
Always read PROJECT_BRAIN.md first. Maintain context across tool switches.
Architecture Decisions are locked unless user explicitly approves changes.
Update PROJECT_BRAIN.md Current State section at session end.
```

---

## GitHub Copilot — .github/copilot-instructions.md

```
# Multi-Tool Project Protocol
Read PROJECT_BRAIN.md at the start of every session.
Follow all constraints. Never reverse Architecture Decisions without user approval.
Update PROJECT_BRAIN.md before the user switches tools.
```

---

## Universal Prompt Prefix (any tool)

Paste at start of every session if your tool has no config file:

```
Before we start: please read PROJECT_BRAIN.md in the project root and summarize
the current project state to confirm your understanding. Do not write any code
until you've confirmed the context.
```

---

## Before Switching Tools

Tell your current AI:

```
I'm about to switch to [Codex/Cursor/Claude/etc.]. Please update PROJECT_BRAIN.md
with what we accomplished this session, what's still in progress, and any
architectural decisions we made. Then confirm it's updated.
```

---

## Git Hook Reminder (optional)

Add to `.git/hooks/pre-push`:

```bash
#!/bin/bash
if git diff --cached --name-only | grep -q "PROJECT_BRAIN.md"; then
  echo "✅ PROJECT_BRAIN.md updated in this commit"
else
  echo "⚠️  Reminder: Did you update PROJECT_BRAIN.md before switching AI tools?"
fi
```

Make executable: `chmod +x .git/hooks/pre-push`
