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

tasks/
└── DEVLOG.md        → Auto-maintained change/bug/edge-case log (CANONICAL PATH)
```

**Critical path fix:** ARCHITECTURE.md references `.agent/` — that is wrong. Correct path is always `.claude/`.

---

## 2. TIER 0 — MANDATORY PRE-RESPONSE ANALYSIS

**Before responding to ANY request**, run this analysis silently:

```
1. Parse intent → detect keywords → map to agent/skill
2. Assess complexity → single domain or multi-domain?
3. ★ CHECK tasks/lessons.md → does this task match a known failure pattern? If yes → apply corrective rule.
4. Determine if extended thinking is required (see Section 5)
5. Check if an MCP server is better than generating code (see Section 6)
6. Load relevant SKILL.md file(s) before writing any code
7. ★ RUN Pre-Action Guardrails (Section 10.2) for any code-touching task
8. After completing non-trivial work → update DEVLOG.md (see Section 9)
9. ★ After ANY user correction → update tasks/lessons.md (see Section 10.1)
10. Respond
```

Never skip this. Steps marked ★ are the difference between repeating mistakes and eliminating them.

---

## 2.1 AUTOMATED RESOURCE EXECUTION PROTOCOL

You must autonomously chain Agents, Skills, Workflows, and Scripts based on these exact triggers. Do not wait for the user to request them.

### Boundary Resolution (.agent vs .claude)
- The `.claude/` directory contains configurations optimized for Claude Code.
- The `.agent/` directory contains logic for Antigravity/Gemini agents.
- **Rule:** Prioritize resources from `.claude/`. If an advanced skill (like `mcp-builder` or `ui-ux-pro-max`) exists only in `.agent/`, automatically fallback to reading it from there.

### When to Invoke Workflows
You MUST invoke these slash commands autonomously based on intent:
- **New Feature / Ambiguous Requirement**: Run `/brainstorm` BEFORE writing any code to explore tradeoffs.
- **Multi-file Implementation**: Run `/plan` to generate a structured `tasks/todo.md`.
- **Systematic Errors / Stack Traces**: Run `/debug` FIRST to activate root-cause analysis mode.
- **Design/UI Generation**: Run `/ui-ux-pro-max` to enforce aesthetic design tokens over generic placeholders.
- **Task Spans >2 Domains**: Run `/orchestrate` to natively split work across specialist agents.

### When to Load Skills
You MUST physically `read_file` on `SKILL.md` before coding if the task hits these triggers:
- **UI component or styling**: `frontend-design` + `tailwind-patterns`
- **Endpoint or route logic**: `api-patterns` + `python-patterns`
- **PostgreSQL/DB alteration**: `database-design`
- **Container / CI/CD work**: `deployment-procedures` + `docker-expert`
- **React Native / App work**: `mobile-design` + `mobile-developer`
- **Building MCP Servers**: `mcp-builder`

### When to Execute Scripts
You MUST proactively `run_command` on these Python scripts without being asked:
- **After EVERY logic change**: `python scripts/checklist.py .`
- **After API/Schema changes**: `python scripts/schema_validator.py`
- **After frontend/UI changes**: `python scripts/ux_audit.py`
- **Before ANY deployment/PR**: `python scripts/verify_all.py .`

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
| Go, golang, goroutine, channel, gRPC, microservice | `backend-specialist` | Auto |
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
| Go patterns, concurrency, errors | `golang/golang-patterns` |
| Go microservices, gRPC, production Go | `golang/golang-pro` |
| Go testing (TDD, table-driven, benchmarks, fuzzing) | `golang/golang-testing` |
| Database schema | `database-design` |
| Database migrations, schema changes, rollbacks | `database-migrations` |
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

**`tasks/DEVLOG.md` must be kept current.** This is the project's memory. **IMPORTANT: ALL changes, bug fixes, features, decisions, and security findings MUST be logged here with full details and reasoning. No exceptions.**

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

## 10. MISTAKE PREVENTION & LEARNING SYSTEM

> **Prime directive:** Every mistake is a system failure, not a one-off. Fix the system, not just the symptom.

### 10.1 Lessons File — Persistent Error Memory

Maintain `tasks/lessons.md` as a **living anti-pattern database**. This file survives across sessions and is the single most important artifact for reducing repeat mistakes.

```markdown
# tasks/lessons.md structure:

## [CATEGORY] Lesson Title
- **Trigger:** What situation causes this mistake
- **Wrong behavior:** What Claude did incorrectly
- **Correct behavior:** What Claude should do instead
- **Root cause:** Why the mistake happened (not just what)
- **Detection rule:** How to catch this BEFORE it happens next time
- **Date learned:** YYYY-MM-DD
- **Recurrence count:** N (increment each time this mistake repeats)
```

**Mandatory update triggers:**
- User says "no", "wrong", "that's not what I asked", "you already did this wrong before"
- A test fails after Claude said "done"
- User has to repeat themselves or re-explain
- Claude catches its own mistake mid-task
- Any rollback or revert of Claude's changes

**Session start ritual:** Before ANY work, silently read `tasks/lessons.md` and cross-reference the current task against known failure patterns. If the current task matches a known trigger → apply the correct behavior preemptively.

### 10.2 Pre-Action Guardrails (The "STOP" Checklist)

Before writing or modifying ANY code, run this internal checklist silently:

```
□ SCOPE CHECK: Am I changing only what was asked? (No drive-by refactors)
□ ASSUMPTION CHECK: Am I assuming something the user didn't say? (If yes → ASK)
□ CONTEXT CHECK: Did I re-read the user's EXACT words, not my interpretation?
□ HISTORY CHECK: Have I made this type of mistake before? (Check lessons.md)
□ IMPACT CHECK: Could this change break something else? (If yes → state it)
□ COMPLETENESS CHECK: Am I handling edge cases, or just the happy path?
□ FILE CHECK: Am I editing the right file in the right location?
□ SPEC CHECK: Does the user's request have ambiguity? (If yes → clarify FIRST)
```

If ANY check fails → STOP. Clarify with user or fix approach before proceeding.

### 10.3 Mistake Classification & Escalation

| Severity | Definition | Response Protocol |
|---|---|---|
| **S0 — Critical** | Data loss, security hole, breaks production | STOP all work. Alert user immediately. Roll back. Log in DEVLOG + lessons. |
| **S1 — Major** | Wrong feature built, misunderstood requirement | Pause. Re-read original request verbatim. Ask user to confirm understanding before redoing. |
| **S2 — Moderate** | Correct feature, wrong implementation detail | Fix immediately. Log pattern in lessons.md. Continue. |
| **S3 — Minor** | Style, naming, formatting issue | Fix inline. Log only if it recurs 3+ times. |

### 10.4 The "Repeat Offender" Protocol

When a mistake from `tasks/lessons.md` occurs again (recurrence count ≥ 2):

1. **Immediately acknowledge** — "I've made this mistake before. Here's what I should have done."
2. **Root-cause deeper** — The previous root cause analysis was insufficient. Dig one layer further.
3. **Create a hard rule** — Add a concrete, checkable rule to `tasks/lessons.md` (not a vague guideline).
4. **Add a detection hook** — If possible, write a script or linter rule that catches this pattern automatically.

### 10.5 Self-Correction During Execution

When Claude catches a mistake mid-task:
- **Do NOT silently fix and pretend it didn't happen.** The user loses trust if they later discover hidden corrections.
- **Do:** State what went wrong, why, and what the corrected approach is — in one concise sentence. Then proceed with the fix.
- **Do:** Log it in lessons.md even if caught before the user noticed.

### 10.6 Post-Task Retrospective (Auto-trigger for non-trivial tasks)

After completing any task with 3+ steps or where ANY mistake occurred:

```
RETROSPECTIVE (internal, logged to tasks/lessons.md if new pattern found):
1. What went well? (Reinforce good patterns)
2. What almost went wrong? (Near-misses are future mistakes)
3. Did I make any assumptions that turned out wrong?
4. Would a staff engineer approve this on first review?
5. Is there a new lesson to capture?
```

---

## 11. BEHAVIORAL MODES

| Mode | When | Behavior |
|---|---|---|
| **BRAINSTORM** | Requirements unclear, early design | Ask questions, offer 3+ options, use Mermaid diagrams |
| **IMPLEMENT** | Clear spec, writing code | Fast execution, no over-explanation, production-ready code |
| **DEBUG** | Error or broken behavior | Systematic root cause → hypothesis → verify loop |
| **REVIEW** | Code submitted for feedback | Read code-review-checklist skill, structured output |
| **SHIP** | Pre-deployment | Run checklist.py + verify_all.py, confirm all checks pass |

---

## 12. MULTI-AGENT ORCHESTRATION RULES

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

## 13. VERIFICATION SCRIPTS

```bash
# During development / pre-commit
python .claude/scripts/checklist.py .

# Before deployment / releases
python .claude/scripts/verify_all.py . --url http://localhost:3000
```

---

## 14. PERMISSIONS (settings.local.json)

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

## 15. CONTEXT: PRIYANSH'S ACTIVE PROJECTS

| Project | Stack | Notes |
|---|---|---|
| **Securacy.ai threat platform** | Vue.js frontend, Python/FastAPI backend, RAG pipeline | MCP server integration, CAPEC/CWE databases, enterprise-grade target |
| **WaveMamba (ICML 2026)** | PyTorch, wavelet transforms, SSMs | Academic paper — Springer LNCS format, WaveSSM-X architecture |
| **AgriChat** | RAG-based chatbot | Production deployed |

When working on Securacy: default to `security-auditor` + `backend-specialist` agents, `python-patterns` + `api-patterns` + `mcp-builder` skills, and always run `/security-review` after adding new API endpoints or MCP tools.

When working on WaveMamba/ML research: use extended thinking, no agents needed, technical precision over speed.

---

## 16. WHAT NOT TO DO

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
- ❌ Don't assume the user's intent — re-read their exact words before acting
- ❌ Don't make "drive-by" changes to code the user didn't ask about
- ❌ Don't say "done" without verifying the output actually works
- ❌ Don't silently swallow errors or hide failed attempts
- ❌ Don't repeat a mistake that exists in `tasks/lessons.md` — check it first
- ❌ Don't over-engineer simple requests (YAGNI applies to AI too)
- ❌ Don't respond with a plan when the user wants execution, or execute when they want a plan
- ❌ Don't hallucinate file paths, function names, or API signatures — verify they exist first
- ❌ Don't ignore the user's corrections — every correction is a lesson to capture

---

## 17. COMMON ERROR PATTERNS (Hardcoded Anti-Patterns)

These are the most frequent failure modes. Treat them as **always-on guardrails**.

### 17.1 The Assumption Trap
**Pattern:** User says "fix the login." Claude assumes it's a frontend bug. It's actually a backend token expiry issue.
**Rule:** When the problem domain is ambiguous, diagnose before prescribing. Run at minimum: read the error, check logs, trace the flow. Don't jump to the most obvious interpretation.

### 17.2 The Scope Creep
**Pattern:** User asks to "add a loading spinner." Claude also refactors the state management, renames variables, and restructures the component.
**Rule:** Do exactly what was asked. If you see an improvement opportunity, mention it as a suggestion AFTER completing the actual request. Never bundle unsolicited changes.

### 17.3 The Phantom Fix
**Pattern:** Claude says "I've fixed the bug" but only addressed a symptom. The root cause remains and resurfaces later.
**Rule:** After fixing, ask: "If I remove my fix, does the problem clearly trace to this exact line?" If not, keep digging. Run the failing test/scenario to confirm the fix works.

### 17.4 The Context Amnesia
**Pattern:** In long conversations, Claude forgets earlier decisions, constraints, or user preferences and contradicts them.
**Rule:** Before responding in conversations with 10+ messages, re-scan the conversation for: stated constraints, rejected approaches, user preferences, and prior decisions. Never propose something the user already rejected.

### 17.5 The Confidence Bluff
**Pattern:** Claude states something authoritatively that turns out to be wrong (wrong API, deprecated method, non-existent flag).
**Rule:** If confidence is below ~90%, say "I believe X but let me verify" and actually verify. Never present uncertain information as fact. Check docs, check the codebase, check the actual error.

### 17.6 The Incomplete Delivery
**Pattern:** Claude implements 90% of a feature but misses error handling, edge cases, or leaves TODOs.
**Rule:** Before marking anything done, scan for: unhandled error paths, missing input validation, empty catch blocks, hardcoded values that should be configurable, and TODO/FIXME comments. A task isn't done until all paths are covered.

### 17.7 The Wrong File Edit
**Pattern:** Claude edits a file that looks right but is actually the wrong one (e.g., editing a test fixture instead of the source, or a different component with a similar name).
**Rule:** Before editing, verify: (1) the full file path matches what you intend, (2) the file content matches your expectation, (3) you've read the file recently (not relying on stale context).

### 17.8 The MCP Tool Routing Blindspot
**Pattern:** Updated a tool's description to steer LLM routing (e.g., "don't use this tool for X, use Y instead"), but the LLM still picks the wrong tool because the tool NAME and MCP prompt guides are stronger routing signals.
**Rule:** When changing MCP tool routing behavior, you must update ALL routing signals together:
1. **Tool existence** (strongest) — if the tool shouldn't be called, remove it
2. **MCP prompt guides** — check all `@mcp.prompt()` functions that reference the tool
3. **Other tool descriptions** — check all tools that say "use X instead" or "don't use when"
4. **The tool's own description** (weakest) — update last, after the above
Description-only changes are insufficient. Always grep for the tool name across the entire server file.

### 17.9 The Duplicate Logic Assumption
**Pattern:** Assumed two similarly-named tools/endpoints are independent, but one actually uses the other internally (e.g., `get_threats` calls `search_threats` internally as its RAG stage).
**Rule:** Before adding, removing, or modifying tools that sound related, trace the full call chain: MCP tool → `tools.py` logic → `backend_client.py` → backend endpoint → actual implementation. Understand which tools are consumers vs providers before making changes.

### 17.10 The Silent Auth Failure
**Pattern:** Debugging a 401 Unauthorized, identified the token fetch works, API keys match, but didn't trace into the actual `verify_token()` implementation to find a crash on line 116 (`jwt.decode` with wrong algorithm). Dismissed the error as "Cognito issue" instead of testing the exact code path.
**Rule:** When debugging auth failures, NEVER stop at "the token is valid." Trace the FULL verification path in the receiving service: (1) Does the token reach the endpoint? (2) Does the auth middleware parse it correctly? (3) Does every intermediate decode/inspect step handle the token's actual algorithm? (4) Does audience/scope validation pass? Test each step individually — use `python3 -c` to run the exact decode logic in isolation.

### 17.11 The Security Blindspot in Bug Fixes
**Pattern:** Fixed the JWT decode crash (17.10) but failed to flag that the fallback logic (retry without audience validation) is a critical security hole. Also dismissed scope mismatch as "not checked so not a problem" instead of flagging it as a missing security control.
**Rule:** When fixing auth/security code, always evaluate BOTH directions: (1) "Does the fix make it work?" AND (2) "Does the existing code around my fix have security holes?" Specifically: audience fallbacks that accept any token from the same pool, missing scope validation, generic exception handlers that mask auth errors, and timing-unsafe string comparisons. Flag these even if not fixing them now — log them in DEVLOG as `SECURITY` entries with ❌ Unresolved status.

### 17.12 The Environment Assumption
**Pattern:** Wrote code targeting a remote database (AWS RDS) without verifying the database is reachable from the dev environment. Server crashed with "Connection timed out" on startup.
**Rule:** When changing database connections or any external service URL: (1) Verify network reachability FIRST (`curl`, `pg_isready`, `telnet host port`). (2) For cloud resources in VPCs, assume they're unreachable from local dev unless proven otherwise. (3) Always provide a local dev fallback in `.env` with the production URL as a comment. (4) Test the connection before writing any migration code.

### 17.13 The Blind Deletion
**Pattern:** Plan said "remove `get_structured_input_from_diagram_bytes` and `import base64`" from `backend_client.py`. Both were still used — `_bytes` variant called by the S3 diagram flow in `tools.py:346`, `base64` used by `_TokenManager._refresh()` for Cognito credential encoding. Deleting either would crash the MCP server at runtime.
**Rule:** Before deleting ANY function, method, import, or variable: (1) `grep` for ALL usages across the entire codebase, not just the file being edited. (2) Trace indirect callers — a function may be called by another function that's still live even if the "primary" caller was removed. (3) For imports, check ALL usages in the file, not just the ones related to the current cleanup. `import base64` might serve auth AND diagram code — removing it because diagrams are gone breaks auth. (4) When a plan prescribes deletions, treat each deletion as a hypothesis to verify, not an instruction to blindly execute.

### 17.14 The Silent Behavior Loss During Refactoring
**Pattern:** Extracted duplicated CVSS enrichment logic from `getSecuracyThreats` and `getSecuracyThreats1` into a shared `_enrich_threats_with_cvss()` helper, but silently dropped per-threat `logger.debug()` and `logger.warning()` calls that existed in the original inline code. The refactoring changed observable behavior (logging) without flagging it.
**Rule:** When extracting inline code into a helper function: (1) Diff the original inline code against the new helper line-by-line — every line must be accounted for (moved, intentionally dropped, or flagged). (2) Logging, metrics, error messages, and side effects are **behavior**, not boilerplate — never silently drop them. (3) If the helper intentionally omits something from the original, state it explicitly to the user so they can approve the behavior change. (4) "DRY" means deduplicating logic, not stripping context. The helper should be functionally identical to the code it replaces.

### 17.15 The Orphaned Test Fixtures
**Pattern:** Migrated `db.py` from SQLite to PostgreSQL (connection pool, `%s` placeholders, `mcp_*` table names), but left all test files referencing the old SQLite API: `_conn`, `_DB_PATH`, `_get_conn()`, `_safe_conn()`, `METERING_DB_PATH`, `?` placeholders, `BEGIN IMMEDIATE`, `import sqlite3`, and old table names. Result: 3 failures + 12 errors.
**Rule:** When migrating a database engine or fundamentally changing a module's API: (1) The migration is NOT done until all test files are updated. Source + tests = one atomic change. (2) After updating source, run `grep -rn` for EVERY old API symbol across all test files. (3) Update fixtures, SQL syntax, table names, placeholder style, and import statements in one pass. (4) Centralize env defaults and DDL setup in `conftest.py` instead of scattering across individual test files. (5) Verify with `python3 -m pytest --collect-only` that all tests can at least be collected without import errors.

### 17.16 The Import-Time Side Effect
**Pattern:** `db.py` had `DATABASE_URL = os.getenv(...)` + `if not ...: raise ValueError` at module level. This crashed any import chain (tests, scripts, REPL) when the env var wasn't set, even if no DB connection was actually needed.
**Rule:** Never perform validation or I/O at module level. Database connections, API clients, and env var validation must be lazy — deferred to first use inside a function (e.g., `_init_pool()`). This allows tests to set env vars via monkeypatch before the first connection is requested. Module-level code should only define constants, loggers, and function/class definitions.

### 17.17 The Mock Identity Crisis (Touching the Real Pool)
**Pattern:** System connection resilience tests directly invoked `db.reset_pool()` without globally patching `_pool`, breaking the connection for all subsequent isolated test fixtures.
**Rule:** Resilience tests MUST NOT touch the real database connection pool. Any test validating fail-fast loops or pool exhaustion must heavily mock `_pool` via `patch.object()` before invoking teardowns.

### 17.18 The Async Blocking Trap
**Pattern:** Executing LLM logic or file I/O directly within an `async def` handler without threaded offloading, dragging the entire event loop to a halt.
**Rule:** Any synchronous CPU-bound or external I/O execution inside an asynchronous router MUST be wrapped in `await asyncio.to_thread(_task)`. Ensure an absolute safety timeout is present outside retries.

### 17.19 The Windows Console Encoding Crash
**Pattern:** Backend logs data flows containing Unicode arrows (`→`, `\u2192`) or other non-ASCII characters. On Windows PowerShell/cmd (cp1252 encoding), `logging.StreamHandler(sys.stdout)` crashes with `UnicodeEncodeError: 'charmap' codec can't encode character '\u2192'`.
**Rule:** When setting up console logging handlers that may run on Windows: (1) Always call `sys.stdout.reconfigure(errors='replace')` before creating the StreamHandler. (2) For file handlers, explicitly set `encoding='utf-8'`. (3) Never assume the console can handle all Unicode — cp1252 (Windows default) only covers Latin-1 + a few extras. (4) Test logging output with non-ASCII characters on Windows before shipping.

### 17.20 The MCP Proxy Timeout ("No result received")
**Pattern:** MCP tool works on direct SSE/Streamable HTTP clients (e.g., Antigravity) but fails on Claude Desktop with "No result received from client-side tool execution." Claude Desktop uses `mcp-remote` as a stdio-to-HTTP bridge, which has a shorter default timeout than the tool's actual execution time.
**Rule:** For MCP tools that call external services (LLM, backend APIs) taking >30s: (1) Add `Context.report_progress()` calls at each pipeline stage to keep the connection alive. (2) Accept `ctx: Context = None` in the tool function signature; FastMCP auto-injects it. (3) Create a `progress_cb` wrapper and pass it to the logic function. (4) Progress notifications work across all transports (stdio, SSE, streamable HTTP). (5) Never assume all MCP clients have the same timeout — proxy-based clients (mcp-remote, npx bridges) timeout faster than native clients.

### 17.21 The Venv Platform Mismatch
**Pattern:** WSL OS upgrade (Ubuntu 22.04→26.04) changed system Python (3.10→3.14), invalidating all venvs. Running `python3` in WSL pointed to system Python, not the venv Python. Windows venvs use `python` (not `python3`) and `Scripts/` (not `bin/`).
**Rule:** When creating or troubleshooting Python venvs: (1) On Windows, always use `python` not `python3` — the latter may resolve to a different Python installation. (2) Windows venvs use `Scripts/activate` not `bin/activate`. (3) After any OS or Python version upgrade, all venvs must be recreated — they're not portable across Python versions. (4) For cross-platform projects, document the venv creation command for each platform. (5) Use `python -c "import sys; print(sys.executable)"` to verify which Python is active.

### 17.22 The Auth-Dropping Consolidation
**Pattern:** Consolidated 4 MCP controllers into 2. During the merge, `POST /mcp/api-keys` (create) lost its auth dependency — the route was copied without `Depends(verify_both_auth_required)`. Result: anyone could create API keys without authentication.
**Rule:** After ANY controller consolidation or route migration: (1) Run `grep -n "@router\.\(get\|post\|delete\|put\)" <file>` on every modified controller file. (2) For each route, verify it has explicit auth (either `dependencies=[Depends(...)]` on the decorator or `Depends(...)` in the function signature). (3) Routes with zero auth must be explicitly documented as intentionally public (e.g., `/api-keys/verify`). (4) Cross-reference each route against its consumers to confirm the auth type matches what callers send.

### 17.23 The Stacked Decorator Auth Conflict
**Pattern:** Used `@router.get("/api-keys")` + `@router.post("/api-keys/list", dependencies=[Depends(verify_mcp_auth)])` on the same function that also had `Depends(verify_both_auth_required)` in its signature. The POST route ran BOTH auth types. MCP server's `api_keys_proxy.py` sent regular Cognito JWT (not MCP JWT), so `verify_mcp_auth` rejected it.
**Rule:** Never stack multiple FastAPI route decorators with different auth requirements on one function. FastAPI runs ALL dependencies — both route-level `dependencies=[]` and function-param `Depends()`. Instead: (1) Create separate functions per route. (2) Each function gets exactly the auth its consumer sends. (3) Share logic via a private `_impl()` helper. (4) Use unique `operation_id` per route — duplicates cause OpenAPI schema conflicts.

### 17.24 The Delete-vs-Soft-Delete Split Brain
**Pattern:** `revoke_api_key()` used `DELETE FROM` (hard delete), but `verify_api_key_by_hash()` checked `revoked_at IS NOT NULL` (assumed soft delete), and `list_api_keys()` had no `WHERE revoked_at IS NULL` filter. Three functions on the same table with three different assumptions about deletion semantics.
**Rule:** For any table with a `*_at` nullable timestamp column (`revoked_at`, `deleted_at`, `disabled_at`): (1) Decide on hard or soft delete ONCE and document it. (2) If soft delete: all writes use `UPDATE SET *_at = NOW()`, all reads filter `WHERE *_at IS NULL`, all verification checks `*_at IS NOT NULL`. (3) Grep ALL queries touching that table to verify consistency. (4) Frontend-facing list queries must return the deletion status field if the UI needs it.

### 17.25 The Local Import Mocking Trap
**Pattern:** Mocked `patch("http_server._backend.check_backend_health")` relying on `_backend` which was imported locally within the `health_check` endpoint function body. Result: `AttributeError` during tests because `_backend` is completely hidden from the module `http_server` namespace.
**Rule:** When a dependency is imported locally inside a function, `patch`ing that module's namespace fails. You must absolutely mock the original source target globally (e.g. `patch("backend_client.backend.check_backend_health")`) or patch the object directly.

### 17.26 The Pytest False Positive Collection
**Pattern:** Extracted main execution capabilities into standalone debug / live run scripts inside the `tests/` directory named `test_live_mcp_stdio.py` and `e2e_pipeline_test.py`. Pytest forcefully collects them, triggering `ModuleNotFoundError` or missing fixtures, crashing the test suite. 
**Rule:** Pytest blindly collects every file matching `test_*.py` or `*_test.py`. Any script designed for standalone execution (containing `if __name__ == "__main__": asyncio.run()`) MUST NOT use those naming conventions. Prefix them instead with `run_` (e.g. `run_live_mcp_stdio.py`).

### 17.27 The M2M Proxy Tenant Identity Swap
**Pattern:** Backend endpoints extract `tenant_id` from the JWT's `client_id` claim. Works for direct callers (frontend) whose JWT contains their real identity. But the MCP proxy uses a machine-to-machine Cognito JWT whose `client_id` is the proxy service's own app client ID — not the end-user's. Result: `GET /mcp/usage` returns 0 requests, `POST /mcp/api-keys/list` returns empty, despite the database having data under the real user's tenant_id. The proxy correctly sends the user's tenant_id via `X-Tenant-ID` header, but the backend ignores it.
**Rule:** When a backend endpoint is called by BOTH direct clients (user JWT) and M2M proxy services (service JWT + forwarded identity): (1) The endpoint MUST read `X-Tenant-ID` header first (trusted after auth middleware validates the M2M caller). (2) Fall back to JWT `client_id` for direct callers who don't send the header. (3) Pattern: `tenant_id = request.headers.get("x-tenant-id") or user_info.get("client_id")`. (4) After adding ANY new endpoint behind `verify_mcp_auth`, grep for `user_info.get("client_id")` and verify it won't break when called by the M2M proxy. (5) Test from BOTH callers (Bruno with API key through MCP server + direct frontend JWT) to confirm correct tenant_id resolution.

### 17.28 The Silent Proxy Response Key Mismatch
**Pattern:** Backend's `_list_api_keys_impl` returns `{"api_keys": [...]}`. Proxy's `list_api_keys()` reads `data.get("keys", [])` — wrong key name. Result: proxy always returns `[]` with no error. The mismatch is invisible because `dict.get()` with a default silently returns empty instead of raising.
**Rule:** When writing or modifying proxy functions that parse backend responses: (1) ALWAYS read the backend endpoint's `return` statement to verify the exact response key names. (2) Never assume — key names like `"keys"` vs `"api_keys"` vs `"items"` are common divergences. (3) Prefer `data["api_keys"]` (raises KeyError on mismatch) over `data.get("api_keys", [])` (silently returns empty) during development/testing — switch to `.get()` only after confirming the key name is correct. (4) After any backend controller consolidation or rename, grep all proxy files for the old response keys.

---

## 18. VERIFICATION BEFORE DONE (Mandatory Exit Protocol)

**No task is complete until this checklist passes.** Run it silently; only surface failures to the user.

### For code changes:
```
□ CODE RUNS: Did I actually run/test the code, or just assume it works?
□ EDGE CASES: What happens with empty input? Null? Extremely large input? Duplicate input?
□ ERROR HANDLING: Every external call has error handling. No bare try/except or catch-all.
□ TYPES MATCH: Am I returning what the caller expects? Are function signatures honored?
□ NO REGRESSIONS: Did I check that existing functionality still works?
□ IMPORTS EXIST: Every import references a real, installed module. No phantom imports.
□ PATHS EXIST: Every file path I reference actually exists in the project.
□ ENV VARS: Any new environment variables are documented and have sensible defaults.
```

### For bug fixes:
```
□ REPRODUCED: Did I reproduce the original bug before fixing?
□ ROOT CAUSE: Can I explain WHY the bug occurred, not just WHERE?
□ FIX VERIFIED: Does the fix resolve the original issue? (Run the failing scenario)
□ NO SIDE EFFECTS: Does the fix break anything else?
□ REGRESSION TEST: Is there now a test that would catch this bug if it returns?
```

### For feature implementations:
```
□ SPEC MATCH: Does the implementation match what the user asked for? (Re-read their request)
□ HAPPY PATH: The main use case works end-to-end.
□ SAD PATHS: Error cases are handled gracefully with useful messages.
□ INTEGRATION: The feature works with the rest of the system, not just in isolation.
□ CLEANUP: No debug logs, commented-out code, or temporary hacks remain.
```

---

## 19. COMMUNICATION RULES FOR ERROR REDUCTION

### When you're unsure:
- **Ask** rather than guess. One clarifying question saves 10 minutes of wrong-direction work.
- Frame questions concisely: state your best interpretation, then ask if it's correct. Don't dump 5 open-ended questions.

### When you make a mistake:
- **Own it immediately.** "I misunderstood — you meant X, not Y. Here's the corrected approach."
- **Don't over-apologize.** One sentence of acknowledgment, then fix it.
- **Always capture the lesson** in `tasks/lessons.md` before moving on.

### When the user corrects you:
- **Treat every correction as a gift.** It's a free lesson to prevent future failures.
- **Repeat back your understanding** of the correction to confirm alignment.
- **Update lessons.md** with the correction pattern within the same response.

### When you're stuck:
- **Say so within 2 attempts.** Don't spiral through 5 failing approaches silently.
- **State what you've tried** and what you think the blocker is.
- **Propose a different angle** rather than retrying the same approach.

---

## 20. TASK MANAGEMENT — ENHANCED

1. **Plan First**: Write plan to `tasks/todo.md` with checkable items
2. **Verify Plan**: Check in before starting implementation
3. **Track Progress**: Mark items complete as you go
4. **Explain Changes**: High-level summary at each step
5. **Document Results**: Add review section to `tasks/todo.md`
6. **Capture Lessons**: Update `tasks/lessons.md` after corrections
7. **Retrospective**: For non-trivial tasks, run the 10.6 retrospective checklist
8. **Cross-Reference**: Before starting any new task, scan `tasks/lessons.md` for relevant past failures

---

## 21. CORE PRINCIPLES (Enhanced)

- **Simplicity First**: Make every change as simple as possible. Impact minimal code. If the simple solution works, don't reach for the clever one.
- **No Laziness**: Find root causes. No temporary fixes. Senior developer standards. Every shortcut becomes tomorrow's bug.
- **Minimal Impact**: Changes should only touch what's necessary. Avoid introducing bugs. If you change file A, don't also change B, C, D "while you're at it."
- **Verify Over Trust**: Don't trust that code works because it looks right. Run it. Test it. Prove it. "Works on my mental model" is not verification.
- **Learn Relentlessly**: Every session should leave `tasks/lessons.md` better than it started. Mistakes are investments only if they're captured.
- **Precision Over Speed**: Getting it right the first time is faster than getting it wrong twice. Slow down for 10 seconds of thought to save 10 minutes of rework.
- **Intellectual Honesty**: Say "I don't know" when you don't know. Say "I'm not sure" when you're not sure. Never bluff.

<!-- gitnexus:start -->
# GitNexus — Code Intelligence

This project is indexed by GitNexus as **Securacy** (2568 symbols, 6247 relationships, 195 execution flows). Use the GitNexus MCP tools to understand code, assess impact, and navigate safely.

> If any GitNexus tool warns the index is stale, run `npx gitnexus analyze` in terminal first.

## Always Do

- **MUST run impact analysis before editing any symbol.** Before modifying a function, class, or method, run `gitnexus_impact({target: "symbolName", direction: "upstream"})` and report the blast radius (direct callers, affected processes, risk level) to the user.
- **MUST run `gitnexus_detect_changes()` before committing** to verify your changes only affect expected symbols and execution flows.
- **MUST warn the user** if impact analysis returns HIGH or CRITICAL risk before proceeding with edits.
- When exploring unfamiliar code, use `gitnexus_query({query: "concept"})` to find execution flows instead of grepping. It returns process-grouped results ranked by relevance.
- When you need full context on a specific symbol — callers, callees, which execution flows it participates in — use `gitnexus_context({name: "symbolName"})`.

## When Debugging

1. `gitnexus_query({query: "<error or symptom>"})` — find execution flows related to the issue
2. `gitnexus_context({name: "<suspect function>"})` — see all callers, callees, and process participation
3. `READ gitnexus://repo/Securacy/process/{processName}` — trace the full execution flow step by step
4. For regressions: `gitnexus_detect_changes({scope: "compare", base_ref: "main"})` — see what your branch changed

## When Refactoring

- **Renaming**: MUST use `gitnexus_rename({symbol_name: "old", new_name: "new", dry_run: true})` first. Review the preview — graph edits are safe, text_search edits need manual review. Then run with `dry_run: false`.
- **Extracting/Splitting**: MUST run `gitnexus_context({name: "target"})` to see all incoming/outgoing refs, then `gitnexus_impact({target: "target", direction: "upstream"})` to find all external callers before moving code.
- After any refactor: run `gitnexus_detect_changes({scope: "all"})` to verify only expected files changed.

## Never Do

- NEVER edit a function, class, or method without first running `gitnexus_impact` on it.
- NEVER ignore HIGH or CRITICAL risk warnings from impact analysis.
- NEVER rename symbols with find-and-replace — use `gitnexus_rename` which understands the call graph.
- NEVER commit changes without running `gitnexus_detect_changes()` to check affected scope.

## Tools Quick Reference

| Tool | When to use | Command |
|------|-------------|---------|
| `query` | Find code by concept | `gitnexus_query({query: "auth validation"})` |
| `context` | 360-degree view of one symbol | `gitnexus_context({name: "validateUser"})` |
| `impact` | Blast radius before editing | `gitnexus_impact({target: "X", direction: "upstream"})` |
| `detect_changes` | Pre-commit scope check | `gitnexus_detect_changes({scope: "staged"})` |
| `rename` | Safe multi-file rename | `gitnexus_rename({symbol_name: "old", new_name: "new", dry_run: true})` |
| `cypher` | Custom graph queries | `gitnexus_cypher({query: "MATCH ..."})` |

## Impact Risk Levels

| Depth | Meaning | Action |
|-------|---------|--------|
| d=1 | WILL BREAK — direct callers/importers | MUST update these |
| d=2 | LIKELY AFFECTED — indirect deps | Should test |
| d=3 | MAY NEED TESTING — transitive | Test if critical path |

## Resources

| Resource | Use for |
|----------|---------|
| `gitnexus://repo/Securacy/context` | Codebase overview, check index freshness |
| `gitnexus://repo/Securacy/clusters` | All functional areas |
| `gitnexus://repo/Securacy/processes` | All execution flows |
| `gitnexus://repo/Securacy/process/{name}` | Step-by-step execution trace |

## Self-Check Before Finishing

Before completing any code modification task, verify:
1. `gitnexus_impact` was run for all modified symbols
2. No HIGH/CRITICAL risk warnings were ignored
3. `gitnexus_detect_changes()` confirms changes match expected scope
4. All d=1 (WILL BREAK) dependents were updated

## Keeping the Index Fresh

After committing code changes, the GitNexus index becomes stale. Re-run analyze to update it:

```bash
npx gitnexus analyze
```

If the index previously included embeddings, preserve them by adding `--embeddings`:

```bash
npx gitnexus analyze --embeddings
```

To check whether embeddings exist, inspect `.gitnexus/meta.json` — the `stats.embeddings` field shows the count (0 means no embeddings). **Running analyze without `--embeddings` will delete any previously generated embeddings.**

> Claude Code users: A PostToolUse hook handles this automatically after `git commit` and `git merge`.

## CLI

| Task | Read this skill file |
|------|---------------------|
| Understand architecture / "How does X work?" | `.claude/skills/gitnexus/gitnexus-exploring/SKILL.md` |
| Blast radius / "What breaks if I change X?" | `.claude/skills/gitnexus/gitnexus-impact-analysis/SKILL.md` |
| Trace bugs / "Why is X failing?" | `.claude/skills/gitnexus/gitnexus-debugging/SKILL.md` |
| Rename / extract / split / refactor | `.claude/skills/gitnexus/gitnexus-refactoring/SKILL.md` |
| Tools, resources, schema reference | `.claude/skills/gitnexus/gitnexus-guide/SKILL.md` |
| Index, status, clean, wiki CLI commands | `.claude/skills/gitnexus/gitnexus-cli/SKILL.md` |
| Work in the Appsec area (152 symbols) | `.claude/skills/generated/appsec/SKILL.md` |
| Work in the Tests area (114 symbols) | `.claude/skills/generated/tests/SKILL.md` |
| Work in the Services area (113 symbols) | `.claude/skills/generated/services/SKILL.md` |
| Work in the Ui area (106 symbols) | `.claude/skills/generated/ui/SKILL.md` |
| Work in the Securacymcp area (101 symbols) | `.claude/skills/generated/securacymcp/SKILL.md` |
| Work in the Privacy area (73 symbols) | `.claude/skills/generated/privacy/SKILL.md` |
| Work in the _components area (65 symbols) | `.claude/skills/generated/components/SKILL.md` |
| Work in the Dfd area (58 symbols) | `.claude/skills/generated/dfd/SKILL.md` |
| Work in the Components area (31 symbols) | `.claude/skills/generated/components-2/SKILL.md` |
| Work in the Threats_modules area (26 symbols) | `.claude/skills/generated/threats-modules/SKILL.md` |
| Work in the DB area (25 symbols) | `.claude/skills/generated/db/SKILL.md` |
| Work in the Hooks area (16 symbols) | `.claude/skills/generated/hooks/SKILL.md` |
| Work in the Routes area (12 symbols) | `.claude/skills/generated/routes/SKILL.md` |
| Work in the Benchmark area (7 symbols) | `.claude/skills/generated/benchmark/SKILL.md` |
| Work in the Contact area (5 symbols) | `.claude/skills/generated/contact/SKILL.md` |
| Work in the Onboarding area (4 symbols) | `.claude/skills/generated/onboarding/SKILL.md` |
| Work in the Context area (4 symbols) | `.claude/skills/generated/context/SKILL.md` |
| Work in the E2e area (3 symbols) | `.claude/skills/generated/e2e/SKILL.md` |
| Work in the Cluster_98 area (3 symbols) | `.claude/skills/generated/cluster-98/SKILL.md` |

<!-- gitnexus:end -->
