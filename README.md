# seethestars

A Claude Code plugin marketplace registry that hosts the `seethestars-plugins` collection. It enables Claude Code users to install curated skill collections and security tools directly into their Claude Code environment.

## What this repository is

`seethestars` is a configuration-only registry. It contains no application source code. It defines a marketplace of 42 plugins spanning development productivity, scientific research, and security tooling. The marketplace is registered as `seethestars-plugins` and is sourced from `kellyblaze/seethestars` on GitHub.

## How to add this marketplace to Claude Code

Register the marketplace by adding the following block to your `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "seethestars-plugins": {
      "source": {
        "source": "github",
        "repo": "kellyblaze/seethestars"
      }
    }
  }
}
```

## How to install a plugin

Once the marketplace is registered, install any plugin using the `@seethestars-plugins` suffix. For example:

```
/plugin install frontend-design@seethestars-plugins
/plugin install superpowers@seethestars-plugins
```

## Currently enabled plugins

The following four plugins are enabled in this repository's own `.claude/settings.json`:

| Plugin | Category | Description |
|---|---|---|
| `frontend-design` | development | Create distinctive, production-grade frontend interfaces with high design quality. Generates creative, polished code that avoids generic AI aesthetics. Authors: Prithvi Rajasekaran & Alexander Bricken. |
| `superpowers` | productivity | Core skills library for Claude Code: TDD, debugging, collaboration patterns, and proven techniques across the SDLC. Author: Jesse Vincent. |
| `scientific-skills` | science | Scientific skills for Claude: research, science, engineering, analysis, finance, and writing capabilities across 140+ domains. Author: K-Dense AI. |
| `fullstack-dev-skills` | development | Comprehensive skill pack with 66 specialized skills for full-stack developers: 12 language experts, 10 backend frameworks, 6 frontend/mobile, plus infrastructure, DevOps, security, and testing. Author: Jeffallan. |

## Trail of Bits security plugin collection

The marketplace includes a large collection of security-focused plugins authored and maintained by Trail of Bits (`https://github.com/trailofbits`). These plugins are sourced from the `trailofbits/skills` repository on GitHub. The collection covers:

- Code auditing: `audit-context-building`, `differential-review`, `c-review`, `variant-analysis`, `static-analysis`
- Smart contract security: `building-secure-contracts`, `entry-point-analyzer`, `spec-to-code-compliance`, `dimensional-analysis`
- Testing: `property-based-testing`, `mutation-testing`, `testing-handbook-skills`
- Tooling: `semgrep-rule-creator`, `semgrep-rule-variant-creator`, `static-analysis`, `gh-cli`
- Detection and analysis: `yara-authoring`, `firebase-apk-scanner`, `insecure-defaults`, `sharp-edges`, `constant-time-analysis`, `zeroize-audit`, `burpsuite-project-parser`
- Infrastructure and DevOps: `devcontainer-setup`, `debug-buttercup`, `seatbelt-sandboxer`, `supply-chain-risk-auditor`, `git-cleanup`, `modern-python`
- Workflow and skills development: `workflow-skill-design`, `skill-improver`, `fp-check`, `second-opinion`, `agentic-actions-auditor`
- Other: `ask-questions-if-underspecified`, `trailmark`, `dwarf-expert`, `culture-index`, `let-fate-decide`

All Trail of Bits plugins are in the `security` category in the marketplace registry.

## Repository structure

```
.claude-plugin/
  marketplace.json        42-plugin marketplace registry
.claude/
  settings.json           Marketplace registration and enabled plugins
plugins/
  frontend-design/        Locally installed plugin source
```

## Contributing

This is a private registry owned by kellyblaze. Changes to `marketplace.json` or `.claude/settings.json` require explicit owner approval before committing or pushing.
