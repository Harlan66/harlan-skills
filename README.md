# harlan-skills

Reusable Codex skills by Harlan.

This repository collects practical Codex Skills that I use in real work, especially for content production, publishing workflows, research, writing, and repeatable personal productivity tasks.

If you use Codex and want ready-made workflows instead of rewriting the same instructions every time, this repo is for you.

## What You Can Use This For

- Reuse proven Codex workflows for specific tasks.
- Learn how to structure your own Codex Skills.
- Copy individual Skills into your own Codex setup.
- Adapt the templates here to build a personal Skill library.

## Available Skills

| Skill | What it does | Status |
| --- | --- | --- |
| `_template` | Starter template for creating a new Skill | Template |

More Skills will be added over time.

## How to Use

Clone this repository:

```bash
git clone https://github.com/Harlan66/harlan-skills.git
```

Then copy the Skill you want into your local Codex Skills directory.

Example:

```bash
cp -R harlan-skills/skills/_template ~/.codex/skills/my-new-skill
```

After copying, rename the folder and update the Skill files for your own use.

## Skill Structure

Each Skill follows this general layout:

```text
skill-name/
├── README.md
├── SKILL.md
├── agents/
├── references/
├── scripts/
└── assets/
```

The important parts are:

- `README.md`: explains the Skill for people browsing GitHub.
- `SKILL.md`: contains the instructions Codex reads when the Skill is used.
- `references/`: stores longer guides, examples, or style rules.
- `scripts/`: stores helper scripts when a workflow needs repeatable actions.
- `assets/`: stores templates, images, or other supporting files.

## Create Your Own Skill

Use `skills/_template` as a starting point:

1. Copy the template folder.
2. Rename it with a short, clear Skill name.
3. Update `README.md` so users understand what the Skill does.
4. Update `SKILL.md` with the actual Codex instructions.
5. Add supporting files only when they are useful.

You can also read:

- `docs/skill-template.md`
- `docs/release-checklist.md`
- `docs/repository-guide.md`

## Star This Repo

If this repository helps you build better Codex workflows, please consider giving it a Star.

Stars help more people discover the project, and they also help me decide which Skills and templates are worth improving next.

## License

MIT License.
