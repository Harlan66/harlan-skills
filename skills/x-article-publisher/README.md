# x-article-publisher

把 Markdown 文章整理并发布到 X Articles 草稿编辑器。

这个 Skill 关注的是“发布草稿”，不是自动公开发布。它会帮助 AI Agent 解析 Markdown、保留富文本格式、处理封面图、正文图片、表格和分割线。

## 适合什么时候用

- 需要把 Markdown 文章发布到 X Articles。
- 文章包含标题、封面图、正文图片或分割线。
- 需要把表格或 Mermaid 图转成图片后插入。
- 需要保留标题、列表、加粗、链接等富文本格式。

## 使用前准备

- 你需要能访问 X Articles 编辑器。
- 你需要已登录可使用 X Articles 的账号。
- 本地需要 Python。
- 如果文章里有表格或图表，可能需要额外图片处理依赖。

## 使用方式

把整个 `x-article-publisher` 文件夹复制到你的 AI 工具 Skills 目录中，然后提供 Markdown 文件路径或文章内容。

示例：

```text
请使用 x-article-publisher，把这篇 Markdown 文章整理到 X Articles 草稿里。
```

## 目录说明

- `SKILL.md`：发布流程和编辑器操作规则。
- `scripts/parse_markdown.py`：解析 Markdown。
- `scripts/copy_to_clipboard.py`：复制富文本或图片到剪贴板。
- `scripts/table_to_image.py`：把表格转为图片。

## 安全说明

这个 Skill 只负责整理并保存草稿，不应自动点击公开发布。最终发布动作应由使用者自己确认。
