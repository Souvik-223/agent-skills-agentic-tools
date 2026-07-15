---
description: Update the project devlog with changes made, bugs found, edge cases, and resolution status. Run after any non-trivial implementation, debugging session, or security review.
---

# Devlog Update Workflow

Update `docs/DEVLOG.md` with a structured entry for the current session.

## ARGUMENTS
$ARGUMENTS

If no arguments provided, summarize the current session automatically based on what was done.

---

## STEP 1: Read current devlog state

Read `docs/DEVLOG.md` to understand existing entries and avoid duplicates.
If file does not exist, create it with the template structure.

## STEP 2: Determine entry type

Classify what happened in the session:

| Type | Use when |
|---|---|
| `CHANGE` | New feature, refactor, or code modification implemented |
| `BUG` | A bug was identified (resolved or not) |
| `EDGE_CASE` | An edge case was discovered during implementation or review |
| `SECURITY` | Security vulnerability found via `/security-review` |
| `DECISION` | An architectural or design decision was made |
| `BLOCKED` | Work stopped due to an unresolved issue |

## STEP 3: Write the entry

Append to `docs/DEVLOG.md` under today's date section. Format:

```markdown
## [YYYY-MM-DD] — Session Title

### [TYPE] Entry Title
- **Files affected:** `path/to/file.py`, `path/to/other.js`
- **What happened:** Clear description of what was done, found, or decided
- **Status:** ✅ Resolved | ⚠️ Partial | ❌ Unresolved | 🔍 Investigating
- **Resolution:** (if resolved) What was done to fix/implement it
- **Open questions:** (if unresolved) What is still unclear or blocking
- **Edge cases noted:** List any edge cases discovered, even if not yet handled
- **Linked to:** (optional) Related bug IDs, PR numbers, CAPEC IDs for security issues
```

## STEP 4: Update summary table

Keep the summary table at the top of DEVLOG.md current:

```markdown
| Date | Type | Title | Status |
|------|------|-------|--------|
| YYYY-MM-DD | BUG | Short title | ❌ Unresolved |
```

Sort by date descending (newest first).

## STEP 5: Verify

After writing, read back the entry to confirm it is accurate and complete. Do not add speculation — only log what actually happened or was concretely identified.
