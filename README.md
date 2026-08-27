# Agent Skills & Agentic Tools Framework

> A universal, multi-platform AI agent ecosystem providing **20 specialist agents**, **50+ domain skills**, **11 workflows**, and **automated verification scripts** for modern AI-assisted software engineering.

Designed and maintained by **Souvik Chakraborty** as a portable, standardized baseline toolkit compatible across **Antigravity (Gemini)**, **Claude Code**, **OpenAI Codex CLI**, **GitHub Copilot in VS Code**, **Cursor**, and **Windsurf**.

---

## 🌟 Overview

Modern AI coding agents excel when guided by structured domain knowledge, modular skills, and specialized personas. This repository serves as a **universal master library** that you can drop into any project to provide instant, expert-level AI capabilities.

### Key Capabilities
- 🤖 **20 Specialist Personas**: Role-based agents (Frontend, Backend, Database Architect, Security Auditor, Debugger, Test Engineer, etc.).
- 🧩 **50+ Modular Domain Skills**: In-depth architecture guides, patterns, and cheatsheets (React, Next.js, FastAPI, Go, Tailwind CSS v4, Postgres, MCP Builder, Security Scanners, etc.).
- 🔄 **11 Slash-Command Workflows**: Structured procedures for brainstorming, step-by-step planning, automated UI token lookups (`/ui-ux-pro-max`), systematic debugging, and multi-agent orchestration.
- 🛡️ **Automated Validation Scripts**: Built-in Python scripts for linting, security audits, schema checks, and accessibility verification (`checklist.py`, `verify_all.py`).
- 🌐 **Cross-Platform Compatibility**: Native configuration files for every major AI coding assistant.

---

## 📁 Repository Architecture

```plaintext
agent-skills-agentic-tools/
├── .agents/                        # Universal / Antigravity workspace customizations root
│   ├── agents/                     # 20 specialist persona definition files (*.md)
│   ├── skills/                     # 50 modular domain skills with SKILL.md and scripts
│   ├── workflows/                  # Slash-command procedures (/brainstorm, /debug, /plan, etc.)
│   ├── scripts/                    # Master validation scripts (checklist.py, verify_all.py)
│   ├── rules/                      # System rules (GEMINI.md, CLAUDE.md)
│   └── .shared/                    # Shared design token data (ui-ux-pro-max palettes/fonts)
│
├── .claude/                        # Claude Code (Anthropic CLI) configuration
│   ├── agents/                     # Specialist agent prompts
│   ├── commands/                   # Claude slash commands (/security-review, /think, etc.)
│   ├── skills/                     # Domain knowledge modules
│   ├── security/                   # False-positive filtering & custom scan configs
│   └── tools.json                  # Tools registry
│
├── .codex/                         # OpenAI Codex CLI configuration
│   ├── agents/                     # Agent definitions in TOML format (*.toml)
│   └── hooks.json                  # Session lifecycle hooks & context monitor
│
├── .github/
│   └── copilot-instructions.md     # Custom instructions for GitHub Copilot in VS Code
│
├── AGENTS.md                       # Master orchestration guide (Antigravity, Cursor, Windsurf, Codex)
├── CLAUDE.md                       # Master orchestration guide for Claude Code
├── README.md                       # Project overview and setup instructions
├── CONTRIBUTING.md                 # Guidelines for adding new skills, agents, and workflows
│
└── tasks/                          # Project memory and error tracking (created per project)
    ├── DEVLOG.md                   # Auto-maintained change, decision, and bug log
    └── lessons.md                  # Anti-pattern database & persistent mistake memory
```

---

## 🚀 How to Setup in Any Project

You can easily copy this framework into any new or existing software repository. Choose the setup option that matches your workflow:

### Option 1: Universal Setup (All AI Agents Supported)
To enable full support across all AI tools (Antigravity, Claude Code, GitHub Copilot, Cursor, Windsurf):

1. Copy the following folders and files into the root of your target project:
   ```bash
   cp -r .agents /path/to/your-project/
   cp -r .claude /path/to/your-project/
   cp -r .github /path/to/your-project/
   cp AGENTS.md CLAUDE.md /path/to/your-project/
   ```
2. Create a `tasks/` directory in your project root:
   ```bash
   mkdir -p /path/to/your-project/tasks
   touch /path/to/your-project/tasks/DEVLOG.md
   touch /path/to/your-project/tasks/lessons.md
   ```

---

### Option 2: Tool-Specific Setup

#### For Google Antigravity / Gemini IDE:
Copy the `.agents/` folder and `AGENTS.md`:
```bash
cp -r .agents /path/to/your-project/
cp AGENTS.md /path/to/your-project/
```

#### For GitHub Copilot in VS Code:
Copy the `.github/` folder and `.agents/`:
```bash
cp -r .github /path/to/your-project/
cp -r .agents /path/to/your-project/
```
*VS Code will automatically load `.github/copilot-instructions.md` and reference `.agents/skills/`.*

#### For Claude Code (Anthropic CLI):
Copy the `.claude/` folder and `CLAUDE.md`:
```bash
cp -r .claude /path/to/your-project/
cp CLAUDE.md /path/to/your-project/
```

#### For OpenAI Codex CLI:
Copy the `.codex/` folder and `AGENTS.md`:
```bash
cp -r .codex /path/to/your-project/
cp AGENTS.md /path/to/your-project/
```

---

## 🤖 Specialist Agents (20)

Tasks are automatically routed to the right specialist persona based on request keywords:

| Agent | Focus Area | Key Associated Skills |
| :--- | :--- | :--- |
| `orchestrator` | Multi-agent coordination (3+ domains) | `parallel-agents`, `behavioral-modes` |
| `project-planner` | Socratic discovery, technical specs, planning | `brainstorming`, `plan-writing`, `architecture` |
| `frontend-specialist` | Web UI/UX, responsive layouts, components | `frontend-design`, `react-patterns`, `tailwind-patterns`, `theme-factory` |
| `backend-specialist` | APIs, services, business logic | `api-patterns`, `python-patterns`, `nodejs-best-practices`, `golang` |
| `database-architect` | Schema design, SQL queries, migrations | `database-design`, `database-migrations` |
| `mobile-developer` | iOS, Android, React Native, Flutter | `mobile-design` |
| `game-developer` | Game mechanics, rendering loops | `game-development` |
| `devops-engineer` | CI/CD pipelines, Docker, cloud deployment | `deployment-procedures`, `server-management` |
| `security-auditor` | Vulnerability assessment, OWASP compliance | `vulnerability-scanner`, `file-security`, `red-team-tactics` |
| `penetration-tester` | Offensive security verification | `red-team-tactics`, `vulnerability-scanner` |
| `debugger` | Systematic root-cause investigation | `systematic-debugging` |
| `test-engineer` | Unit, integration, and E2E testing | `testing-patterns`, `tdd-workflow`, `webapp-testing` |
| `performance-optimizer` | Web Vitals, profiling, bundle reduction | `performance-profiling` |
| `seo-specialist` | SEO, E-E-A-T, and Generative AI search (GEO) | `seo-fundamentals`, `geo-fundamentals` |
| `documentation-writer` | API docs, architecture specs, READMEs, technical blog posts | `documentation-templates`, `tech-blogging` |
| `product-manager` | PRDs, user stories, requirements | `plan-writing`, `brainstorming` |
| `product-owner` | Roadmaps, backlog grooming, MVP scope | `plan-writing`, `brainstorming` |
| `qa-automation-engineer` | Automated test suites & CI regression | `webapp-testing`, `testing-patterns` |
| `code-archaeologist` | Legacy code refactoring, dead code cleanup | `clean-code`, `code-review-checklist` |
| `explorer-agent` | Codebase mapping & architecture discovery | `gitnexus` |

---

## 🧩 Modular Skills (51)

Skills are loaded on demand by reading their `SKILL.md` file:

- **Frontend & Design**: `frontend-design`, `react-patterns`, `nextjs-best-practices`, `tailwind-patterns`, `theme-factory`, `web-artifacts-builder`, `ui-ux-pro-max`.
- **Backend & APIs**: `api-patterns`, `python-patterns`, `nodejs-best-practices`, `golang`, `mcp-builder`, `mcporter`.
- **Databases**: `database-design`, `database-migrations`.
- **Security**: `vulnerability-scanner`, `file-security`, `red-team-tactics`.
- **Testing & Quality**: `testing-patterns`, `webapp-testing`, `tdd-workflow`, `code-review-checklist`, `lint-and-validate`, `playwright-dev`.
- **Architecture & Workflow**: `clean-code`, `architecture`, `app-builder`, `brainstorming`, `plan-writing`, `behavioral-modes`, `parallel-agents`, `systematic-debugging`.
- **Operations & Systems**: `deployment-procedures`, `server-management`, `bash-linux`, `powershell-windows`, `performance-profiling`.
- **SEO, Content & Growth**: `seo-fundamentals`, `geo-fundamentals`, `i18n-localization`, `tech-blogging`.
- **Specialized Utilities**: `gitnexus`, `pdf`, `skill-creator`, `dfd-analysis`, `source-command-gsd-*`.

---

## 🛠️ Validation Scripts

Run pre-configured validation scripts before committing or deploying code:

```bash
# Priority audit (Security -> Lint -> Schema -> Tests -> UX -> SEO)
python .agents/scripts/checklist.py .

# Full verification suite (including Lighthouse & Playwright E2E)
python .agents/scripts/verify_all.py . --url http://localhost:3000

# Individual specialized checks:
python .agents/skills/vulnerability-scanner/scripts/security_scan.py .
python .agents/skills/frontend-design/scripts/ux_audit.py .
python .agents/skills/database-design/scripts/schema_validator.py .
```

---

## 🤝 Contributing

To learn how to create new skills, agents, or workflows, please check [CONTRIBUTING.md](CONTRIBUTING.md).

---

## 📄 License

MIT License. Free to use, modify, and distribute across all personal and commercial projects.
