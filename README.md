<div align="center">

# harlan-skills

**Harlan 的 AI Agent Skills 索引。**

[English](README.en.md) | **简体中文**

[![GitHub stars](https://img.shields.io/github/stars/Harlan66/harlan-skills?style=for-the-badge&logo=github)](https://github.com/Harlan66/harlan-skills/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/Harlan66/harlan-skills?style=for-the-badge&logo=github)](https://github.com/Harlan66/harlan-skills/forks)
[![GitHub issues](https://img.shields.io/github/issues/Harlan66/harlan-skills?style=for-the-badge&logo=github)](https://github.com/Harlan66/harlan-skills/issues)
[![Last commit](https://img.shields.io/github/last-commit/Harlan66/harlan-skills?style=for-the-badge)](https://github.com/Harlan66/harlan-skills/commits/main)
[![License](https://img.shields.io/github/license/Harlan66/harlan-skills?style=for-the-badge)](LICENSE)

[当前 Skills](#当前包含的-skills) · [快速开始](#快速开始) · [如何使用](#如何使用某个-skill) · [创建 Skill](#创建你自己的-skill) · [Star 支持](#给这个仓库点-star)

</div>

这里汇总我在真实工作中沉淀出来的可复用 Skills，适用于内容创作、资料整理、发布流程、研究写作和个人效率场景。你可以把它理解成一个 Skill 导航页：从这里找到对应 Skill，再跳转到独立仓库查看完整说明和安装方式。

这些 Skills 不只面向 Codex，也尽量采用通用的 Agent Skills 结构，方便迁移到 Claude Code、Cursor、GitHub Copilot、Gemini CLI、Windsurf 等支持类似机制的 AI 工具中。

## 这个仓库能帮你做什么

- 直接复用我整理好的 AI Agent 工作流。
- 学习如何组织一个清晰、可维护的 Skills 仓库。
- 基于模板创建自己的个人技能库。
- 把常用提示词、流程、规范和辅助文件沉淀成可长期维护的资产。

## 当前包含的 Skills

| Skill | 说明 | 状态 |
| --- | --- | --- |
| [`harlan-app-interaction-map`](https://github.com/Harlan66/harlan-app-interaction-map) | 把截图、录屏、页面列表和路由线索整理成结构化交互地图 | 独立仓库 |
| [`harlan-goal-mode-planner`](https://github.com/Harlan66/harlan-goal-mode-planner) | 把模糊目标整理成适合 Goal Mode 长时间执行的清晰目标 | 独立仓库 |
| [`harlan-gzh-pb`](https://github.com/Harlan66/harlan-gzh-pb) | 中文微信公众号文章排版、配图规划和发布前检查 | 独立仓库 |
| [`harlan-tencent-meeting-share-transcript`](https://github.com/Harlan66/harlan-tencent-meeting-share-transcript) | 从合法可访问的腾讯会议录制分享页中提取逐字稿 | 独立仓库 |
| [`harlan-x-article-publisher`](https://github.com/Harlan66/harlan-x-article-publisher) | 把 Markdown 文章整理到 X Articles 草稿编辑器 | 独立仓库 |
| [`_template`](skills/_template) | 创建新 Skill 的起始模板 | 模板 |

## 快速开始

克隆仓库：

```bash
git clone https://github.com/Harlan66/harlan-skills.git
```

进入仓库：

```bash
cd harlan-skills
```

如果你的工具支持 `skills add`，可以直接安装单个 Skill：

```bash
npx skills add Harlan66/harlan-goal-mode-planner
```

也可以安装其他独立 Skill：

```bash
npx skills add Harlan66/harlan-app-interaction-map
npx skills add Harlan66/harlan-gzh-pb
npx skills add Harlan66/harlan-tencent-meeting-share-transcript
npx skills add Harlan66/harlan-x-article-publisher
```

如果你的工具不支持 `skills add`，进入对应独立仓库，按该仓库 README 中的手动安装方式复制 Skill 文件夹。

## 如何使用某个 Skill

1. 在上方表格中选择一个 Skill。
2. 进入独立仓库查看完整使用说明。
3. 按该仓库 README 安装 Skill。
4. 在对话中描述任务，AI 会在合适的时候读取对应 Skill。

如果你的工具不支持自动加载 Skills，也可以手动打开该 Skill 的 `SKILL.md`，把其中的规则交给 AI 使用。

## Skill 的基本结构

```text
harlan-skill-name/
├── README.md
├── SKILL.md
├── agents/
├── references/
├── scripts/
└── assets/
```

常见文件说明：

- `README.md`：给使用者看的介绍，说明这个 Skill 能做什么、怎么用。
- `SKILL.md`：给 AI Agent 看的核心规则。
- `references/`：较长的参考资料、案例、风格规范。
- `scripts/`：可重复运行的辅助脚本。
- `assets/`：模板、图片、示例文件等素材。
- `agents/`：面向部分工具的展示信息。

## 创建你自己的 Skill

你可以从模板开始：

```bash
cp -R skills/_template skills/harlan-my-skill
```

然后依次修改：

1. `README.md`：写给使用者，说明用途、安装和示例。
2. `SKILL.md`：写给 AI Agent，保留最核心的执行规则。
3. `references/`：放长说明、案例和规范。
4. `scripts/`：放可重复使用的小工具。
5. `assets/`：放模板和素材。

发布前可以参考：

- `docs/skill-template.md`
- `docs/release-checklist.md`
- `docs/repository-guide.md`

## 适合谁

- 经常使用 AI Agent 处理重复任务的人。
- 想把提示词升级成可维护工作流的人。
- 想整理个人知识、创作流程、发布流程的人。
- 想学习 Agent Skills 仓库结构的人。

## 给这个仓库点 Star

如果这个仓库对你有帮助，欢迎点一个 Star。

你的 Star 会帮助更多人发现这个项目，也会让我知道哪些 Skills 和模板值得继续完善。

## 许可证

MIT License。
