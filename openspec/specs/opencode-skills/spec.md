## Requirements

### Requirement: Skill directories use category-prefixed names

The system SHALL create skill directories under `.agents/skills/` using category-prefixed kebab-case names. Overlapping agents (same role in both platforms) SHALL use the Claude naming convention. OpenCode-only agents SHALL be assigned a category prefix based on their role.

#### Scenario: Overlapping agent uses Claude name
- **WHEN** an OpenCode agent `anthropologist.md` maps to Claude's `academic-anthropologist`
- **THEN** a skill directory SHALL be created at `.agents/skills/academic-anthropologist/SKILL.md`

#### Scenario: OpenCode-only agent gets assigned prefix
- **WHEN** an OpenCode agent `senior-project-manager.md` has no Claude counterpart and its role is project management
- **THEN** a skill directory SHALL be created at `.agents/skills/project-management-senior-project-manager/SKILL.md` or the most appropriate category-prefixed name

### Requirement: Names are consistent with `.claude/skills/`

Every skill in `.agents/skills/` that has a corresponding Claude skill SHALL use the identical directory name. The two directories SHALL have the same set of skill names.

#### Scenario: Same skill name in both directories
- **WHEN** both directories contain the Anthropologist skill
- **THEN** both SHALL use the directory name `academic-anthropologist`

### Requirement: Skill frontmatter contains required metadata fields

Each SKILL.md SHALL include `name` (the category-prefixed directory name), `description` (from the agent's original description), `license` (set to `MIT`), `compatibility` (set to `"Requires a compatible coding agent"`), and `metadata` (with `author` and `version`).

#### Scenario: Frontmatter uses directory name
- **WHEN** a skill is created at `academic-anthropologist/SKILL.md`
- **THEN** the frontmatter `name` field SHALL be `academic-anthropologist`

### Requirement: Agent body content preserved verbatim

The Markdown body content SHALL be copied unchanged into the skill file.

#### Scenario: Body content matches original
- **WHEN** a skill file is created from an agent file
- **THEN** the body content SHALL be byte-for-byte identical to the agent's body content

### Requirement: Existing OpenCode skills preserved

The existing 4 skill directories in `.opencode/skills/` (openspec-propose, openspec-apply-change, openspec-archive-change, openspec-explore) SHALL remain untouched.

#### Scenario: Existing openspec skills untouched
- **WHEN** migration runs
- **THEN** directories `.opencode/skills/openspec-propose/`, `.opencode/skills/openspec-apply-change/`, `.opencode/skills/openspec-archive-change/`, and `.opencode/skills/openspec-explore/` SHALL have no changes

### Requirement: Old agent files deleted after migration

After skill files are verified, the corresponding agent files in `.opencode/agents/` SHALL be deleted.

#### Scenario: Agent file removed
- **WHEN** `.agents/skills/academic-anthropologist/SKILL.md` exists and matches source
- **THEN** `.opencode/agents/anthropologist.md` SHALL be deleted

### Requirement: AGENTS.md updated to reflect unified structure

The `AGENTS.md` file SHALL document the unified category-prefixed naming convention and the two skill directories.

#### Scenario: AGENTS.md references skills
- **WHEN** migration is complete
- **THEN** `AGENTS.md` SHALL reference `.agents/skills/` with unified category-prefixed names
