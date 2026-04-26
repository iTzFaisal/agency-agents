# AGENTS.md

Dual-platform skill definition repository. Contains AI agent personality/prompt files as **skills** (SKILL.md) for **Claude Code** (`.claude/skills/`) and **compatible coding agents** (`.agents/skills/`).

## Repository structure

- `.claude/skills/` — 184 skill directories for Claude Code, each containing a `SKILL.md`
- `.agents/skills/` — 184 skill directories for compatible coding agents (OpenCode, Codex, Cline, Cursor, Gemini CLI, Copilot, etc.), each containing a `SKILL.md`
- `.opencode/skills/` — 4 OpenCode-specific skills (openspec-propose, openspec-apply-change, openspec-archive-change, openspec-explore)
- **No build, test, or lint pipeline.** This is a content-only repo.

## Skill directory structure

Each skill lives in a named directory containing a single `SKILL.md` file:

```
<category-prefixed-name>/
  SKILL.md
```

Example:

```
academic-anthropologist/
  SKILL.md
```

## Naming convention

All skills use **category-prefixed kebab-case names** (Claude naming conventions adopted for all platforms):

| Category      | Prefix                | Examples                                                      |
| ------------- | --------------------- | ------------------------------------------------------------- |
| Academic      | `academic-`           | `academic-anthropologist`, `academic-geographer`              |
| Design        | `design-`             | `design-brand-guardian`, `design-ui-designer`                 |
| Engineering   | `engineering-`        | `engineering-code-reviewer`, `engineering-frontend-developer` |
| Finance       | `finance-`            | `finance-bookkeeper-controller`, `finance-tax-strategist`     |
| Marketing     | `marketing-`          | `marketing-seo-specialist`, `marketing-tiktok-strategist`     |
| Paid Media    | `paid-media-`         | `paid-media-auditor`, `paid-media-ppc-strategist`             |
| Product       | `product-`            | `product-manager`, `product-behavioral-nudge-engine`          |
| Project Mgmt  | `project-management-` | `project-management-project-shepherd`                         |
| Sales         | `sales-`              | `sales-coach`, `sales-engineer`                               |
| Specialized   | `specialized-`        | `specialized-chief-of-staff`, `specialized-mcp-builder`       |
| Support       | `support-`            | `support-analytics-reporter`, `support-support-responder`     |
| Testing       | `testing-`            | `testing-accessibility-auditor`, `testing-api-tester`         |
| Uncategorized | (none)                | `game-audio-engineer`, `narrative-designer`                   |

- Directory names follow `^[a-z0-9]+(-[a-z0-9]+)*$` and are ≤64 characters
- The name in the SKILL.md frontmatter must match the directory name

## Skill frontmatter schema

Each `SKILL.md` uses this frontmatter structure:

```yaml
---
name: engineering-code-reviewer
description: Expert code reviewer who provides constructive, actionable feedback...
license: MIT
compatibility: "Requires Claude Code"
metadata:
  author: agency-agents
  version: "1.0"
---
```

### Fields

| Field              | Description                                                                                                  |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| `name`             | Category-prefixed directory name                                                                             |
| `description`      | Agent/skill description (preserved from original agent)                                                      |
| `license`          | Always `MIT`                                                                                                 |
| `compatibility`    | `"Requires Claude Code"` for `.claude/skills/`, `"Requires a compatible coding agent"` for `.agents/skills/` |
| `metadata.author`  | Always `agency-agents`                                                                                       |
| `metadata.version` | Always `"1.0"`                                                                                               |

### Dropped fields

The following original agent fields are **not preserved** in the skill format (skill spec ignores unknown fields):

- `color` — not supported by skill spec
- `emoji` — Claude-only cosmetic field
- `vibe` — Claude-only cosmetic field
- `mode` — OpenCode-specific field

The agent's original display name is preserved in the body content (e.g., `# Anthropologist Agent Personality`).

## Cross-platform consistency

- The same 184 skills exist in both `.claude/skills/` and `.agents/skills/` with identical directory names
- `.claude/skills/` uses `compatibility: "Requires Claude Code"`
- `.agents/skills/` uses `compatibility: "Requires a compatible coding agent"`
- Content (personality/prompt body) is identical across platforms for the same skill

## OpenCode npm state is intentionally untracked

- `.opencode/package.json` and `.opencode/package-lock.json` are listed in `.opencode/.gitignore`.
- The `.opencode/node_modules/` directory is also ignored.
- Do not commit these files. The `package.json` exists only for local `@opencode-ai/plugin` dependency resolution.

## Workflow guidance

- **No CI, tests, or pre-commit hooks.** Changes go straight to review.
- When creating a new skill, follow the directory and frontmatter structure above.
- Skills must be placed in both `.claude/skills/` and `.agents/skills/` with the same canonical name.
- When editing a skill that exists in both platforms, apply the change to both unless it's platform-specific.
- Use the unified category-prefixed naming convention for all new skills.
