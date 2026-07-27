# CLAUDE.md — Claude Code Project Operating Instructions

> **Purpose:** This file is the project-specific **80% layer** for Claude Code.  
> The universal operating agreement lives in `~/.claude/CLAUDE.md`.  
> This file takes precedence on project-specific matters.

---

## 1. Project profile

| Field | Project value |
|---|---|
| Project name | `seethestars` |
| Product purpose | Claude Code plugin marketplace registry — hosts `seethestars-plugins`, enabling kellyblaze to install skill collections and security tools in Claude Code |
| Primary users | kellyblaze (owner); any Claude Code user who adds this marketplace |
| Repository type | Plugin/configuration registry (no application source code) |
| Primary language(s) | JSON, Markdown |
| Framework(s) | Claude Code plugin system (`.claude-plugin/marketplace.json`, `plugins/*/`) |
| Package manager | npm (available; no `package.json` in repo root) |
| Database/storage | None |
| Authentication | None (GitHub authorization implicit) |
| Hosting/deployment | GitHub — `kellyblaze/seethestars` |
| Production branch | `[UNRESOLVED — no main/master exists; confirm with owner]` |
| CI provider | None found |
| Current autonomy ceiling | `L1 — report-only` |
| Project owner/approver | `kellyblaze` (kellyblazeent@gmail.com) |

When a field is unresolved, inspect and report evidence. Do not guess or silently modify these instructions.

---

## 2. Claude Code's role in this project

Act as the **primary deep implementation, debugging, and self-verifying engineering agent** when explicitly designated as the writer.

Use Claude Code for:

- repository exploration;
- implementation planning;
- bounded changes to plugin configuration, marketplace registry, and loop files;
- maker/checker workflows;
- hook-assisted validation;
- measurable `/goal` tasks;
- active-session `/loop` polling;
- project-local skills and subagents.

This file does not authorize push, merge, release, deployment, production access, external communications, secrets changes, or destructive actions.

---

## 3. Instruction and memory hierarchy

Apply:

1. Platform, organization, and managed policies.
2. The user's explicit current task.
3. User-level `~/.claude/CLAUDE.md`.
4. This project `CLAUDE.md`.
5. Relevant `.claude/rules/` and nested instructions.
6. `LOOP.md`, `gate.yaml`, `loop-constraints.md`, and `loop-budget.md`.
7. The current approved task scope.
8. Existing repository conventions.
9. Auto memory, only when it does not conflict with verified project facts.

When instructions conflict materially, stop and report the conflict.

---

## 4. Repository map

```text
.claude/                  Claude Code project configuration
  settings.json           Marketplace registration + enabled plugins
  agents/                 Project-local subagents (loop-verifier, planner, etc.)
  skills/                 Project-local skills (loop-triage, loop-budget, loop-constraints)
.claude-plugin/
  marketplace.json        42-plugin marketplace registry (seethestars-plugins)
plugins/
  frontend-design/        Installed plugin with skills and README
LOOP.md                   Loop Engineering contract
STATE.md                  Durable loop state
loop-budget.md            Runtime and retry limits
loop-constraints.md       Binding loop constraints
loop-run-log.md           Append-only run history
.loop-setup-backup/       Backup of pre-scaffold config files
LOOP_SETUP_READINESS_REPORT.md   Initial setup audit
```

### Protected paths

Do not edit these without explicit approval:

```text
.claude/settings.json           Marketplace config — changes affect plugin installation
.claude-plugin/marketplace.json Plugin registry — changes affect all marketplace users
.loop-setup-backup/             Backup — do not modify
```

---

## 5. Verified commands

This is a configuration-only repository. There are no application build, test, lint, or typecheck commands.

```text
Install dependencies:       NOT APPLICABLE (no package.json)
Start development server:   NOT APPLICABLE
Lint:                       NOT APPLICABLE
Format check:               NOT APPLICABLE
Typecheck:                  NOT APPLICABLE
Unit tests:                 NOT APPLICABLE
Integration tests:          NOT APPLICABLE
End-to-end tests:           NOT APPLICABLE
Build:                      NOT APPLICABLE
Database validation:        NOT APPLICABLE
Security scan:              NOT APPLICABLE

Loop Engineering validation:
  npx @cobusgreyling/loop doctor .
  npx @cobusgreyling/loop sync .
```

Never invent commands. Do not install dependencies merely to test a guess.

---

## 6. Architecture and project conventions

### Architecture summary

```text
seethestars is a Claude Code plugin marketplace registry.

Structure:
  .claude-plugin/marketplace.json  — defines all available plugins for the
                                     seethestars-plugins marketplace
  plugins/<name>/                  — installed plugin source (skills, README)
  .claude/settings.json            — registers the marketplace and enables plugins

Plugins are sourced from external GitHub repositories. The marketplace.json
references each plugin's source repo, version, and category. Users install
plugins via `/plugin install <name>@seethestars-plugins`.

No runtime server, database, authentication, or payment system exists.
```

### Invariants

```text
- marketplace.json must remain valid JSON conforming to the Claude Code marketplace schema.
- Plugin entries must reference real, reachable source repositories.
- .claude/settings.json must not be modified in a way that disables existing enabled plugins
  without the owner's explicit approval.
- The .loop-setup-backup/ directory is read-only after creation.
```

### Conventions

```text
- Naming: plugin names are lowercase-hyphenated (e.g. frontend-design, loop-triage)
- File placement: plugin config in .claude-plugin/; installed plugin source in plugins/<name>/
- JSON: 2-space indentation; valid against schema before committing
- Markdown: standard GitHub-flavored Markdown
- Loop files: follow Loop Engineering conventions (stable IDs, append-only logs)
- Branches: claude/<name> pattern observed; no main/master confirmed yet
```

---

## 7. Project-local Claude configuration

```text
CLAUDE.md                         This file
CLAUDE.local.md                   Private notes — add to .gitignore if created
.claude/settings.json             Shared permissions and marketplace config
.claude/settings.local.json       Personal overrides — do not commit
.claude/agents/                   planner, verifier, loop-verifier
.claude/skills/                   loop-triage, loop-budget, loop-constraints
.claude/hooks/                    [not yet created]
.claude/rules/                    [not yet created]
```

---

## 8. Loop Engineering files

| File | Purpose |
|---|---|
| `LOOP.md` | Loop contract and stop conditions |
| `STATE.md` | Durable project and loop state |
| `gate.yaml` | Approval boundaries — not yet created; create before L2 |
| `loop-budget.md` | Runtime, retry, and scope limits |
| `loop-constraints.md` | Allowed paths and prohibited actions |
| `loop-run-log.md` | Append-only loop history |
| `TASK_SCOPE.md` | Current task boundaries — created per task, then archived |

Read and maintain these when present. If absent, default to L1 and recommend setup.

---

## 9. Autonomy levels

### L0 — Orientation
Read, map, explain, propose. No edits.

### L1 — Report-only (current ceiling)
Run non-destructive checks, triage, update approved state/loop files, prepare implementation packets. No application-code edits.

### L2 — Assisted implementation
Requires an explicit task scope. May edit approved files (marketplace.json, plugin source, loop files). Approval still required for commits, push, PR creation, and all protected categories.

### L3 — Unattended allowlisted work
Requires explicit `gate.yaml` allowance, proven L2 history, sandboxing, and human-reviewed scheduling. Do not use until L2 is stable.

Default to L1 whenever the level is unclear.

---

## 10. One-active-writer rule

Only one designated agent may edit the active branch or worktree.

- Planner subagents are read-only.
- Verifier subagents are read-only.
- Parallel implementers require separate worktrees and non-overlapping files.
- Cowork or Codex must not edit Claude Code's active worktree.

---

## 11. Standard Claude Code workflow

**Phase 1 — Orient:** Read this file, LOOP.md, STATE.md, loop-constraints.md, and the relevant plugin/config files. Run `git status`.

**Phase 2 — Define the task:** Restate objective, scope, risk, required approvals, and verification plan.

**Phase 3 — Plan:** Use the `plan-change` skill or a concise written plan. Identify expected files, rollback, and stop conditions.

**Phase 4 — Implement:** The designated implementer makes the smallest coherent change following existing JSON/Markdown conventions. No unrelated changes.

**Phase 5 — Deterministic checks:** Run `npx @cobusgreyling/loop doctor .` and `npx @cobusgreyling/loop sync .` after loop-file changes. Validate JSON manually or with `node -e "JSON.parse(require('fs').readFileSync('.claude-plugin/marketplace.json','utf8'))"` after marketplace changes.

**Phase 6 — Independent verifier:** Use `verify-change` skill or `loop-verifier` agent.

**Phase 7 — Final review:** Review the full diff via `review-diff` skill.

**Phase 8 — State and report:** Update STATE.md and loop-run-log.md when authorized.

---

## 12. Mandatory human approval gates

Stop before:

- any change to `.claude/settings.json` or `.claude-plugin/marketplace.json`;
- adding or removing plugins from the marketplace;
- Git commit, push, PR creation, merge, or release;
- creating or modifying `.github/` CI workflows;
- changes with uncertain legal, privacy, or compliance impact.

Authorization is action-specific and does not carry forward automatically.

---

## 13. Permissions and sandbox

Current `.claude/settings.json` has marketplace/plugin config only — no permissions block yet. Until a permissions block is added:

- treat all `git push`, `git commit`, and `npm install` as requiring explicit approval each time;
- do not use bypass-permissions mode;
- do not execute unreviewed downloaded scripts.

Recommended next step: add a conservative `permissions` block per the Loop Engineering guide (Section 8).

---

## 14. Git policy

Allowed without authorization: `git status`, `git diff`, `git log`, branch inspection.

Require explicit authorization for: staging, committing, pushing, PR creation, rebasing, merging, releases, branch deletion.

Never force-push. Never discard work you did not create.

Production branch is unresolved — confirm before any merge or release action.

---

## 15. Definition of done

A task is complete only when:

- the approved behavior exists;
- the diff remains within scope;
- any changed JSON files are valid;
- `loop doctor` and `loop sync` pass after loop-file changes;
- the final diff is reviewed;
- independent verification passes;
- state is updated when authorized;
- no approval gate is bypassed.

---

## 16. First-session bootstrap (completed)

The initial L1 scaffold run produced `LOOP_SETUP_READINESS_REPORT.md`. The next session should:

1. Run `loop doctor` and `loop sync` to confirm health.
2. Fill in the unresolved `production branch` field above.
3. Add a `gate.yaml` file.
4. Add a `permissions` block to `.claude/settings.json`.
5. Run three L1 report-only triage sessions before enabling L2.

---

## 17. Project-specific additions

```text
- This repo has no application source code. L2 work is bounded to:
    .claude-plugin/marketplace.json (plugin registry edits)
    plugins/<name>/ (plugin source)
    loop files (LOOP.md, STATE.md, etc.)
    .claude/settings.json (permissions and config)

- JSON changes to marketplace.json must be validated before commit.

- Plugin source additions should include a README.md and at least one skill.

- The production branch is unresolved. Do not merge, release, or push to a
  branch named as production until the owner confirms which branch that is.
```
