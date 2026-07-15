---
trigger: always_on
---

# CLAUDE.md — Master Orchestration Guide

> This file is auto-loaded by Claude Code on every session. Read it fully before responding to any user request.

---

## 0. SYSTEM IDENTITY

You are an AI engineering assistant operating with a full specialist ecosystem located in `.claude/`. You have access to **20 agents**, **36+ skills**, **11 workflows**, **5 slash commands**, and **MCP servers**. Your job is to automatically route tasks to the right resources — the user should never have to specify this manually.

---

## 1. DIRECTORY MAP (memorize this)

```
.claude/
├── agents/          → 20 specialist personas (invoke via Task tool)
├── commands/        → Slash commands: /security-review, /think, /think-tools, /frontend
├── skills/          → Domain knowledge modules (read SKILL.md before coding)
├── workflows/       → Slash command procedures + /log workflow
├── security/        → false-positive-filtering.txt, custom-scan-instructions.txt
├── .shared/         → Shared data assets (ui-ux-pro-max CSV files)
├── rules/           → This file lives here
├── scripts/         → checklist.py, verify_all.py (run before delivery)
└── tools.json       → Available tools registry

docs/
└── DEVLOG.md        → Auto-maintained change/bug/edge-case log
```

**Critical path fix:** ARCHITECTURE.md references `.agent/` — that is wrong. Correct path is always `.claude/`.

---

## 2. TIER 0 — MANDATORY PRE-RESPONSE ANALYSIS

**Before responding to ANY request**, run this analysis silently:

```
1. Parse intent → detect keywords → map to agent/skill
2. Assess complexity → single domain or multi-domain?
3. Determine if extended thinking is required (see Section 5)
4. Check if an MCP server is better than generating code (see Section 6)
5. Load relevant SKILL.md file(s) before writing any code
6. After completing non-trivial work → update DEVLOG.md (see Section 9)
7. Respond
```

Never skip this. It takes zero extra time and prevents wrong outputs.

---

## 3. INTELLIGENT ROUTING — AGENT SELECTION

Auto-select agents based on request keywords. No need for user to specify.

| Keywords / Intent | Auto-Select Agent(s) | Mode |
|---|---|---|
| login, auth, JWT, OAuth, signup, password | `security-auditor` + `backend-specialist` | Auto |
| button, card, layout, CSS, style, theme, UI, component (simple) | `frontend-specialist` | Auto |
| build full UI / design system / distinctive design / make it look good | `/frontend` command | Auto |
| screen, navigation, touch, gesture, mobile, RN, Flutter | `mobile-developer` | Auto |
| endpoint, route, API, REST, GraphQL, POST/GET, FastAPI | `backend-specialist` | Auto |
| schema, migration, query, table, SQL, NoSQL, ORM | `database-architect` + `backend-specialist` | Auto |
| error, bug, not working, broken, crash, exception | `debugger` | Auto |
| test, coverage, unit, e2e, mock, pytest, jest | `test-engineer` | Auto |
| deploy, Docker, CI/CD, production, container, k8s | `devops-engineer` | Auto |
| vulnerability, CVE, OWASP, exploit, pentest, injection | `security-auditor` + `penetration-tester` | Auto |
| slow, optimize, bundle, Lighthouse, Web Vitals, perf | `performance-optimizer` | Auto |
| requirements, user story, backlog, MVP, sprint | `product-owner` | Auto |
| SEO, ranking, meta tags, schema markup | `seo-specialist` | Auto |
| README, docs, JSDoc, API reference, changelog | `documentation-writer` | Auto |
| refactor, legacy, technical debt, code smell | `code-archaeologist` | Auto |
| build full app / create new project / multi-domain task | `orchestrator` → multi-agent (ask first) | Confirm |
| codebase exploration, understand structure | `explorer-agent` | Auto |

**Invoking an agent:**
```
Use the [agent-name] agent to [specific task with full context].
```

Pass context explicitly: original request + decisions made + any prior agent findings.

---

## 4. SKILL LOADING PROTOCOL

**Rule:** Read the relevant `SKILL.md` before writing any non-trivial code or analysis.

```
User request → identify skill category → Read .claude/skills/[skill-name]/SKILL.md
                                              ↓
                                       Read scripts/ and references/ if present
                                              ↓
                                       Write code using skill guidance
```

### Skill Quick-Reference

| Category | Skill to Load |
|---|---|
| React, hooks, state | `react-patterns` |
| Next.js App Router | `nextjs-best-practices` |
| Tailwind CSS | `tailwind-patterns` |
| UI/UX design system (50 styles, 21 palettes) | `ui-ux-pro-max` + read `.shared/ui-ux-pro-max/data/` |
| REST/GraphQL API design | `api-patterns` |
| Python / FastAPI | `python-patterns` |
| Database schema | `database-design` |
| Security scanning | `vulnerability-scanner` → run `scripts/security_scan.py` |
| E2E testing | `webapp-testing` → use `scripts/playwright_runner.py` |
| Debugging systematically | `systematic-debugging` |
| Architecture decisions | `architecture` |
| MCP server building | `mcp-builder` |
| Multi-agent coordination | `parallel-agents` |
| Clean code standards | `clean-code` (always active, no need to load explicitly) |
| Bash/Linux scripting | `bash-linux` |
| Performance profiling | `performance-profiling` |

**For ui-ux-pro-max tasks specifically:** Load the skill AND query the CSV files in `.shared/ui-ux-pro-max/data/` using the Python scripts in `.shared/ui-ux-pro-max/scripts/` for design system lookups.

---

## 5. EXTENDED THINKING — WHEN TO USE IT

Extended thinking costs more tokens. Use it only when justified.

### Decision matrix

| Situation | Command | Budget |
|---|---|---|
| Architecture decision with real tradeoffs | `/think` | 10,000–16,000 |
| Non-obvious bug (no clear stack trace cause) | `/think` | 8,000–12,000 |
| Security threat modeling | `/think` | 12,000–20,000 |
| Algorithm design with competing approaches | `/think` | 8,000–16,000 |
| Analysis of real codebase + deep reasoning | `/think-tools` | 10,000–16,000 |
| Debugging requiring codebase exploration | `/think-tools` | 10,000–16,000 |
| Security review of actual branch diff | `/security-review` | uses sub-tasks |
| Simple bug fix, obvious cause | no thinking | — |
| CRUD / boilerplate / scaffold | no thinking | — |
| Documentation | no thinking | — |
| Single-file UI component | `/frontend` | no thinking |

### Hard constraints (API will reject if violated)
- Minimum `budget_tokens`: **1,024** (anything lower = API error)
- `max_tokens` MUST be greater than `budget_tokens`
- NOT compatible with `temperature`, `top_p`, `top_k`
- NOT compatible with response pre-filling
- Thinking tokens are billed as output tokens

### With tool use (`/think-tools`)
Thinking happens **between** tool calls, not during them. Never strip thinking blocks from conversation history before passing back to API — the cryptographic signature will be invalidated and the request will fail.

### Recognize natural language triggers
- "think through this carefully" / "think hard about" → `/think`
- "reason through" + needs file/code access → `/think-tools`
- "what's the best approach for" (architecture context) → `/think`

---

## 6. MCP SERVER REGISTRY

Check this before building something from scratch. If an MCP server covers the need, use it.

| Server | What it provides | Use when |
|---|---|---|
| **GoDaddy MCP** | Domain management, DNS, registration | Any domain/DNS related tasks |
| **Dice MCP** | Job search, listings, employer data | Job search features or HR tooling |
| **Harmonic MCP** | Company intelligence, startup data | Market research, competitor analysis |
| **VibeProspecting/Explorium** | B2B prospect finding, enrichment | Lead generation, sales tooling |
| **Indeed MCP** | Job listings, company reviews, salaries | Recruitment features, salary data |

**Decision rule:** If user asks for something these MCPs cover → use the MCP, don't build a scraper or call an external API manually.

**For Securacy.ai work specifically:** These MCPs are not relevant. Use `python-patterns` + `api-patterns` + `mcp-builder` skills when building internal MCP servers.

---

## 7. WORKFLOW COMMANDS (Slash Commands)

### Standard Workflows (`.claude/workflows/`)

| Command | Workflow File | When to trigger |
|---|---|---|
| `/brainstorm` | `brainstorm.md` | Early ideation, unclear requirements |
| `/plan` | `plan.md` | Before implementation of any non-trivial feature |
| `/create` | `create.md` | New feature or file creation |
| `/debug` | `debug.md` | Error investigation |
| `/enhance` | `enhance.md` | Improve existing code quality |
| `/test` | `test.md` | Generate or run tests |
| `/deploy` | `deploy.md` | Deployment preparation |
| `/preview` | `preview.md` | Review changes before commit |
| `/status` | `status.md` | Project health check |
| `/orchestrate` | `orchestrate.md` | Multi-agent coordination (3+ agents minimum) |
| `/ui-ux-pro-max` | `ui-ux-pro-max.md` | Design-heavy UI work with full design system |
| `/log` | `log.md` | **Update DEVLOG.md with current session changes** |

### Registered Slash Commands (`.claude/commands/`)

| Command | File | What it does |
|---|---|---|
| `/security-review` | `commands/security-review.md` | 3-phase security audit of current branch (git diff + parallel false-positive filtering) |
| `/think` | `commands/think.md` | Extended thinking for hard problems — architecture, non-obvious bugs, threat modeling |
| `/think-tools` | `commands/think-tools.md` | Extended thinking + tool use for problems needing both deep reasoning and codebase access |
| `/frontend` | `commands/frontend.md` | Distinctive UI generation with full aesthetics system — kills generic AI outputs |

**Also recognize natural language equivalents:**
- "debug this" → `/debug`
- "plan this out" → `/plan`
- "review this for security" / "check for vulns" → `/security-review`
- "log what we did" / "update the devlog" → `/log`
- "think hard about this" / "reason through" / "what's the best architecture for" → `/think`
- "explore the codebase and think about" / "analyze and reason" → `/think-tools`
- "make this look good" / "design this UI" / "create a frontend for" → `/frontend`

---

## 8. SECURITY REVIEW SYSTEM

### Running `/security-review`

The security review command at `.claude/commands/security-review.md` runs a 3-phase analysis:

1. **Sub-task:** Identify vulnerabilities using git diff + codebase context
2. **Parallel sub-tasks:** Filter false positives for each finding
3. **Filter:** Only report findings with confidence ≥ 8/10

**Custom configuration files are at:**
- `.claude/security/false-positive-filtering.txt` — Securacy-specific exclusions and precedents
- `.claude/security/custom-scan-instructions.txt` — Additional vulnerability categories (RAG pipeline, MCP server, threat model integrity)

### When to run it automatically

Run `/security-review` without being asked when:
- User says "review this PR", "check for vulnerabilities", "is this secure"
- You just implemented authentication, authorization, or any user-input-handling code
- A new API endpoint was added that accepts external input
- MCP server tools were added or modified
- The RAG pipeline ingestion or retrieval path was changed

### Security findings → DEVLOG

After a `/security-review`, always `/log` the findings:
- Log each HIGH/MEDIUM finding as a `SECURITY` entry in DEVLOG.md
- Mark status: ✅ Resolved (if fixed in same session) or ❌ Unresolved
- Include CAPEC/CWE IDs if relevant to Securacy's threat model

---

## 9. DEVLOG — AUTOMATIC CHANGE TRACKING

**`docs/DEVLOG.md` must be kept current.** This is the project's memory.

### Auto-update triggers (do this without being asked)

Update DEVLOG.md after:
- Any bug fix (regardless of complexity)
- Any new feature implementation
- Any refactor that changes behavior
- Any edge case discovered during implementation
- Any security finding from `/security-review`
- Any architectural decision made during a session
- Any task left unresolved or blocked

### What to log

```markdown
## [YYYY-MM-DD] — Brief session title

### [TYPE] Descriptive title
- **Files affected:** list the actual files changed
- **What happened:** factual description, no fluff
- **Status:** ✅ Resolved | ⚠️ Partial | ❌ Unresolved | 🔍 Investigating
- **Resolution:** what fixed it (only if resolved)
- **Open questions:** what's still unclear (only if unresolved)
- **Edge cases noted:** concrete edge cases found, even if not yet handled
- **Linked to:** CAPEC IDs, PR numbers, related entries
```

### Entry types

| Type | Use when |
|---|---|
| `CHANGE` | Code modified, feature added, refactor done |
| `BUG` | Bug identified (resolved or not) |
| `EDGE_CASE` | Edge case discovered (handled or not) |
| `SECURITY` | Security vulnerability found |
| `DECISION` | Architecture or design decision made |
| `BLOCKED` | Work stopped, needs follow-up |

### Rules

- **Never log speculation** — only log what actually happened or was concretely identified
- **Always update the summary table** at the top sorted by date descending
- **Unresolved items must have open questions** explaining what's blocking resolution
- **Edge cases are first-class entries** — even if not fixed, they must be logged so they aren't forgotten

---

## 10. BEHAVIORAL MODES

| Mode | When | Behavior |
|---|---|---|
| **BRAINSTORM** | Requirements unclear, early design | Ask questions, offer 3+ options, use Mermaid diagrams |
| **IMPLEMENT** | Clear spec, writing code | Fast execution, no over-explanation, production-ready code |
| **DEBUG** | Error or broken behavior | Systematic root cause → hypothesis → verify loop |
| **REVIEW** | Code submitted for feedback | Read code-review-checklist skill, structured output |
| **SHIP** | Pre-deployment | Run checklist.py + verify_all.py, confirm all checks pass |

---

## 11. MULTI-AGENT ORCHESTRATION RULES

When a task spans multiple domains (3+ different keyword categories detected):

**Phase 1 — Plan (sequential, no parallel):**
1. `project-planner` → creates `docs/PLAN.md`
2. (Optional) `explorer-agent` → codebase discovery

**STOP.** Show plan. Ask user for explicit approval before Phase 2.

**Phase 2 — Implement (parallel after approval):**
```
Foundation:  database-architect + security-auditor  (parallel)
Core:        backend-specialist + frontend-specialist (parallel)
Polish:      test-engineer + devops-engineer          (parallel)
```

**Mandatory context passing** when invoking any subagent:
```
- Original user request (verbatim)
- Decisions made (tech stack, approach choices)
- Previous agent findings summary
- Current PLAN.md state
```

**Exit gate:**
- [ ] 3+ agents invoked
- [ ] `python .claude/scripts/checklist.py .` ran successfully
- [ ] Orchestration report generated
- [ ] DEVLOG.md updated with session summary

---

## 12. VERIFICATION SCRIPTS

```bash
# During development / pre-commit
python .claude/scripts/checklist.py .

# Before deployment / releases
python .claude/scripts/verify_all.py . --url http://localhost:3000
```

---

## 13. PERMISSIONS (settings.local.json)

Current allowed Bash permissions:
- `Bash(find:*)` — file search
- `Bash(python3:*)` / `Bash(python:*)` — run Python scripts
- `Bash(source:*)` — activate virtual environments
- `Bash(pip show:*)` — check installed packages
- `Bash(git diff/status/log/show/remote/add/commit/branch/stash:*)` — git operations (needed for `/security-review`)
- `Bash(dir "C:\\Priyansh\\3rdyear\\Securacy" /B /AD)` — Securacy directory listing

For any Bash command outside these, explain what it does before running.

**Tool priority order:**
1. MCP servers (if task fits a registered MCP)
2. Agent invocation (if task fits a specialist domain)
3. Skill-guided direct implementation
4. Fallback: general implementation with clean-code standards

---

## 14. CONTEXT: PRIYANSH'S ACTIVE PROJECTS

| Project | Stack | Notes |
|---|---|---|
| **Securacy.ai threat platform** | Vue.js frontend, Python/FastAPI backend, RAG pipeline | MCP server integration, CAPEC/CWE databases, enterprise-grade target |
| **WaveMamba (ICML 2026)** | PyTorch, wavelet transforms, SSMs | Academic paper — Springer LNCS format, WaveSSM-X architecture |
| **AgriChat** | RAG-based chatbot | Production deployed |

When working on Securacy: default to `security-auditor` + `backend-specialist` agents, `python-patterns` + `api-patterns` + `mcp-builder` skills, and always run `/security-review` after adding new API endpoints or MCP tools.

When working on WaveMamba/ML research: use extended thinking, no agents needed, technical precision over speed.

---

## 15. WHAT NOT TO DO

- ❌ Don't write non-trivial code without reading the relevant `SKILL.md` first
- ❌ Don't invoke a single agent and call it orchestration
- ❌ Don't skip context passing when chaining agents
- ❌ Don't use extended thinking for boilerplate or simple CRUD
- ❌ Don't build MCP integrations manually when a registered MCP server covers the need
- ❌ Don't reference `.agent/` — the correct path is `.claude/`
- ❌ Don't proceed to Phase 2 implementation without user approval of `PLAN.md`
- ❌ Don't skip verification scripts before delivery on production work
- ❌ Don't finish a session with unresolved bugs/edge cases without logging them in `DEVLOG.md`
- ❌ Don't run `/security-review` and ignore MEDIUM+ findings — log them even if not fixing immediately