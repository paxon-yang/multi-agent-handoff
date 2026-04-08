# Multi-Agent Switching: Risk Matrix

## Full Risk Analysis

| Risk | Trigger | Impact | Likelihood | Mitigation |
|------|---------|--------|------------|------------|
| **上下文断裂** Context Loss | Tool switch, new session | 🔴 Critical | Very High | PROJECT_BRAIN.md required read |
| **决策反转** Decision Reversal | New model disagrees with old choices | 🔴 Critical | High | Architecture Decisions section locked |
| **风格漂移** Style Drift | Different models have different defaults | 🟡 Medium | Very High | Code Style Contract section |
| **重复实现** Duplication | Model doesn't know function exists | 🟡 Medium | High | Key Files Map + session summary |
| **隐性约束丢失** Lost Constraints | "Don't touch X because Y" not written down | 🔴 Critical | Medium | Constraints & Non-Negotiables section |
| **进度错误估计** Progress Misjudgment | Model assumes in-progress = complete | 🔴 Critical | High | Current State section |
| **环境假设冲突** Env Conflicts | Models assume different runtimes | 🟡 Medium | Medium | Environment & Config section |
| **回归引入** Regression Introduction | Model changes working code unknowingly | 🔴 Critical | Medium | "What's working" list |
| **半成品提交** Half-baked Commits | Switching mid-feature | 🟠 High | Medium | "In progress" flag + branch discipline |
| **注释语言混乱** Comment Language Mix | EN + ZH comments coexisting | 🟢 Low | High (bilingual devs) | Comment language in Style Contract |

## When Risk Is Highest

1. **Long projects (>1 week)** — more state to lose
2. **Multiple contributors** — including AI "contributors"
3. **Complex architecture** — more decisions that need rationale
4. **Bilingual teams** — style contracts matter more
5. **Rapid prototyping** — lots of temporary decisions that become permanent

## Risk Score by Workflow

| Workflow | Risk Level | Recommended Protocol |
|----------|------------|---------------------|
| Single tool, single session | 🟢 Low | Minimal — just commit often |
| Single tool, multiple sessions | 🟡 Medium | SESSION_SUMMARY.md per session |
| Multiple tools, same model family | 🟠 Medium-High | PROJECT_BRAIN.md required |
| Multiple tools, different models | 🔴 High | Full handoff protocol |
| Team + AI (multiple people switching) | 🔴 Critical | PROJECT_BRAIN.md + DECISION_LOG mandatory |
