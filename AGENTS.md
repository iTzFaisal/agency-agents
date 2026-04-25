# AGENTS.md

Dual-platform agent definition repository. Contains AI agent personality/prompt files for **Claude** (`.claude/agents/`) and **OpenCode** (`.opencode/agents/`).

## Repository structure

- `.claude/agents/` — 186 agent markdown files for Claude Desktop/IDE
- `.opencode/agents/` — 186 agent markdown files for OpenCode
- **No build, test, or lint pipeline.** This is a content-only repo.

## Critical conventions

### The two platforms are NOT in sync

- Agent sets differ: some agents exist only in one platform, not both.
- File naming conventions differ:
  - **Claude**: often uses category prefixes (`academic-`, `engineering-`, `marketing-`, `specialized-`, `testing-`, `project-management-`, `support-`, `sales-`, `product-`, `finance-`, `paid-media-`)
  - **OpenCode**: mostly flat names without prefixes
- **There is no automated sync.** When adding or updating an agent, decide whether it belongs in one or both platforms and follow each directory's naming convention.

### Frontmatter schemas differ

**Claude** (`---` block):

```yaml
name: Anthropologist
description: Expert in cultural systems...
color: "#D97706"
emoji: 🌍
vibe: No culture is random...
```

**OpenCode** (`---` block):

```yaml
name: Accessibility Auditor
description: Expert accessibility specialist...
mode: subagent
color: "#6B7280"
```

- Claude uses `emoji` and `vibe`; OpenCode uses `mode`.
- Do not mix fields across platforms.

### OpenCode npm state is intentionally untracked

- `.opencode/package.json` and `.opencode/package-lock.json` are listed in `.opencode/.gitignore`.
- The `.opencode/node_modules/` directory is also ignored.
- Do not commit these files. The `package.json` exists only for local `@opencode-ai/plugin` dependency resolution.

## Workflow guidance

- **No CI, tests, or pre-commit hooks.** Changes go straight to review.
- When creating a new agent, mirror the frontmatter and heading structure of existing agents in the target platform.
- When editing an agent that exists in both platforms, consider whether the change should apply to both or is platform-specific.
