# harlan-skills

个人 Codex Skills 集合，用来整理、维护和分享可复用的工作流、经验规则和辅助工具。

## 这个仓库适合放什么

- 可以反复使用的个人工作方法
- 已经验证过的内容生产、整理、检查、发布流程
- 面向特定场景的 Codex 使用规则
- 可复用的模板、参考资料和小工具

不建议放一次性项目记录、聊天摘录、私人账号信息、未脱敏资料或只适合单个项目的临时规则。

## 目录结构

```text
harlan-skills/
├── README.md
├── LICENSE
├── docs/
│   ├── skill-template.md
│   └── release-checklist.md
└── skills/
    └── skill-name/
        ├── README.md
        ├── SKILL.md
        ├── agents/
        ├── references/
        ├── scripts/
        └── assets/
```

## Skill 列表

| Skill | 用途 | 状态 |
| --- | --- | --- |
| `_template` | 新 Skill 的复制模板 | 模板 |

## 单个 Skill 的文档分工

- `README.md`：给人看的说明，包括用途、安装、示例和维护说明。
- `SKILL.md`：给 Codex 看的核心规则，只保留真正影响执行的内容。
- `references/`：较长的参考材料、风格规范、案例说明。
- `scripts/`：可重复使用的小工具。
- `assets/`：模板、图片、示例文件等素材。
- `agents/openai.yaml`：Skill 在界面中展示时使用的简短信息。

## 新增一个 Skill

1. 复制 `skills/_template/`。
2. 把目录名改成小写英文、数字和连字符组成的名字。
3. 填写该 Skill 的 `README.md`。
4. 编写精简的 `SKILL.md`。
5. 按需补充 `references/`、`scripts/` 和 `assets/`。
6. 按 `docs/release-checklist.md` 检查后再发布。

## 维护原则

- 一个 Skill 只解决一类明确问题。
- 说明文档面向人，执行规则面向 Codex。
- 复杂说明放到 `references/`，不要塞进 `SKILL.md`。
- 发布前删除私人信息、账号信息、临时路径和未授权内容。
- 每次调整后，用真实场景检查一次是否还能按预期工作。
