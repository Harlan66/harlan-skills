# Skill README 模板

复制下面内容到每个 Skill 的 `README.md`，再按实际情况删改。

````markdown
# skill-name

一句话说明这个 Skill 解决什么问题。

## 适合什么时候用

- 场景一
- 场景二
- 场景三

## 不适合什么时候用

- 不适合的场景一
- 不适合的场景二

## 安装方式

把本目录复制到你的 AI 工具指定的 Skills 目录，或从 GitHub 仓库中按需下载。

## 使用示例

```text
请使用这个 Skill 完成……
```

## 目录说明

```text
skill-name/
├── README.md
├── SKILL.md
├── agents/
├── references/
├── scripts/
└── assets/
```

## 维护说明

- 核心执行规则写在 `SKILL.md`。
- 长说明、案例和规范写在 `references/`。
- 可重复使用的小工具放在 `scripts/`。
- 模板和素材放在 `assets/`。

## 隐私和限制

说明是否包含外部资料、账号相关内容、人工判断环节或使用限制。
````

## SKILL.md 基础模板

````markdown
---
name: skill-name
description: Use when the user needs [specific trigger or situation].
---

# Skill Name

## When to Use

- Use this skill when...

## Workflow

1. Do the first essential step.
2. Check the relevant references only when needed.
3. Verify the result before reporting completion.

## References

- Read `references/example.md` when...
````
