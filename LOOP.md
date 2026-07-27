# Loop Configuration — seethestars (Daily Triage)

## Active Loops

| Pattern | Cadence | Status | Command |
|---------|---------|--------|---------|
| Daily Triage | 1d | L1 report-only | `/loop 1d Run $loop-triage` |

## State

Durable state is maintained in **STATE.md**. Read STATE.md before every run.
Update STATE.md with new findings; deduplicate against existing entries.
Append run summaries to loop-run-log.md — never overwrite it.

## Human Gates

All gates defined in gate.yaml. Summary of always-required approvals:
- git push, merge, PR creation, release, or tag
- edits to .claude/settings.json or .claude-plugin/marketplace.json
- adding or removing marketplace plugins
- dependency installation
- file deletion
- branch deletion

No auto-fix until L2 checklist complete (see gate.yaml l2_allowlist).

## Stop Conditions

- Same failure occurs twice without new evidence → escalate, do not retry.
- Budget limits in loop-budget.md are reached → pause and notify owner.
- `loop-pause-all` label or flag is active → exit immediately.
- Max repair cycles (2) reached → report blocker.

## Worktrees

- Use `isolation: worktree` when spawning implementer sub-agents (L2+).
- One worktree per fix attempt; discard after verifier REJECT.
- Branch pattern: `loop/<TASK-ID>-<short-description>`

## Connectors (MCP)

- MCP optional for L1 report-only loops.
- For L2+: GitHub MCP to read CI/issues; scope to read + comment only until trusted.

## Budget

- Max sub-agent spawns per run: 0 (L1) / 2 (L2)
- See loop-budget.md for full limits.
- Review STATE.md before each run.

## Rollback

- All changes are in Git. Roll back with `git revert` or restore from .loop-setup-backup/.
- Protected files (.claude/settings.json, .claude-plugin/marketplace.json) are backed up in .loop-setup-backup/.