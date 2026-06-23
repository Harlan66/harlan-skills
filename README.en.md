# harlan-skills

Harlan's AI Agent Skills collection.

[中文](README.md)

This repository collects reusable skills from real workflows: content creation, publishing, research, writing, product analysis, and personal productivity. Think of each Skill as a compact operating guide for an AI agent.

These Skills are not limited to Codex. They are written in a general Agent Skills structure so they can be adapted to tools such as Claude Code, Cursor, GitHub Copilot, Gemini CLI, Windsurf, and other AI agent environments with similar mechanisms.

## What This Repository Helps With

- Reuse practical AI agent workflows.
- Learn how to structure a maintainable Skills repository.
- Build your own personal Skill library from the template.
- Turn repeated prompts, rules, and workflows into reusable assets.

## Available Skills

| Skill | Description | Status |
| --- | --- | --- |
| `harlan-app-interaction-map` | Turns screenshots, recordings, routes, and notes into a structured interaction map. | Ready |
| `harlan-gzh-pb` | Prepares Chinese WeChat public account articles with fixed layout, visual style, and image planning rules. | Ready |
| `harlan-tencent-meeting-share-transcript` | Extracts transcript content from lawful Tencent Meeting recording share pages. | Ready |
| `harlan-x-article-publisher` | Publishes Markdown articles to X Articles drafts with formatting and media handling guidance. | Ready |
| `_template` | Starter template for creating a new Skill. | Template |

## Quick Start

Clone the repository:

```bash
git clone https://github.com/Harlan66/harlan-skills.git
```

Enter the repository:

```bash
cd harlan-skills
```

Copy the Skill you need into the Skills directory used by your AI tool.

Codex example:

```bash
cp -R skills/harlan-app-interaction-map ~/.codex/skills/harlan-app-interaction-map
```

If your tool uses another directory, copy the whole Skill folder there. The key structure is a folder that contains `SKILL.md`.

## How to Use a Skill

1. Pick a Skill from `skills/`.
2. Read that Skill's `README.md` to confirm it fits your task.
3. Copy the full Skill folder into your AI tool's Skills directory.
4. Ask your AI agent to perform a matching task.

If your tool does not support automatic Skill loading, open the Skill's `SKILL.md` manually and provide the instructions to your AI agent.

## Skill Structure

```text
harlan-skill-name/
├── README.md
├── SKILL.md
├── agents/
├── references/
├── scripts/
└── assets/
```

- `README.md`: human-facing introduction and usage guide.
- `SKILL.md`: core instructions for the AI agent.
- `references/`: longer examples, rules, and background material.
- `scripts/`: reusable helper scripts.
- `assets/`: templates, images, or sample files.
- `agents/`: optional metadata for tools that display Skills in an interface.

## Create Your Own Skill

Start from the template:

```bash
cp -R skills/_template skills/harlan-my-skill
```

Then update:

1. `README.md` for human readers.
2. `SKILL.md` for agent instructions.
3. `references/` for long examples and rules.
4. `scripts/` for repeatable helpers.
5. `assets/` for templates and reusable files.

Before sharing, see:

- `docs/skill-template.md`
- `docs/release-checklist.md`
- `docs/repository-guide.md`

## Who This Is For

- People who use AI agents for repeated work.
- People who want to turn prompts into maintainable workflows.
- Creators, researchers, product people, and builders who want reusable AI operating guides.
- Anyone learning how to structure Agent Skills.

## Star This Repository

If this repository helps you build better AI agent workflows, please consider giving it a Star.

Stars help more people discover the project and help me decide which Skills and templates to improve next.

## License

MIT License.
