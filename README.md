# Agency Agents

A curated collection of AI agent definitions for dual-platform use — **Claude Desktop/IDE** and **OpenCode**.

Each agent is a self-contained markdown file that defines a specialist persona, enabling AI assistants to adopt domain-specific expertise, workflows, and communication styles on demand.

> **Original repository:** [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents)

---

## Overview

This repository contains **186+ agent definitions** across two platforms, covering disciplines from software engineering and marketing to finance, legal, gaming, and academia. Agents are designed to function as modular, swappable experts that can be invoked contextually within AI-powered workflows.

### Supported Platforms

| Platform     | Directory           | Count      | Notes                                |
| ------------ | ------------------- | ---------- | ------------------------------------ |
| **Claude**   | `.claude/agents/`   | 186 agents | Uses category-prefixed filenames     |
| **OpenCode** | `.opencode/agents/` | 186 agents | Uses flat filenames without prefixes |

> **Note:** The two agent sets are **not in sync**. Some agents exist only on one platform. See [Conventions](#conventions) below.

---

## Repository Structure

```
agency-agents/
├── .claude/
│   └── agents/           # Claude Desktop/IDE agent definitions
│       ├── academic-historian.md
│       ├── engineering-senior-developer.md
│       ├── marketing-seo-specialist.md
│       └── ...
├── .opencode/
│   └── agents/           # OpenCode agent definitions
│       ├── historian.md
│       ├── senior-developer.md
│       ├── seo-specialist.md
│       └── ...
├── AGENTS.md             # Detailed conventions and workflow guidance
└── README.md             # This file
```

---

## Quick Start

### Claude Desktop/IDE

1. Copy the desired agent markdown file(s) from `.claude/agents/` into your Claude agents directory.
2. Restart Claude or refresh the agent list.
3. Invoke the agent by name in your conversation.

### OpenCode

1. Copy the desired agent markdown file(s) from `.opencode/agents/` into your OpenCode agents directory.
2. The agent will be available as a subagent or mode depending on your OpenCode configuration.

---

## Conventions

### File Naming

- **Claude:** Uses category prefixes for grouping (e.g., `engineering-`, `marketing-`, `sales-`, `specialized-`)
- **OpenCode:** Uses flat, human-readable names without prefixes

### Frontmatter Schemas

Each platform uses a distinct YAML frontmatter block:

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

> Do not mix fields across platforms. Claude uses `emoji` and `vibe`; OpenCode uses `mode`.

### OpenCode NPM State

The `.opencode/` directory contains a `package.json` for local plugin dependency resolution, but it is intentionally untracked:

- `.opencode/package.json` and `.opencode/package-lock.json` are `.gitignore`d
- `.opencode/node_modules/` is also ignored
- Do not commit these files

---

## Contributing

- **No CI, tests, or pre-commit hooks** — this is a content-only repository
- When creating a new agent, mirror the frontmatter and heading structure of existing agents in the target platform
- When editing an agent that exists in both platforms, consider whether the change should apply to both or is platform-specific
- There is no automated sync between platforms — manual maintenance is required

For full workflow guidance, see [`AGENTS.md`](./AGENTS.md).

---

## Agent Categories

Agents span a wide range of domains, including but not limited to:

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

## License

This project is licensed under the [MIT License](./LICENSE).

---

## Acknowledgments

Built for teams and individuals who want modular, swappable AI expertise across their development and creative workflows.
