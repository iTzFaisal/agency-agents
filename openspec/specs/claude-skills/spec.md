## Requirements

### Requirement: Skill directories use category-prefixed names

The system SHALL create skill directories using category-prefixed kebab-case names matching the Claude naming convention. Each directory name SHALL follow the pattern `^[a-z0-9]+(-[a-z0-9]+)*$` and SHALL NOT exceed 64 characters.

#### Scenario: Claude agent keeps its prefix
- **WHEN** a Claude agent file exists at `.claude/agents/academic-anthropologist.md`
- **THEN** a skill directory SHALL be created at `.claude/skills/academic-anthropologist/SKILL.md`

#### Scenario: OpenCode agent renamed to Claude convention
- **WHEN** an OpenCode agent `anthropologist` maps to Claude's `academic-anthropologist`
- **THEN** a skill directory SHALL be created at `.agents/skills/academic-anthropologist/SKILL.md`

### Requirement: Skill directory names are consistent across platforms

The same skill SHALL use identical directory names in both `.claude/skills/` and `.agents/skills/`.

#### Scenario: Same skill, two platforms, one name
- **WHEN** both `.claude/agents/academic-anthropologist.md` and `.opencode/agents/anthropologist.md` exist for the same agent
- **THEN** both SHALL produce `academic-anthropologist/SKILL.md` in their respective skill directories

### Requirement: Skill frontmatter contains required metadata fields

Each SKILL.md SHALL include `name` (the category-prefixed directory name), `description` (from the agent's original description), `license` (set to `MIT`), `compatibility`, and `metadata`.

#### Scenario: Frontmatter uses directory name
- **WHEN** a skill is created at `academic-anthropologist/SKILL.md`
- **THEN** the frontmatter `name` field SHALL be `academic-anthropologist`

#### Scenario: Description preserved from agent
- **WHEN** a Claude agent has description "Expert in cultural systems..."
- **THEN** the skill frontmatter `description` SHALL be "Expert in cultural systems..."

### Requirement: Agent body content preserved verbatim

The Markdown body content SHALL be copied unchanged into the skill file, preserving the original display name and all personality instructions.

#### Scenario: Body content matches original
- **WHEN** a skill file is created from an agent file
- **THEN** the body content SHALL be byte-for-byte identical to the agent's body content

### Requirement: Old agent files deleted after migration

After skill files are verified, the corresponding agent files in `.claude/agents/` SHALL be deleted.

#### Scenario: Agent file removed
- **WHEN** `.claude/skills/academic-anthropologist/SKILL.md` exists and matches source
- **THEN** `.claude/agents/academic-anthropologist.md` SHALL be deleted

### Requirement: AGENTS.md updated to reflect unified structure

The `AGENTS.md` file SHALL document the unified category-prefixed naming convention and the two skill directories.

#### Scenario: AGENTS.md references skills
- **WHEN** migration is complete
- **THEN** `AGENTS.md` SHALL reference `.claude/skills/` and `.agents/skills/` with unified category-prefixed names
