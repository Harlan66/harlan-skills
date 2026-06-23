# Current WeChat Layout Style

## Current Project Context

- Main project: a local WeMD workspace.
- App preview: `http://localhost:4173/`.
- Preview server: `pnpm --filter @wemd/web preview -- --host 127.0.0.1`.
- Local image proxy: `pnpm --filter @wemd/server start`, expected at `http://localhost:4000`.
- Current article folder pattern: `articles/<slug>/`.
- Public image folder pattern: `apps/web/public/article-assets/<slug>/`.
- Current theme file example: `apps/web/src/store/themes/aiLearningBlueTheme.ts`.

## Style Direction

The selected article direction is a restrained deep-blue knowledge article style:

- serious, clear, and long-term reusable;
- no green theme;
- no large dark filled title blocks;
- no random keyword coloring;
- title modules and content modules must be visually distinct.

Palette:

- Main text: `#17233a` or `#22304a`.
- Primary navy: `#10233f`.
- Secondary blue: `#183b67` or `#2368a2`.
- Accent blue: `#7fb6f2` or `#8cbdec`.
- Light background: `#eaf3ff` or `#f8fbff`.
- Border: `#cfe2f8`.

## Module Rules

### Featured Summary

Use once near the opening of each long-form article.

- Position: immediately after the cover image and before the first body paragraph.
- Length: 120 Chinese characters or fewer.
- Purpose: give readers a concise preview of the article's core judgment and reading path.
- Markdown form:

```markdown
> **精选摘要**：AI 时代，学习的关键不再是和机器比记忆与执行，而是先判断什么值得学，再用 AI 做定制化、项目化学习，并把工具变成长期协作的知识系统。
```

- Style: reuse the quote module, but treat it as an opening card. It should be visually lighter than a section title and stronger than an ordinary paragraph.
- Content rule: this is an editorial guide generated from the article, not a replacement for the user's original text. Do not change `source.md`.
- Keep this as the default opening module for long WeChat articles unless the user explicitly removes it.

### Main Section Title

Use for `##` only.

- Shape: minimalist left-line.
- Layout: small label above title, title below.
- Label examples: `SECTION`, `METHOD`, `PART`.
- Accent: one dark-blue vertical line on the left.
- Avoid: large filled rectangle, heavy colored block, rounded banner.

### Subsection Title

Use for `###`.

- Smaller than H2.
- Can use a thin underline or short left accent.
- Should not look like the main title module.

### Quote or Key Sentence

Use for `>`.

- Shape: simple left-line quote.
- Background: white or very light blue.
- Purpose: rhythm break, summary, or important observation.
- Avoid: using it for every paragraph.

### List or Tag Card

Use for summary lists and method lists.

- Background: white.
- Border: 1px light blue.
- Shadow: subtle light-blue offset shadow.
- Bullets: dark navy dots or simple tag-like list rows.
- Avoid: dense solid background or decorative card inside card.

## Inline Emphasis

Use emphasis to control reading rhythm, not to decorate.

- `++concept++`: important term or recurring concept. Render as blue underline.
- `==judgment==`: key conclusion or judgment sentence. Render as light blue highlight.
- `**emphasis**`: only when the original article already needs strong emphasis or the sentence is a core claim.

Rules:

- Do not use `**++text++**`; this can render literal `**`.
- Do not highlight more than one or two phrases in a paragraph.
- Do not color random words just because they sound important.
- Prefer highlighting concepts, contrasts, method names, and turning points.

## Image Rules

Current selected style:

- Hand-drawn knowledge-card style.
- Clean white or light-blue background.
- Deep navy linework.
- Small blue accent labels and simple symbolic elements.
- Light paper texture is acceptable if subtle.

Cover text rule:

- Do not reuse the article title verbatim on the cover.
- Article title and cover text should work as a pair: the title names the topic, while the cover text gives the sharper conclusion, tension, or hook.
- Prefer short cover text that can be read quickly in a WeChat feed.

Default count for a long article:

- 1 cover image, 21:9.
- 5 to 7 inline images.

Recommended insertion rhythm:

1. Cover after the article title.
2. First conceptual transition.
3. AI capability boundary or limitation section.
4. Method/framework summary section.
5. Learning workflow section.
6. Tool-type explanation section.
7. Final summary or closing section.

Generated images should be saved twice:

- archival copy: `articles/<slug>/images/`;
- app-facing copy: `apps/web/public/article-assets/<slug>/`.

Markdown path format:

```markdown
![描述](/article-assets/<slug>/<file>.png)
```

When copying to WeChat, these local app-facing paths must not be copied as-is. The copy flow should upload or map them to HTTPS URLs first, then place the HTTPS URLs in the clipboard HTML. WeChat cannot fetch `localhost` images.

For local WeMD preview, keep the image proxy server running:

```bash
pnpm --filter @wemd/server start
```

The local web app uses this server to proxy official image uploads and avoid browser CORS failures from `https://api.wemd.app/upload`.

Before final copy, verify the upload chain with one actual article image:

```bash
curl -sS -w '\nHTTP_STATUS:%{http_code}\n' \
  -F 'file=@apps/web/public/article-assets/<slug>/<image>.png' \
  http://localhost:4000/api/upload/official
```

Success criteria:

- HTTP status is `201`;
- returned `url` starts with `https://`;
- no copied image URL remains `localhost`, `127.0.0.1`, or `/article-assets/...`.

If the UI shows `复制失败: Failed to fetch`:

1. Check `lsof -nP -iTCP:4000 -sTCP:LISTEN`.
2. Start `pnpm --filter @wemd/server start` if nothing is listening.
3. Test one image with the `curl` command above.
4. Only then retry `复制到公众号`.

Do not diagnose this as a Markdown or style problem until the proxy and upload test pass.

## Source Preservation

Treat `source.md` as the truth.

Allowed layout-only additions in `article-wechat-layout.md`:

- image Markdown lines;
- separators such as `---`;
- one featured summary quote after the cover image;
- blockquote marker `>`;
- emphasis markers `++...++`, `==...==`, `**...**`;
- heading markers that reflect the original heading structure.

Not allowed unless explicitly requested:

- rewriting paragraphs;
- changing article title;
- adding "配图建议" into the article body;
- deleting user-provided content;
- editing the original uploaded file.

## Browser Edit Capture

When the user edits directly in WeMD, the browser editor is the newest version.

Before refreshing, rebuilding, repairing history, or changing default article wiring:

1. Focus the WeMD Markdown editor.
2. Select all editor text and copy it.
3. Save the copied Markdown to `articles/<slug>/article-wechat-layout.md`.
4. Re-read the saved file and confirm it exactly matches the copied browser text.

Do not overwrite `source.md` with browser-edited layout content. Browser edits can include images, separators, quote wrappers, and emphasis markers.

If automation cannot directly read editor state, use the clipboard route:

```text
click editor -> select all -> copy -> read clipboard -> write article-wechat-layout.md
```

This prevents user edits from being lost when WeMD history, preview reloads, or default article imports change.

## WeMD Theme Binding

If the preview unexpectedly shows green accents or default styling, inspect the active theme before changing article Markdown.

Expected theme:

- name: `深蓝知识卡片`;
- H2: dark-blue left line with small `SECTION` label;
- quote/summary: light-blue card, not green;
- list card: white background, light-blue border, light-blue offset shadow.

Common root cause:

- Browser-side history restores an older article snapshot with `默认主题`.

Fix direction:

- ensure the current article snapshot uses the fixed deep-blue theme;
- update history recognition only for the intended managed article slug;
- avoid broad rules that replace unrelated user history entries.

## Verification Details

Recommended checks:

1. Confirm source file is byte-identical to the uploaded original when available.
2. Normalize `article-wechat-layout.md` by removing image lines, separators, blockquotes, and layout markers, then compare text against `source.md`.
3. Run the app build.
4. Open the browser preview and inspect:
   - no literal Markdown artifacts such as `**`;
   - no internal notes;
   - featured summary appears after the cover image and is no more than 120 Chinese characters;
   - images loaded;
   - copied images are converted to HTTPS URLs before pasting to WeChat;
   - H2 and list modules match the selected design.
5. If the user edited in WeMD during the session:
   - browser Markdown was saved to `article-wechat-layout.md`;
   - saved file exactly matches the copied browser text;
   - build was run after saving.
