# Contributing to the Agent Skills & Agentic Tools Framework

Thank you for contributing! This guide explains how to create, format, and add new **Skills**, **Specialist Agents**, and **Workflows** to maintain a clean, modular, and cross-platform architecture.

---

## 🏗️ Architecture & Conventions

When contributing, ensure your additions conform to the multi-platform structure:

```
.agents/
├── skills/          → Domain knowledge modules (<skill-name>/SKILL.md)
├── agents/          → Specialist agent personas (<agent-name>.md)
├── workflows/       → Slash commands & procedures (<workflow-name>.md)
└── scripts/         → Validation & audit scripts
```

---

## 1. How to Add a New Skill

Skills are domain knowledge modules loaded on demand by AI agents when relevant keywords or tasks are detected.

### Step 1: Create the Skill Directory
Create a directory under `.agents/skills/<skill-name>/` (and mirror to `.claude/skills/<skill-name>/` if targeting Claude Code):

```plaintext
.agents/skills/<skill-name>/
├── SKILL.md                 # (Required) Main instructions & YAML frontmatter
├── scripts/                 # (Optional) Python / shell helper scripts
├── references/              # (Optional) Extended specs, cheatsheets, templates
└── assets/                  # (Optional) Static assets or starter code
```

### Step 2: Write `SKILL.md`
Every skill MUST have a valid YAML frontmatter at the top of `SKILL.md`:

```markdown
---
name: my-new-skill
description: Comprehensive guidelines for building X. Use when designing X, handling Y, or troubleshooting Z.
---

# My New Skill Title

> Concise summary of the skill's purpose and principles.

---

## 1. When to Apply
- Keyword triggers: `keyword1`, `keyword2`, `keyword3`
- Scenarios: When building feature X or refactoring Y

---

## 2. Core Architecture & Patterns
- Key principles and rules
- Code examples and best practices

---

## 3. Anti-Patterns & Common Pitfalls
- What NOT to do
- Common bugs and edge cases to avoid

---

## 4. Helper Scripts & Verification
- `python .agents/skills/my-new-skill/scripts/audit_tool.py .`
```

### Step 3: Register the Skill
Add the skill to the quick-reference tables in:
1. [`AGENTS.md`](AGENTS.md) (Section 4 — Skill Loading Protocol)
2. [`CLAUDE.md`](CLAUDE.md) (Section 4)
3. [`.github/copilot-instructions.md`](.github/copilot-instructions.md) (Section 3)

---

## 2. How to Add a New Specialist Agent

Specialist agents represent expert personas tailored to a specific domain (e.g., Security, UI/UX, Backend, QA).

### Step 1: Create the Agent Definition
1. **For Antigravity & Universal Agents**: Create `.agents/agents/<agent-name>.md`
2. **For Claude Code**: Create `.claude/agents/<agent-name>.md`
3. **For OpenAI Codex CLI**: Create `.codex/agents/<agent-name>.toml`

### Step 2: Structure the Markdown Agent File (`.agents/agents/<agent-name>.md`)

```markdown
---
name: my-specialist-agent
description: Specialist in X domain. Handles tasks related to A, B, and C.
skills:
  - clean-code
  - my-new-skill
  - relevant-skill-2
---

# My Specialist Agent Persona

> You are a senior specialist in [Domain]. Your goal is to [Core Mission].

---

## Directives & Persona
- Always prioritize [key priority].
- Adhere strictly to clean-code standards and test-driven development.

## Decision Matrix & Workflow
1. Analyze requirements.
2. Cross-reference domain rules in referenced skills.
3. Generate minimal, production-ready implementations.
```

### Step 3: Structure the Codex Agent File (`.codex/agents/<agent-name>.toml`)

```toml
name = "my-specialist-agent"
description = "Specialist in X domain. Handles tasks related to A, B, and C."
skills = ["clean-code", "my-new-skill"]

[persona]
role = "Senior Specialist in [Domain]"
instructions = """
Detailed instructions for the Codex model...
"""
```

### Step 4: Update Routing Tables
Update the Intelligent Routing table in [`AGENTS.md`](AGENTS.md), [`CLAUDE.md`](CLAUDE.md), and [`.github/copilot-instructions.md`](.github/copilot-instructions.md) with keyword triggers for your new agent.

---

## 3. How to Add a New Workflow (Slash Command)

Workflows provide structured step-by-step procedures triggered via slash commands (e.g. `/brainstorm`, `/plan`, `/debug`).

### Step 1: Create the Workflow File
Add `.agents/workflows/<workflow-name>.md`:

```markdown
# /workflow-name — Workflow Title

> Description of the workflow and when to invoke it.

---

## Phase 1: Discovery & Analysis
- Questions to ask before proceeding.
- Information gathering steps.

## Phase 2: Execution
- Concrete execution steps.
- Checklist to satisfy.

## Phase 3: Verification & Logging
- Validation commands to execute.
- Log completion in `tasks/DEVLOG.md`.
```

### Step 2: Register the Workflow Command
Add the command to the workflow tables in [`AGENTS.md`](AGENTS.md) and [`CLAUDE.md`](CLAUDE.md).

---

## 4. Quality Checklist Before Submitting

Before finalizing any new additions, verify the following:

- [ ] `SKILL.md` contains valid YAML frontmatter (`name` and `description`).
- [ ] No hardcoded personal paths, author-specific machine directories, or proprietary credentials exist.
- [ ] Internal file links use relative paths or standard workspace formatting.
- [ ] Scripts in `scripts/` are executable and tested with Python 3.10+.
- [ ] Run the project audit script:
  ```bash
  python .agents/scripts/checklist.py .
  ```
