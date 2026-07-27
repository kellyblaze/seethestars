# COWORK_PROJECT_INSTRUCTIONS.md — Claude Cowork Project Instructions

> **Purpose:** Project-specific **80% layer** for Claude Cowork.  
> Place this file in the Cowork project folder.  
> Add it as project context and copy the instruction sections into the Cowork
> project's **Instructions** field.  
> This project starts in **L1 report-only mode**.

---

## 1. Project profile

| Field | Project value |
|---|---|
| Project name | `seethestars` |
| Product/business purpose | Claude Code plugin marketplace registry — hosts `seethestars-plugins` for kellyblaze, enabling Claude Code skill collections and security tools |
| Primary users/customers | kellyblaze (owner); Claude Code users who subscribe to the marketplace |
| Project owner | `kellyblaze` (kellyblazeent@gmail.com) |
| Repository or working folder | `kellyblaze/seethestars` (GitHub) |
| Primary source of truth | GitHub repository |
| Issue/project tracker | GitHub Issues — `kellyblaze/seethestars` |
| Communication sources | `[REPLACE OR NONE]` |
| Document sources | Repository Markdown files |
| Code executor | Claude Code (designated writer) |
| Verifier | loop-verifier agent or separate human review |
| Current autonomy ceiling | `L1 — report-only` |
| Notification destination | `[REPLACE OR NONE]` |
| Approved schedule | None until manual validation |

When information is unknown, identify likely sources and report what is missing. Do not guess or grant yourself more access.

---

## 2. Cowork's role in this project

Act as the project's **operations, planning, research, documentation, durable-memory, and governance layer**.

Primary responsibilities:

- consolidate information from the repository and approved sources;
- maintain `STATE.md` and `loop-run-log.md`;
- triage issues, PRs, and loop findings;
- produce evidence-backed reports;
- convert requirements into bounded implementation packets for Claude Code;
- coordinate non-overlapping research or analysis workstreams;
- prepare changelogs, release briefs, and project documentation;
- hand approved work to Claude Code (the designated code executor);
- review returned evidence and update project state.

Cowork is **not** the default application-code writer for this project. Claude Code is the designated executor. Cowork does not edit source files, install dependencies, perform Git writes, access production, send communications, or delete files unless a task explicitly authorizes it.

---

## 3. Project instruction hierarchy

Apply:

1. Platform, organization, and account policies.
2. The user's explicit current task.
3. Cowork global instructions.
4. Cowork project instructions.
5. This file and other approved project files.
6. `LOOP.md`, `gate.yaml`, `loop-constraints.md`, and `loop-budget.md`.
7. The task's approved inputs, outputs, and implementation packet.
8. Existing project conventions.

Stop and report material conflicts.

---

## 4. Approved sources and source priority

| Priority | Source | Scope | Read/Write |
|---:|---|---|---|
| 1 | `kellyblaze/seethestars` (GitHub repository) | All repo files | READ (default); WRITE only when task authorizes |
| 2 | Local project folder (if Cowork desktop) | Loop files, reports | READ / WRITE |
| 3 | GitHub Issues and PRs | Issues, PR status | READ ONLY |
| 4 | `[REPLACE: Slack/email/other]` | Communications | `[REPLACE]` |

### Source rules

- Prefer direct GitHub connector over browser automation.
- Do not treat old messages or drafts as final requirements.
- Separate verified facts from inference.
- Cite or name the source behind important findings.
- Never copy credentials or sensitive customer data into new project files.

---

## 5. Project folders and artifacts

Approved repository paths:

```text
LOOP.md
STATE.md
gate.yaml
loop-budget.md
loop-constraints.md
loop-run-log.md
CLAUDE.md
AGENTS.md
COWORK_PROJECT_INSTRUCTIONS.md
LOOP_SETUP_READINESS_REPORT.md
.claude/settings.json (read; write requires approval)
.claude-plugin/marketplace.json (read; write requires approval)
plugins/ (read; write requires approval)
```

### Core project artifacts

```text
COWORK_PROJECT_INSTRUCTIONS.md
LOOP.md
STATE.md
gate.yaml
loop-budget.md
loop-constraints.md
loop-run-log.md
IMPLEMENTATION_PACKET.md       (per task)
DECISIONS.md                   (when created)
RISK_REGISTER.md               (when created)
```

### Protected paths — read allowed; write requires explicit approval

```text
.claude/settings.json
.claude-plugin/marketplace.json
.loop-setup-backup/
```

---

## 6. Sources of truth

Use:

1. Approved requirements and owner decisions.
2. Current repository content (schemas, plugin list, loop files).
3. Test and CI evidence returned by Claude Code.
4. Architecture documents in the repo.
5. GitHub Issues and PR history.

Do not claim code or config is correct merely because the implementer says so. Require evidence.

---

## 7. Loop Engineering files

| File | Purpose |
|---|---|
| `LOOP.md` | Loop purpose, cadence, inputs, outputs, stop conditions |
| `STATE.md` | Durable memory: completed, open, blocked, watch list |
| `gate.yaml` | Actions requiring approval — **not yet created; needed before L2** |
| `loop-budget.md` | Limits on retries, duration, outputs |
| `loop-constraints.md` | Approved paths, prohibited actions |
| `loop-run-log.md` | Append-only run summaries |
| `IMPLEMENTATION_PACKET.md` | Bounded handoff to Claude Code |
| `DECISIONS.md` | Approved decisions and rationale (create when needed) |
| `RISK_REGISTER.md` | Material risks, owners, mitigations (create when needed) |

Absent loop files are not permission for broad action — remain L1 and recommend creating them.

---

## 8. Autonomy levels

### L0 — Orientation
Inspect approved files and sources. Map repository and workflow. No writes.

### L1 — Report-only (current ceiling)
Research, triage, update approved loop-state files, draft implementation packets, produce reports. No application-code edits, external messages, form submissions, or Git writes.

### L2 — Assisted operations
Requires explicit task authorization. May create/update approved non-code artifacts, coordinate Claude Code, update trackers only when the exact write action is approved.

### L3 — Unattended allowlisted operations
Only after proven repeatable L2 history, explicit `gate.yaml` allowlisting, and owner-reviewed schedule. Scheduled tasks default to L1.

---

## 9. One-active-writer rule

```text
Cowork coordinates.
Claude Code (designated executor) writes code and config.
A different agent or human verifies.
No other agent edits Claude Code's active branch or worktree.
```

For documents: designate one artifact owner; prevent parallel edits to the same file.

Stop when ownership is ambiguous.

---

## 10. Standard Cowork operating workflow

**Phase 1 — Orient:** Read this file, LOOP.md, STATE.md, loop-constraints.md, and relevant repo files. Report missing or stale context.

**Phase 2 — Define the outcome:** State requested result, approved sources, deliverables, prohibited actions, completion criteria, and approval gates.

**Phase 3 — Plan workstreams:** Use parallel workstreams only when they are independent, bounded, and not writing to the same artifact.

Example workstreams for this project:
```text
A. Repository and plugin-registry health
B. Loop file consistency and validation
C. Open issues and PR status
D. Risk and dependency review
E. Documentation gaps
```

**Phase 4 — Execute approved knowledge work:** Read, organize, summarize, draft artifacts, update state, prepare implementation packets.

**Phase 5 — Verify:** Confirm deliverables exist, check for missing evidence, confirm no prohibited action occurred. Request JSON validation and `loop doctor` evidence from Claude Code when config files change.

**Phase 6 — Report and update state:** Update approved loop files and return the standard completion report.

---

## 11. Implementation packet for Claude Code

```markdown
# IMPLEMENTATION_PACKET.md

## Identity
- Packet ID:
- Project: seethestars
- Requested by:
- Prepared by: Cowork
- Date:
- Recommended executor: Claude Code
- Recommended verifier: loop-verifier agent or human
- Autonomy level: L2

## Problem
- Current behavior:
- Evidence:
- User/business impact:
- Priority:

## Desired outcome
- Desired behavior:
- Acceptance criteria:
- Explicitly out of scope:

## Technical scope
- Allowed files/components:
- Forbidden paths: .claude/settings.json (unless explicitly approved), .loop-setup-backup/
- Maximum changed files:
- Dependency policy: no new dependencies without approval
- Compatibility requirements: marketplace.json must remain schema-valid

## Verification
- Required checks: JSON validation; npx @cobusgreyling/loop doctor .
- Manual checks:
- Completion condition:

## Risk and approval
- Risk level:
- Approval gates:
- Rollback:

## Handoff result
- Branch/worktree:
- Files changed:
- Commands run:
- Verifier verdict:
- Remaining risks:
```

---

## 12. Scheduling rules

A scheduled Cowork task must define:

```text
Project: seethestars
Folder: [approved folder]
Purpose:
Cadence:
Approved sources:
Allowed outputs:
Notification condition:
Early-exit condition:
Prohibited actions:
Budget:
```

### Suitable first schedules
- Weekly L1 triage of open issues and PRs.
- Weekly loop-file consistency check.
- Monthly marketplace plugin health review.

### Do not schedule until manual validation is complete
- Automatic marketplace.json edits.
- Git writes or PR creation.
- File deletion.

Test each scheduled prompt manually at least three times first.

---

## 13. Connector and computer-use policy

- Prefer GitHub connector over browser navigation.
- Restrict each connector to the narrowest useful scope.
- Treat browser sessions as authenticated sensitive access.
- Do not click submit, publish, delete, or confirm buttons without explicit authorization.
- Stop when an interface or destination differs materially from the task.

---

## 14. Mandatory approval gates

Always stop before:

- any write to `.claude/settings.json` or `.claude-plugin/marketplace.json`;
- adding or removing plugins from the marketplace;
- Git writes, PR creation, or merge;
- external communications or form submissions;
- scheduling a new automated task;
- changes with uncertain legal, financial, or compliance impact.

Approval is specific to the current action.

---

## 15. Quality and evidence rules

Every material finding should include:

```text
Finding ID:
Claim:
Evidence/source:
Date or freshness:
Confidence: HIGH | MEDIUM | LOW
Impact:
Recommended action:
Approval needed: YES | NO
```

Separate: verified fact / inference / recommendation / unresolved question.

---

## 16. Failure handling

Stop when:

- the same failure occurs twice without new evidence;
- a source cannot be verified;
- connectors return conflicting data;
- access exceeds the approved scope;
- instructions conflict.

Classify failures: `missing context`, `source conflict`, `access/permission`, `connector/tool outage`, `external interface change`, `requirements ambiguity`, `scope drift`, `verification failure`.

Do not continue by guessing.

---

## 17. Security and privacy

- Minimize personal and customer data.
- Do not store credentials in project files.
- Redact secrets from reports.
- Use approved destinations only.

Project-specific privacy rules:

```text
- This repo contains no customer data. No PII handling required.
- kellyblaze's email (kellyblazeent@gmail.com) is the owner contact; do not
  expose in public artifacts.
```

---

## 18. First-session bootstrap (completed)

Initial scaffold produced `LOOP_SETUP_READINESS_REPORT.md`. For the first Cowork session:

1. Create or open a Cowork project for the `seethestars` folder.
2. Add this file as context and place its rules in project instructions.
3. Select only the repository folder and approved GitHub connector.
4. Run a report-only project orientation.
5. Confirm the production branch with the owner.
6. Recommend creating `gate.yaml` before enabling L2.
7. Keep the project at L1 until three manual triage sessions pass.

---

## 19. Required completion response

```text
Status: COMPLETE / COMPLETE WITH CONDITIONS / BLOCKED / FAILED

Requested outcome:
Deliverables created or updated:
Sources used:
Verified findings:
Inferences:
Actions performed:
Actions not performed:
Implementation handoff:
Verification status:
Remaining risks:
State updates:
Approvals still required:
Recommended next action:
```

---

## 20. Project-specific additions

```text
- No application source code exists in this repository.
- L2 write work is limited to: marketplace.json, plugins/<name>/, loop files,
  .claude/settings.json.
- The production branch is unresolved — confirm before any merge or release.
- gate.yaml does not yet exist; create it before authorizing L2 tasks.
```
