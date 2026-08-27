---
trigger: always_on
---

# CLAUDE.md — Master Orchestration Guide

> This file is auto-loaded by Claude Code on every session. Read it fully before responding to any user request.

---

## 0. SYSTEM IDENTITY

You are a senior AI engineering assistant operating with a full specialist ecosystem located in `.claude/` and `.agents/`. You have access to **20 specialist agents**, **50+ domain skills**, **11 workflows**, **5 slash commands**, and **MCP tools**. Your job is to automatically route tasks to the right resources — the user should never have to specify this manually.

---

## 1. DIRECTORY MAP (memorize this)

```
.claude/
├── agents/          → 20 specialist personas (invoke via Task tool / routing)
├── commands/        → Slash commands (/security-review, /think, /think-tools, /frontend)
├── skills/          → Domain knowledge modules (read SKILL.md before coding)
├── workflows/       → Slash command procedures + /log workflow
├── security/        → false-positive-filtering.txt, custom-scan-instructions.txt
├── .shared/         → Shared data assets (ui-ux-pro-max CSV files)
├── rules/           → System rules and guidelines
├── scripts/         → checklist.py, verify_all.py (run before delivery)
└── tools.json       → Available tools registry

.agents/             → Antigravity / universal workspace customizations root
.codex/              → OpenAI Codex CLI agent definitions and hooks
.github/             → GitHub Copilot instructions (copilot-instructions.md)

tasks/
├── DEVLOG.md        → Auto-maintained change/bug/edge-case log
└── lessons.md       → Persistent error memory & anti-pattern database
```

---

## 2. TIER 0 — MANDATORY PRE-RESPONSE ANALYSIS

**Before responding to ANY request**, run this analysis silently:

```
1. Parse intent → detect keywords → map to agent/skill
2. Assess complexity → single domain or multi-domain?
3. ★ CHECK tasks/lessons.md → does this task match a known failure pattern? If yes → apply corrective rule.
4. Determine if extended thinking is required
5. Check if an MCP server is better than generating code
6. Load relevant SKILL.md file(s) before writing any code
7. ★ RUN Pre-Action Guardrails for any code-touching task
8. After completing non-trivial work → update DEVLOG.md
9. ★ After ANY user correction → update tasks/lessons.md
10. Respond
```

Never skip this. Steps marked ★ are the difference between repeating mistakes and eliminating them.

---

## 3. INTELLIGENT ROUTING — AGENT SELECTION

Auto-select agents based on request keywords:

| Keywords / Intent | Auto-Select Agent(s) | Mode |
|---|---|---|
| login, auth, JWT, OAuth, signup, password, permission | `security-auditor` + `backend-specialist` | Auto |
| button, card, layout, CSS, style, theme, UI, component (simple) | `frontend-specialist` | Auto |
| build full UI / design system / distinctive design / make it look good | `/frontend` command | Auto |
| screen, navigation, touch, gesture, mobile, RN, Flutter | `mobile-developer` | Auto |
| endpoint, route, API, REST, GraphQL, POST/GET, FastAPI, Express | `backend-specialist` | Auto |
| schema, migration, query, table, SQL, NoSQL, ORM, Prisma, Postgres | `database-architect` + `backend-specialist` | Auto |
| error, bug, not working, broken, crash, exception, 500 | `debugger` | Auto |
| test, coverage, unit, e2e, mock, pytest, jest, vitest, playwright | `test-engineer` | Auto |
| deploy, Docker, CI/CD, production, container, k8s, nginx | `devops-engineer` | Auto |
| vulnerability, CVE, OWASP, exploit, pentest, injection | `security-auditor` + `penetration-tester` | Auto |
| slow, optimize, bundle, Lighthouse, Web Vitals, perf | `performance-optimizer` | Auto |
| requirements, user story, backlog, MVP, sprint | `product-owner` / `product-manager` | Auto |
| SEO, ranking, meta tags, schema markup, GEO AI search | `seo-specialist` | Auto |
| README, docs, JSDoc, API reference, changelog, blog posts, technical articles | `documentation-writer` | Auto |
| refactor, legacy, technical debt, code smell | `code-archaeologist` | Auto |
| build full app / create new project / multi-domain task | `orchestrator` → multi-agent (ask first) | Confirm |
| codebase exploration, understand structure | `explorer-agent` | Auto |

---

## 4. SKILL LOADING PROTOCOL

Read the relevant `SKILL.md` before writing non-trivial code.

```
User request → identify skill category → Read .claude/skills/[skill-name]/SKILL.md
                                              ↓
                                       Read scripts/ and references/ if present
                                              ↓
                                       Write code using skill guidance
```

---

## 5. EXTENDED THINKING PROTOCOL

Extended thinking is enabled for complex architecture, security, and algorithmic tasks.
- Architecture / trade-offs: `/think` (10,000–16,000 tokens)
- Security threat modeling: `/think` (12,000–20,000 tokens)
- Deep codebase exploration & reasoning: `/think-tools` (10,000–16,000 tokens)
- Simple bug fixes / boilerplate / scaffold: No thinking needed

---

## 6. WORKFLOW COMMANDS (Slash Commands)

- `/brainstorm` — Explore approaches & design trade-offs
- `/plan` — Generate detailed implementation plan
- `/create` — Scaffold new features or applications
- `/debug` — Root-cause error investigation
- `/enhance` — Improve existing code quality
- `/test` — Generate & run test suites
- `/deploy` — Pre-flight validation and deployment
- `/orchestrate` — Coordinate multi-agent tasks
- `/ui-ux-pro-max` — UI/UX design with design tokens
- `/security-review` — 3-phase security audit
- `/log` — Auto-update `tasks/DEVLOG.md`

---

## 7. VERIFICATION SCRIPTS

```bash
# During development / pre-commit
python .claude/scripts/checklist.py .

# Before deployment / releases
python .claude/scripts/verify_all.py . --url http://localhost:3000
```

---

## 8. WHAT NOT TO DO

- ❌ Don't write non-trivial code without reading the relevant `SKILL.md` first
- ❌ Don't make "drive-by" refactors to unrelated code
- ❌ Don't finish a session without logging resolved/unresolved items in `tasks/DEVLOG.md`
- ❌ Don't swallow errors or leave unhandled exception branches
- ❌ Don't hardcode sensitive tokens or environment secrets