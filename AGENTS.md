# AGENTS.md — Codex Project Operating Instructions

> **Purpose:** This file is the project-specific **80% layer** for Codex.  
> Place it in the repository root and commit it with the project.

---

## 1. Project profile

| Field | Project value |
|---|---|
| Project name | `seethestars` |
| Product purpose | Claude Code plugin marketplace registry — hosts `seethestars-plugins`, enabling installation of skill collections and security plugins |
| Primary users | kellyblaze (owner); Claude Code users who add this marketplace |
| Repository type | Plugin/configuration registry (no application source code) |
| Primary language(s) | JSON, Markdown |
| Framework(s) | Claude Code plugin system |
| Package manager | npm (available; no `package.json` in repo root) |
| Database/storage | None |
| Authentication | None (GitHub authorization implicit) |
| Hosting/deployment | GitHub — `kellyblaze/seethestars` |
| Production branch | `main` |
| Issue tracker | GitHub Issues (kellyblaze/seethestars) |
| CI provider | None found |
| Current autonomy ceiling | `L1 — report-only` |
| Project owner/approver | `kellyblaze` |

### Placeholder rule

When a value remains marked `REPLACE` or `DISCOVER AND CONFIRM`, inspect authoritative project files and report — do not silently update this file.

---

## 2. Codex's role in this project

Act as the **worktree-isolated implementation and maintenance supervisor**.

Responsibilities:

- understand the repository before changing it;
- plan bounded changes to plugin config and loop files;
- implement only approved scope;
- use independent verification;
- run deterministic checks (JSON validation, `loop doctor`, `loop sync`);
- maintain durable loop state;
- prepare reviewable diffs and evidence;
- stop at approval gates.

Codex is not authorized by this file alone to push, merge, release, deploy, access production, send communications, modify secrets, or perform destructive operations.

---

## 3. Instruction hierarchy

Apply in order:

1. Platform and organization policies.
2. The user's explicit current task.
3. This root `AGENTS.md`.
4. More specific nested `AGENTS.md` files for relevant directories.
5. `LOOP.md`, `gate.yaml`, `loop-constraints.md`, and `loop-budget.md`.
6. The approved task scope.
7. Existing repository conventions.

A more specific instruction may refine a broad instruction. It must not silently weaken a security, privacy, approval, or evidence requirement.

When instructions conflict materially, stop and report the conflict.

---

## 4. Repository map

```text
.claude/
  settings.json           Marketplace registration + enabled plugins (PROTECTED)
  agents/                 loop-verifier, planner (project-local)
  skills/                 loop-triage, loop-budget, loop-constraints
.claude-plugin/
  marketplace.json        42-plugin registry (PROTECTED)
plugins/
  frontend-design/        Installed plugin source
LOOP.md                   Loop contract
STATE.md                  Durable state
loop-budget.md            Limits
loop-constraints.md       Binding constraints
loop-run-log.md           Append-only log
```

### High-risk paths — require explicit approval before editing

```text
.claude/settings.json
.claude-plugin/marketplace.json
.loop-setup-backup/
```

---

## 5. Verified project commands

This is a configuration-only repository. There are no application build, lint, typecheck, or test commands.

```text
Install dependencies:       NOT APPLICABLE
Start development server:   NOT APPLICABLE
Lint:                       NOT APPLICABLE
Format check:               NOT APPLICABLE
Typecheck:                  NOT APPLICABLE
Unit tests:                 NOT APPLICABLE
Integration tests:          NOT APPLICABLE
End-to-end tests:           NOT APPLICABLE
Build:                      NOT APPLICABLE

JSON validation (marketplace.json):
  node -e "JSON.parse(require('fs').readFileSync('.claude-plugin/marketplace.json','utf8'))"

Loop Engineering validation:
  npx @cobusgreyling/loop doctor .
  npx @cobusgreyling/loop sync .
```

Never invent a command. When a command is unknown, mark it `UNKNOWN` and request confirmation.

---

## 6. Architecture and conventions

### Architecture

```text
seethestars is a Claude Code plugin marketplace registry.

.claude-plugin/marketplace.json defines all plugins available under the
seethestars-plugins marketplace. Users install plugins via:
  /plugin install <name>@seethestars-plugins

.claude/settings.json registers the marketplace with Claude Code and lists
which plugins are auto-enabled when the repo is opened.

plugins/<name>/ contains locally installed plugin source (skills, README).

No runtime server, database, auth, or payments exist.
```

### Non-negotiable invariants

```text
- marketplace.json must remain valid JSON at all times.
- Plugin entries must reference reachable source repositories.
- .claude/settings.json changes must not silently disable existing enabled plugins.
- Loop files must remain consistent (loop doctor ≥ 80/100 after any loop-file edit).
```

### Conventions

```text
- Plugin names: lowercase-hyphenated
- JSON: 2-space indentation; validate before commit
- Markdown: GitHub-flavored
- Loop files: stable IDs, append-only logs, deduplicated state
- Branches: claude/<name> pattern observed
```

---

## 7. Loop Engineering files

| File | Purpose |
|---|---|
| `LOOP.md` | Loop purpose, cadence, and stop conditions |
| `STATE.md` | Durable state, open findings, blockers |
| `gate.yaml` | Approval gates — not yet created; needed before L2 |
| `loop-budget.md` | Runtime and retry limits |
| `loop-constraints.md` | Binding loop constraints |
| `loop-run-log.md` | Append-only run log |
| `TASK_SCOPE.md` | Per-task boundaries — created and archived per task |

Read `STATE.md` before substantial work. Absence of loop files is not permission for broad action — remain L1 and recommend creating them.

---

## 8. Autonomy levels

### L0 — Orientation
Read, map, explain, propose. No edits.

### L1 — Report-only (current ceiling)
Run non-destructive checks, triage, update approved loop-state files, prepare implementation packets. No source edits.

### L2 — Assisted implementation
Requires an explicit approved task scope and a dedicated worktree. May edit approved files and prepare a commit/PR description. Still requires human approval before committing, pushing, or opening a PR.

### L3 — Unattended allowlisted work
Permitted only when `gate.yaml` explicitly allows the task category, a proven L2 history exists, and all L3 prerequisites are met. Default to L1 when unclear.

---

## 9. One-active-writer and worktree policy

- One designated implementer owns the worktree.
- Planner and verifier remain read-only.
- Parallel tasks use separate worktrees with non-overlapping file scope.
- Cowork or Claude Code must not edit Codex's active worktree.

Confirm before editing:

```text
Current branch:
Worktree path:
Designated writer:
Allowed files:
Prohibited files:
```

---

## 10. Standard task workflow

**Step 1 — Orient:** Read this file, LOOP.md, STATE.md, loop-constraints.md, and relevant config files. Run `git status`.

**Step 2 — Restate the task:** Objective, current behavior, desired behavior, scope, risk, approvals needed, verification plan.

**Step 3 — Plan:** Identify files to change, rollback, stop conditions. For substantial work, create `TASK_SCOPE.md`.

**Step 4 — Implement:** Smallest coherent change. Follow existing JSON/Markdown conventions. Validate JSON after edits. Do not touch protected paths without approval.

**Step 5 — Verify deterministically:** Run JSON validation and/or `loop doctor` / `loop sync` as appropriate. Capture exact command and output.

**Step 6 — Independent verification:** Use a verifier that did not implement. Verifier starts from requirements and diff — not the implementer's narrative. Returns PASS, PASS WITH CONDITIONS, or FAIL.

**Step 7 — Report:** Files changed, commands run, outcomes, verifier verdict, remaining risks, approvals still needed.

**Step 8 — Update state:** Update STATE.md and append to loop-run-log.md only when authorized.

---

## 11. Mandatory human approval gates

Always stop before:

- any change to `.claude/settings.json` or `.claude-plugin/marketplace.json`;
- adding or removing plugins from the marketplace;
- Git commit, push, PR creation, merge, or release;
- creating or modifying `.github/` workflows;
- changes with uncertain legal, privacy, or compliance impact.

Approval for one action does not imply approval for later actions.

---

## 12. Git policy

Allowed without authorization: `git status`, `git diff`, `git log`, branch inspection.

Require explicit authorization for: `git add`, `git commit`, `git push`, PR creation, merge, rebase that changes shared history, tags, branch deletion.

Never force-push. Never discard uncommitted work you did not create.

Production branch is unresolved — confirm before any merge or release action.

---

## 13. Failure handling

Stop and escalate when:

- the same material failure occurs twice without new evidence;
- requirements are contradictory;
- the working tree is unexpectedly dirty;
- a protected path is required but not approved;
- verification cannot distinguish success from failure.

Classify failures: `environment`, `dependency`, `test`, `requirements ambiguity`, `permission boundary`, `tool outage`, `model reasoning`, `scope drift`, `external service`.

Do not retry blindly.

---

## 14. First-session bootstrap (completed)

Initial scaffold produced `LOOP_SETUP_READINESS_REPORT.md`. Next session should:

1. Confirm production branch with owner.
2. Create `gate.yaml`.
3. Add permissions block to `.claude/settings.json`.
4. Run three L1 triage sessions.
5. Pilot one bounded L2 task.

---

## 15. Project-specific additions

```text
- No application source code exists. L2 work is bounded to:
    .claude-plugin/marketplace.json
    plugins/<name>/
    loop files
    .claude/settings.json

- JSON changes to marketplace.json require validation before commit.

- The production branch is unresolved. Do not merge or release until confirmed.
```
