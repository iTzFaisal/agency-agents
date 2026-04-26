## Context

This is a content-only repository containing ~184 AI agent personality definitions across two platforms: Claude (`.claude/agents/`) and OpenCode (`.opencode/agents/`). Each agent is a single Markdown file with YAML frontmatter and instructional body content. The industry has adopted a skill system (`SKILL.md` in named directories) with `.agents/skills/` as the cross-agent convention. Claude Code natively supports `.claude/skills/`. Currently `.opencode/skills/` already contains 4 openspec-related skills.

**Constraints:**
- No CI, tests, or pre-commit hooks
- The two platforms currently use different naming conventions (Claude: category-prefixed, OpenCode: flat names)
- Agent content (prompt bodies) must be preserved verbatim
- Existing 4 skills in `.opencode/skills/` must not be affected
- Skill spec only recognizes `name`, `description`, `license`, `compatibility`, `metadata`; unknown frontmatter fields are silently ignored
- Skill `name` must be lowercase alphanumeric with single hyphens, match directory name, max 64 chars

## Goals / Non-Goals

**Goals:**
- Unify all skill names to Claude's category-prefixed convention across both `.claude/skills/` and `.agents/skills/`
- Convert all agents to `SKILL.md` format with standardized frontmatter
- Map overlapping agents (same role, different names per platform) to a single canonical name
- Assign category prefixes to OpenCode-only agents
- Preserve all agent personality/prompt content unchanged
- Update `AGENTS.md` to document the new structure

**Non-Goals:**
- Changing agent content, personalities, or prompt wording
- Adding CI, tests, or build pipelines
- Adding new agents or removing existing ones
- Keeping the old flat naming convention for OpenCode

## Decisions

### 1. Unified naming: Claude convention wins

All skills use Claude's category-prefixed kebab-case convention. Examples:

| Category | Prefix | Example |
|----------|--------|---------|
| Academic | `academic-` | `academic-anthropologist`, `academic-geographer` |
| Design | `design-` | `design-brand-guardian`, `design-ui-designer` |
| Engineering | `engineering-` | `engineering-code-reviewer`, `engineering-frontend-developer` |
| Finance | `finance-` | `finance-bookkeeper-controller`, `finance-tax-strategist` |
| Marketing | `marketing-` | `marketing-seo-specialist`, `marketing-tiktok-strategist` |
| Paid Media | `paid-media-` | `paid-media-auditor`, `paid-media-ppc-strategist` |
| Product | `product-` | `product-manager`, `product-behavioral-nudge-engine` |
| Project Mgmt | `project-management-` | `project-management-project-shepherd` |
| Sales | `sales-` | `sales-coach`, `sales-engineer` |
| Specialized | `specialized-` | `specialized-chief-of-staff`, `specialized-mcp-builder` |
| Support | `support-` | `support-analytics-reporter`, `support-support-responder` |
| Testing | `testing-` | `testing-accessibility-auditor`, `testing-api-tester` |
| Uncategorized | none | `game-audio-engineer`, `narrative-designer`, etc. |

**Rationale:** Category prefixes self-document what a skill does before reading the file. All names validate under the skill spec regex (`^[a-z0-9]+(-[a-z0-9]+)*$`, ≤64 chars).

### 2. Mapping overlapping agents

Where Claude and OpenCode have the same agent under different names, the Claude name is used for both:

| OpenCode Name | Claude Name | Canonical Skill Name |
|---------------|-------------|---------------------|
| `anthropologist` | `academic-anthropologist` | `academic-anthropologist` |
| `code-reviewer` | `engineering-code-reviewer` | `engineering-code-reviewer` |
| `frontend-developer` | `engineering-frontend-developer` | `engineering-frontend-developer` |
| `ux-architect` | `design-ux-architect` | `design-ux-architect` |
| `product-manager` | `product-manager` | `product-manager` |
| `seo-specialist` | `marketing-seo-specialist` | `marketing-seo-specialist` |

The original internal display name (e.g. "Anthropologist") remains in the agent body content — only the directory/file name changes.

### 3. OpenCode-only agents: assign category

OpenCode agents that don't exist in Claude get a category prefix based on their role. Non-obvious mappings determined by content analysis during migration (task 1.1).

### 4. Frontmatter migration

| Agent field | Skill field | Notes |
|-------------|-------------|-------|
| `name` (display) | `name` | Replaced with category-prefixed directory name; original display name preserved in body content |
| `description` | `description` | Preserved as-is |
| `color` | dropped | Skill spec ignores unknown fields |
| `emoji` / `vibe` / `mode` | dropped | Skill spec ignores unknown fields |

Standard skill fields added: `license: MIT`, `compatibility: "Requires Claude Code"` (Claude) or `"Requires a compatible coding agent"` (`.agents/`), `metadata: { author: "agency-agents", version: "1.0" }`.

### 5. Content preservation

The entire Markdown body below the frontmatter `---` block is preserved verbatim. The agent's personality definition becomes the skill's instruction content.

### 6. Existing skills protection

All 4 existing skill directories in `.opencode/skills/` (openspec-propose, openspec-apply-change, openspec-archive-change, openspec-explore) are excluded from the migration.

## Risks / Trade-offs

- **[Risk] Agent metadata loss**: `color`, `emoji`, `vibe`, `mode` fields dropped → **Mitigation**: Cosmetic/platform-specific; body content (the personality prompt) is fully preserved.
- **[Risk] Name changes break references**: OpenCode agents renamed from flat to category-prefixed → **Mitigation**: This is a content-only repo with no CI; consumers reference skills by directory name, not old agent filenames.
- **[Risk] Large diff**: ~368 files created/deleted + many renames → **Mitigation**: Batch commits by category.
- **[Risk] Category assignment for OpenCode-only agents may be subjective** → **Mitigation**: Use agent's own description/role to determine the best-fit prefix during migration.

## Open Questions

- None remaining.
