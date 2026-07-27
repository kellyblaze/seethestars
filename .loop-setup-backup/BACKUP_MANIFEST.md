# Loop Engineering Setup — Backup Manifest

**Date:** 2026-07-27
**Branch at backup time:** claude/upbeat-cori-swv4jr
**Setup branch:** chore/loop-engineering-setup

## Files Backed Up

| Original Path | Backup Path | SHA-256 | Existed Before Loop Setup | Reason |
|---|---|---|---|---|
| `.claude/settings.json` | `.loop-setup-backup/.claude/settings.json` | `85d780a6ce777ba201d2739b9369e126aa60e325055376ca74ba87188f028e78` | Yes | Plugin marketplace + permissions config |
| `.claude-plugin/marketplace.json` | `.loop-setup-backup/.claude-plugin/marketplace.json` | `c332070e82d94dfad973d53c4d8e438ecf0044a536865d03644100c582717ee2` | Yes | 42-plugin marketplace registry |

## Files NOT Backed Up

| File | Reason |
|---|---|
| `plugins/` directory | Application plugin code — excluded per policy |
| `.git/` | Git internal data — not applicable |

## Notes

- No `AGENTS.md`, `CLAUDE.md`, `LOOP.md`, `STATE.md`, `gate.yaml`, or other loop instruction files existed prior to setup.
- Originals remain in place; this backup is additive only.
