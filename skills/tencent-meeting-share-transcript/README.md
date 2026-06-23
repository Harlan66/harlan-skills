# tencent-meeting-share-transcript

从合法可访问的腾讯会议录制分享页中提取逐字稿或会议纪要。

## 适合什么时候用

- 你有腾讯会议录制分享链接和访问密码。
- 分享页中能正常看到逐字稿或纪要。
- 你需要导出逐字稿、结构化纪要或批量提取流程。
- 你想判断录制页里的音视频是否真的可下载。

## 不适合什么时候用

- 绕过权限。
- 获取未授权内容。
- 偷取或复用他人的登录状态。
- 强制下载页面明确不允许下载的媒体文件。

## 使用方式

把整个 `tencent-meeting-share-transcript` 文件夹复制到你的 AI 工具 Skills 目录中，然后提供分享链接和访问密码。

示例：

```text
请使用 tencent-meeting-share-transcript，帮我导出这个腾讯会议分享页里的逐字稿。
```

## 目录说明

- `SKILL.md`：提取流程、浏览器操作和安全边界。
- `references/extraction-snippets.md`：常用提取片段。
- `agents/openai.yaml`：展示信息。
