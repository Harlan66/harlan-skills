# Extraction Snippets

Use these snippets with the `playwright` skill or with `playwright-cli` directly.

## Password Entry

```bash
PLAYWRIGHT_CLI_SESSION=tm-share npx --yes --package @playwright/cli playwright-cli open "https://meeting.tencent.com/crm/SHARE_CODE" --headed
PLAYWRIGHT_CLI_SESSION=tm-share npx --yes --package @playwright/cli playwright-cli snapshot
PLAYWRIGHT_CLI_SESSION=tm-share npx --yes --package @playwright/cli playwright-cli fill ePASSWORD "ACCESS_PASSWORD"
PLAYWRIGHT_CLI_SESSION=tm-share npx --yes --package @playwright/cli playwright-cli click eSUBMIT
PLAYWRIGHT_CLI_SESSION=tm-share npx --yes --package @playwright/cli playwright-cli snapshot
```

## Transcript Endpoint Discovery

After opening the transcript tab, inspect loaded resources:

```js
async () => {
  const resources = performance.getEntriesByType("resource").map(r => r.name);
  return {
    minutesUrl: [...resources].reverse().find(u => u.includes("/wemeet-cloudrecording-webapi/v1/minutes/detail")),
    fileUrl: [...resources].reverse().find(u => u.includes("/get-multi-record-file")),
    signUrl: [...resources].reverse().find(u => u.includes("/wemeet-cloudrecording-webapi/v1/sign")),
  };
}
```

## Transcript Pagination

The verified response shape is:

- `code`
- `minutes`
- `more`

`minutes` is usually an object with `paragraphs`. Each paragraph contains:

- `pid`
- `start_time`
- `end_time`
- `speaker.user_name`
- `sentences[].words[].text`

Pagination pattern:

1. Start with `pid=0`, `start_pid=0`, `limit=20`.
2. Fetch the transcript URL with `credentials: "include"`.
3. Append `minutes.paragraphs`.
4. If `more` is true, set `pid` and `start_pid` to `last_pid + 1`.
5. Repeat.

## Media Permission Check

Check `/get-multi-record-file` and inspect:

- `data.files[].resource_type`
- `data.files[].resource_id`
- `data.files[].size`
- `data.files[].downloadable`

If every `downloadable` value is `false`, the page is transcript-readable but media-not-downloadable.
