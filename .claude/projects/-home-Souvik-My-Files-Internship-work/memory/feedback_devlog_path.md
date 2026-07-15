---
name: DEVLOG canonical path
description: Every change made must be logged to tasks/DEVLOG.md (not docs/DEVLOG.md) with full details and reasoning
type: feedback
---

Always log ALL changes — code edits, bug fixes, features, architectural decisions, security findings — to `tasks/DEVLOG.md`.

**Why:** User explicitly set this as the canonical DEVLOG path for this project. The CLAUDE.md previously referenced `docs/DEVLOG.md` but the actual file lives at `tasks/DEVLOG.md`.

**How to apply:** After every non-trivial change, append an entry to `tasks/DEVLOG.md` following the Section 9 format in CLAUDE.md (type tag, files affected, what happened, status, reasoning). Never skip this step and never write to `docs/DEVLOG.md`.