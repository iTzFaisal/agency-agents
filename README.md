# Agency Agents

A curated collection of AI skill definitions for dual-platform use — **Claude Code** (`.claude/skills/`) and **compatible coding agents** (`.agents/skills/`).

Each skill is a self-contained `SKILL.md` file in a named directory that defines a specialist persona, enabling AI assistants to adopt domain-specific expertise, workflows, and communication styles on demand.

> **Original repository:** [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents)

---

## Overview

This repository contains **184 skill definitions** across two platforms, covering disciplines from software engineering and marketing to finance, legal, gaming, and academia. Skills are designed to function as modular, swappable experts that can be invoked contextually within AI-powered workflows.

### Supported Platforms

| Platform                | Directory           | Count      | Notes                                                       |
| ----------------------- | ------------------- | ---------- | ----------------------------------------------------------- |
| **Claude Code**         | `.claude/skills/`   | 184 skills | Compatibility: `"Requires Claude Code"`                     |
| **Compatible Agents**   | `.agents/skills/`   | 184 skills | Compatibility: `"Requires a compatible coding agent"`       |
| **OpenCode (built-in)** | `.opencode/skills/` | 4 skills   | openspec workflow skills (propose, apply, archive, explore) |

> All platform skills use unified category-prefixed names. Content is identical across platforms for the same skill.

---

## Repository Structure

```
agency-agents/
├── .claude/
│   └── skills/             # Claude Code skill directories
│       ├── academic-anthropologist/
│       │   └── SKILL.md
│       ├── engineering-code-reviewer/
│       │   └── SKILL.md
│       └── ...
├── .agents/
│   └── skills/             # Cross-agent skill directories
│       ├── academic-anthropologist/
│       │   └── SKILL.md
│       ├── engineering-code-reviewer/
│       │   └── SKILL.md
│       └── ...
├── .opencode/
│   └── skills/             # OpenCode built-in skills (untouched)
│       ├── openspec-propose/
│       ├── openspec-apply-change/
│       ├── openspec-archive-change/
│       └── openspec-explore/
├── AGENTS.md               # Detailed conventions and workflow guidance
└── README.md               # This file
```

---

## Quick Start

### Claude Code

Place skill directories in `.claude/skills/` in your project. Claude Code auto-discovers skills from this location.

### Compatible Coding Agents (OpenCode, Codex, Cline, Cursor, Gemini CLI, Copilot, etc.)

Place skill directories in `.agents/skills/` in your project. Supported agents auto-discover skills from this location.

---

## Skill Directory Structure

Each skill lives in a named directory containing a single `SKILL.md`:

```
<category-prefixed-name>/
  SKILL.md
```

Example:

```
academic-anthropologist/
  SKILL.md
```

### Frontmatter Schema

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

| Field              | Description                                                        |
| ------------------ | ------------------------------------------------------------------ |
| `name`             | Category-prefixed directory name                                   |
| `description`      | Agent/skill description (preserved from original agent)            |
| `license`          | Always `MIT`                                                       |
| `compatibility`    | `"Requires Claude Code"` or `"Requires a compatible coding agent"` |
| `metadata.author`  | Always `agency-agents`                                             |
| `metadata.version` | Always `"1.0"`                                                     |

---

## Naming Convention

All skills use **category-prefixed kebab-case names**:

| Category      | Prefix                | Examples                                                    |
| ------------- | --------------------- | ----------------------------------------------------------- |
| Academic      | `academic-`           | `academic-anthropologist`, `academic-geographer`            |
| Design        | `design-`             | `design-brand-guardian`, `design-ui-designer`               |
| Engineering   | `engineering-`        | `engineering-code-reviewer`, `engineering-devops-automator` |
| Finance       | `finance-`            | `finance-bookkeeper-controller`, `finance-tax-strategist`   |
| Marketing     | `marketing-`          | `marketing-seo-specialist`, `marketing-tiktok-strategist`   |
| Paid Media    | `paid-media-`         | `paid-media-auditor`, `paid-media-ppc-strategist`           |
| Product       | `product-`            | `product-manager`, `product-behavioral-nudge-engine`        |
| Project Mgmt  | `project-management-` | `project-management-project-shepherd`                       |
| Sales         | `sales-`              | `sales-coach`, `sales-engineer`                             |
| Specialized   | `specialized-`        | `specialized-chief-of-staff`, `specialized-mcp-builder`     |
| Support       | `support-`            | `support-analytics-reporter`, `support-support-responder`   |
| Testing       | `testing-`            | `testing-accessibility-auditor`, `testing-api-tester`       |
| Uncategorized | (none)                | `game-audio-engineer`, `narrative-designer`                 |

---

## Skill Categories

Skills span a wide range of domains, including but not limited to:

- **Engineering** — Software architecture, DevOps, security, data engineering, blockchain
- **Marketing** — SEO, social media, content creation, paid media, influencer strategy
- **Sales** — Outreach, pipeline analysis, deal strategy, account expansion
- **Product** — Product management, sprint prioritization, UX research, trend analysis
- **Finance** — FP&A, investment research, bookkeeping, tax strategy
- **Legal** — Document review, compliance, client intake, billing
- **Gaming** — Unity, Unreal Engine, Godot, Roblox, game design, shaders
- **Creative** — Visual storytelling, image prompting, inclusive design
- **Specialized** — Salesforce, MCP servers, cultural intelligence, regional business navigation
- **Academic** — History, anthropology, psychology, geography, narratology

---

## Contributing

- **No CI, tests, or pre-commit hooks** — this is a content-only repository
- When creating a new skill, follow the directory and frontmatter structure above
- Skills must be placed in both `.claude/skills/` and `.agents/skills/` with the same canonical name
- When editing a skill that exists in both platforms, apply the change to both unless it's platform-specific
- Use the unified category-prefixed naming convention for all new skills

For full workflow guidance, see [`AGENTS.md`](./AGENTS.md).

---

## License

This project is licensed under the [MIT License](./LICENSE).

---

## Acknowledgments

Built for teams and individuals who want modular, swappable AI expertise across their development and creative workflows.
