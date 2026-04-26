## Why

The repository currently defines AI agent personalities as flat Markdown files in `.claude/agents/` and `.opencode/agents/`. Coding agents have standardized on a skill system (`SKILL.md` in named directories) with the `.agents/skills/` path emerging as the cross-agent convention (supported by OpenCode, Codex, Cline, Cursor, Gemini CLI, Copilot, and others). Migrating to skills with unified category-prefixed names provides richer metadata, directory-based organization, and broad compatibility across the agent ecosystem.

## What Changes

- Consolidate naming: adopt Claude's category-prefixed convention (`academic-anthropologist`, `engineering-code-reviewer`) for all skills across both platforms
- Convert all agent `.md` files into skill directories with unified names under `.claude/skills/<name>/SKILL.md` and `.agents/skills/<name>/SKILL.md`
- Map overlapping agents (same role, different names across platforms) to a single canonical name
- Assign category prefixes to OpenCode-only agents based on their role
- Standardize frontmatter to the skill schema: `name`, `description`, `license`, `compatibility`, `metadata`
- Preserve agent personality/prompt content as the skill instruction body
- Remove old agent `.md` files after migration is verified
- **BREAKING**: Update `AGENTS.md` documentation to reflect the new skill-based structure

## Capabilities

### New Capabilities
- `claude-skills`: Claude Code skill directory at `.claude/skills/` using category-prefixed names
- `agents-skills`: Cross-agent skill directory at `.agents/skills/` using the same unified category-prefixed names

### Modified Capabilities
<!-- None - no existing specs to modify -->

## Impact

- All files in `.claude/agents/` and `.opencode/agents/` → restructured into `.claude/skills/<name>/SKILL.md` and `.agents/skills/<name>/SKILL.md` with unified category-prefixed names
- OpenCode flat names (e.g. `anthropologist`) renamed to Claude convention (e.g. `academic-anthropologist`)
- OpenCode-only agents assigned category prefixes (e.g. `engineering-`, `marketing-`, `sales-`)
- Existing 4 skills in `.opencode/skills/` (openspec-propose, openspec-apply-change, openspec-archive-change, openspec-explore) remain untouched
- `AGENTS.md` updated to document the new unified structure
