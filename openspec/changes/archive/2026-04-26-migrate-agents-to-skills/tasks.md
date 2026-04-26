## 1. Setup and analysis

- [x] 1.1 Build a cross-reference map: for each Claude agent, identify its OpenCode counterpart (same role, different name). Mark OpenCode-only agents (no Claude counterpart) for category prefix assignment.
- [x] 1.2 Read one sample agent from each platform to confirm frontmatter structure (Claude: name/description/color/emoji/vibe; OpenCode: name/description/mode/color)
- [x] 1.3 Create `.claude/skills/` parent directory if it does not exist
- [x] 1.4 Create `.agents/skills/` parent directory if it does not exist
- [x] 1.5 Verify existing 4 skill directories in `.opencode/skills/` are intact
- [x] 1.6 Generate the complete canonical name list (category-prefixed) for all ~184 unique agents

## 2. Migrate agents to `.claude/skills/`

- [x] 2.1 For each Claude agent file, create directory `.claude/skills/<canonical-name>/` using its existing category-prefixed filename
- [x] 2.2 Set frontmatter: `name` = canonical directory name, `description` = original agent description, `license` = `MIT`, `compatibility` = `"Requires Claude Code"`, `metadata` = `{ author: "agency-agents", version: "1.0" }`
- [x] 2.3 Drop agent-specific fields: `color`, `emoji`, `vibe` (not supported by skill spec)
- [x] 2.4 Copy agent body content verbatim below the new frontmatter
- [x] 2.5 Write SKILL.md to each skill directory

## 3. Migrate agents to `.agents/skills/`

- [x] 3.1 For each OpenCode agent, determine canonical name: use Claude name for overlapping agents (e.g. `anthropologist` → `academic-anthropologist`); assign category prefix for OpenCode-only agents
- [x] 3.2 Create directory `.agents/skills/<canonical-name>/` for each agent
- [x] 3.3 Set frontmatter: `name` = canonical directory name, `description` = original agent description, `license` = `MIT`, `compatibility` = `"Requires a compatible coding agent"`, `metadata` = `{ author: "agency-agents", version: "1.0" }`
- [x] 3.4 Drop agent-specific fields: `mode`, `color` (not supported by skill spec)
- [x] 3.5 Copy agent body content verbatim below the new frontmatter
- [x] 3.6 Write SKILL.md to each skill directory

## 4. Cleanup old agent files

- [x] 4.1 Verify all `.claude/skills/` directories exist with non-empty SKILL.md
- [x] 4.2 Delete all agent `.md` files from `.claude/agents/`
- [x] 4.3 Verify all `.agents/skills/` directories exist with non-empty SKILL.md
- [x] 4.4 Delete all agent `.md` files from `.opencode/agents/`

## 5. Update documentation

- [x] 5.1 Update `AGENTS.md` to reference `.claude/skills/` and `.agents/skills/` instead of old agent directories
- [x] 5.2 Document the unified category-prefixed naming convention (Claude conventions adopted for all skills)
- [x] 5.3 Document the skill frontmatter schema (name, description, license, compatibility, metadata)
- [x] 5.4 Document the skill directory structure (`<name>/SKILL.md`)
- [x] 5.5 Note that agent-specific fields (`color`, `emoji`, `vibe`, `mode`) are not preserved in skill format

## 6. Verification

- [x] 6.1 Verify `.claude/skills/` and `.agents/skills/` have the same set of skill directory names
- [x] 6.2 Verify skill count matches expected total
- [x] 6.3 Spot-check 5 random skills per directory for frontmatter correctness and body content fidelity
- [x] 6.4 Verify all directory names match `^[a-z0-9]+(-[a-z0-9]+)*$` pattern and are ≤64 chars
- [x] 6.5 Verify existing 4 openspec skills in `.opencode/skills/` remain unchanged
- [x] 6.6 Run `openspec status --change "migrate-agents-to-skills"` to confirm all tasks checked
