# Skill: implementation-packet (seethestars)

Assemble a bounded implementation packet before any L2 task begins.

## When to invoke

Before any L2 edit to marketplace.json, plugin source, settings.json, or loop files. The packet is the scope boundary for the implementer and verifier.

## Steps

1. Read CLAUDE.md, gate.yaml, loop-constraints.md, and STATE.md.
2. Confirm the task does not involve a high-risk gate that needs human sign-off first.
3. Write TASK_SCOPE.md in the repo root using the template below.
4. Confirm the packet with the user before any edits begin.
5. Archive or delete TASK_SCOPE.md after the task is complete.

## TASK_SCOPE.md template

```markdown
# TASK_SCOPE.md

- Task ID: <TS-NNN>
- Date: <YYYY-MM-DD>
- Objective: <one sentence>
- Allowed files: <explicit list — no wildcards>
- Forbidden paths: .claude/settings.json (unless explicitly approved), .claude-plugin/marketplace.json (unless explicitly approved), .loop-setup-backup/, .env*
- Maximum changed files: <N>
- Out of scope: <explicit list>
- Acceptance criteria:
  - <criterion 1>
  - <criterion 2>
- Validation commands:
  - node -e "JSON.parse(...)" (if JSON changed)
  - npx @cobusgreyling/loop doctor . (if loop files changed)
- Maximum repair cycles: 2
- Approval gates: <list from gate.yaml>
- Rollback: git revert <commit> or restore from .loop-setup-backup/
- Branch/worktree: <branch>
- Designated implementer: implementer agent or Claude Code
- Designated verifier: verifier agent or loop-verifier agent
- Completion condition: <verifiable statement>
```

## Constraints

- Do not begin implementation until the packet is confirmed by the user.
- The verifier must differ from the implementer.
- If the allowed files list includes any protected path, require explicit human approval before writing the packet.
