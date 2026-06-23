---
name: harlan-tencent-meeting-share-transcript
description: Use when the user wants to extract or batch export transcript content from Tencent Meeting share links that provide an access password, especially cross-org share pages where the recording page already shows a transcript or minutes view. This skill is for lawful access to shared recording pages, transcript export, transcript pagination, and checking whether media files are actually downloadable.
---

# Tencent Meeting Share Transcript

## Overview

Use this skill for Tencent Meeting recording share pages such as `https://meeting.tencent.com/crm/...` when the user provides a share link and access password and wants the transcript content, structured minutes, or a batchable extraction workflow.

This skill is for transcript extraction from the shared page, not permission bypass. It is common for transcript data to be readable while media files remain non-downloadable.

## When To Use

- The user has a Tencent Meeting recording share link plus access password.
- The user wants transcript text, verbatim content, minutes JSON, or a batch extraction workflow.
- The user wants to know whether audio/video can be downloaded from the same share page.
- The page is a recording share, not a live meeting join flow.

Do not use this skill to bypass permissions, steal cookies, or force downloads when the page reports that media is not downloadable.

## Workflow

### 1. Open The Share Page In A Real Browser

Prefer the Playwright CLI skill in headed mode because Tencent Meeting share pages are more reliable in a visible browser session than in pure headless automation.

Use this sequence:

```bash
export CODEX_HOME="${CODEX_HOME:-$HOME/.codex}"
export PWCLI="$CODEX_HOME/skills/playwright/scripts/playwright_cli.sh"

bash "$PWCLI" open "https://meeting.tencent.com/crm/SHARE_CODE" --headed
bash "$PWCLI" snapshot
```

If the page shows `请输入访问密码`, fill the password and continue:

```bash
bash "$PWCLI" fill eX "PASSWORD"
bash "$PWCLI" click eY
bash "$PWCLI" snapshot
```

Expected success signals:

- The page title remains `录制文件`
- The main page shows `视频` and `逐字稿`
- `另存为` may still be disabled

Failure signals:

- `无法访问`
- `文件涉嫌违反相关法律法规或平台服务协议`
- The page never progresses past the password prompt

If blocked, stop and report the recording as inaccessible.

### 2. Switch To The Transcript Tab

After the recording page loads, click `逐字稿` and re-snapshot. This matters because the transcript endpoint may not appear until after the transcript tab is opened.

```bash
bash "$PWCLI" click eTRANSCRIPT
bash "$PWCLI" snapshot
```

### 3. Read The In-Page Transcript Endpoint

After the transcript tab is open, inspect the page's loaded resources and fetch the same endpoint the page uses. The verified endpoint pattern is:

- `/wemeet-cloudrecording-webapi/v1/minutes/detail`

Also inspect these related endpoints:

- `/get-multi-record-file`
- `/wemeet-cloudrecording-webapi/v1/sign`

Use `page.evaluate` with `credentials: "include"` so the browser reuses the lawful page session:

```js
async () => {
  const resources = performance.getEntriesByType("resource").map(r => r.name);
  const minutesUrl = [...resources].reverse().find(u => u.includes("/wemeet-cloudrecording-webapi/v1/minutes/detail"));
  const fileUrl = [...resources].reverse().find(u => u.includes("/get-multi-record-file"));
  const signUrl = [...resources].reverse().find(u => u.includes("/wemeet-cloudrecording-webapi/v1/sign"));
  return { minutesUrl, fileUrl, signUrl };
}
```

### 4. Paginate The Transcript

The transcript response is typically shaped like:

- top-level `code`
- top-level `minutes`
- top-level `more`
- `minutes.paragraphs[]`

Each paragraph usually contains:

- `pid`
- `start_time`
- `end_time`
- `speaker.user_name`
- `sentences[]`
- `sentences[].words[].text`

When paginating, start from `pid=0` and `start_pid=0`, and set a limit such as `20`. Keep requesting until `more` becomes false.

Practical pattern:

1. Parse the first observed `minutes/detail` URL with `new URL(...)`.
2. Remove any existing `pid`, `start_pid`, and `limit`.
3. Set:
   - `limit=20`
   - `start_pid=0`
   - `pid=0`
4. Fetch the URL.
5. Append `minutes.paragraphs`.
6. If `more` is true, set both `pid` and `start_pid` to `last_pid + 1`.
7. Repeat.

Important: `minutes` is often an object with `paragraphs`, not a plain array.

## Output Format

Save two outputs whenever possible:

- `json`: full structured payload with timestamps, speakers, paragraphs, and permission metadata
- `txt`: flattened transcript lines in the format `[HH:MM:SS] speaker: text`

Recommended flattening rule:

```text
[00:00:20] su: 我们来先来介绍一下这本书的背景，这本书的作者是豆豆！
```

Build each line by:

1. Taking `paragraph.start_time`
2. Formatting to `HH:MM:SS`
3. Reading `paragraph.speaker.user_name`
4. Concatenating all `sentence.words[].text`

## Media Permission Check

Always inspect `/get-multi-record-file` and report the permission state. The important fields are typically:

- `data.files[].resource_type`
- `data.files[].resource_id`
- `data.files[].size`
- `data.files[].downloadable`

Interpretation:

- If any `downloadable` value is `true`, the page likely allows a lawful media download path.
- If all `downloadable` values are `false`, report that transcript extraction is available but media download is not.

Also inspect `/wemeet-cloudrecording-webapi/v1/sign` to determine whether playback streams exist. Playback availability does not imply download permission.

## Reporting Rules

Report these facts explicitly:

- Whether the recording page was accessible
- Whether transcript extraction succeeded
- How many transcript paragraphs or pages were collected
- Whether any media file is downloadable
- Whether playback streams exist

Keep these distinctions clear:

- `transcript readable` does not mean `audio/video downloadable`
- `playable in page` does not mean `downloadable`

## Guardrails

- Use only the session created by lawful access to the provided share page.
- Do not suggest stealing or importing someone else's cookies.
- Do not present playback URLs as downloadable files unless the page permissions allow it.
- If the share page is blocked or removed, stop and report that result.

## Reference

Load [references/extraction-snippets.md](./references/extraction-snippets.md) when you need ready-to-run Playwright CLI snippets or the verified response patterns for transcript and media inspection.
