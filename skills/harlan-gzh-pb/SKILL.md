---
name: harlan-gzh-pb
description: Use when preparing Chinese WeChat public account articles with WeMD, fixed Markdown-to-WeChat formatting, deep-blue visual themes, image planning/generation, cover and inline illustration consistency, and project-local workflow constraints.
---

# GZH PB

## Purpose

Use this skill for WeChat public account article production in the local WeMD project. It preserves the user's original article text, applies a stable deep-blue layout system, plans and inserts consistent images, and verifies the result in the browser before reporting.

For detailed style tokens, module patterns, image prompts, and verification rules, read `references/current-style.md` before editing an article or theme.

## Non-Negotiables

1. Preserve the original text. Never rewrite, expand, summarize, or rename the user's article unless explicitly asked.
2. Keep the uploaded source copy pristine. Store it as `articles/<slug>/source.md`; only add layout wrappers, emphasis markers, images, and separators in a derived layout file.
3. Keep work project-local. Related skills, references, prompts, and article files belong under the current folder, not global locations, unless the user explicitly requests global installation.
4. Use one visual language across cover and inline images. The current selected style is hand-drawn knowledge-card illustration.
5. Verify before reporting: build, browser preview, loaded images, no literal Markdown artifacts, and no unintended text changes.
6. One-click WeChat copy must not leave local `localhost` image URLs in the copied content. Local images must be uploaded or rewritten to HTTPS before clipboard output.
7. Do not make the cover text identical to the article title. The article title should state the topic, while the cover text should complement it with a sharper angle, takeaway, or curiosity hook.
8. If the user edits inside WeMD, save the current editor content back to `article-wechat-layout.md` before refreshing, rebuilding, or changing history state.

## Standard Workflow

1. Create an article folder: `articles/<slug>/`.
2. Copy the uploaded article exactly into `source.md`.
3. Create `article-wechat-layout.md` from `source.md`, adding only formatting, image references, and allowed wrappers.
4. Add a featured summary module after the cover image and before the first body paragraph.
5. Save image planning notes and prompts under `articles/<slug>/prompts/`.
6. Save generated images under `articles/<slug>/images/`, then copy public-facing versions to `apps/web/public/article-assets/<slug>/`.
7. Wire the layout into WeMD as the visible article content and choose the fixed deep-blue theme.
8. Build and inspect `http://localhost:4173/` in the browser.
9. Before final copy, start the local image proxy server and confirm one local article image can be converted to an HTTPS image URL.

## Formatting System

- `#` is the article title only.
- Add one featured summary after the cover image. It should be no more than 120 Chinese characters, summarize the article's core direction, and render as a quote-style card using `> **精选摘要**：...`.
- `##` is the main section title. Use the selected minimalist left-line style: dark-blue vertical line, small uppercase label, large navy title, no heavy filled block.
- `###` is a subsection title. Use a restrained underline or small left accent, not a large card.
- `>` is for quotes, recap sentences, or key observations. Use a light left-line quote style.
- Lists that summarize a method or framework should use the tag-card/list-card style: white background, light-blue border, subtle offset shadow.
- `++...++` marks important concepts or terms with a blue underline. Do not nest it inside `**...**`.
- `==...==` marks one key judgment or conclusion in a subsection. Use sparingly.
- `**...**` is only for necessary emphasis. Do not randomly bold keywords.
- Avoid green unless the user changes the theme direction. The selected theme is deep navy and light blue.

## Image System

- Default style: hand-drawn knowledge-card illustration.
- Cover ratio: 21:9.
- Cover text should complement the article title, not repeat it verbatim. Prefer a shorter, stronger phrase that captures the core judgment.
- Inline images should use the same style as the cover. Do not mix Notion line art, flat illustration, and hand-drawn card styles in the same article.
- Normal long-form article image count: one cover plus five to seven inline images.
- Insert images at real rhythm points: after the title, at major section transitions, before important method summaries, and near tool/workflow explanations.
- Use the `imagegen` skill and image generation tool for bitmap visuals unless the user asks for another route.
- When handing image generation to a parallel worker, include exact style, palette, aspect ratio, article topic, image count, output paths, and the rule that article text must not be changed.

## WeMD Notes

- Build check: `pnpm --filter @wemd/web build`.
- Preview server: `pnpm --filter @wemd/web preview -- --host 127.0.0.1`.
- Local image proxy server: `pnpm --filter @wemd/server start`. Keep it running on `http://localhost:4000` when one-click WeChat copy needs to upload local images.
- Browser target: `http://localhost:4173/`.
- Copy-to-WeChat should process local images before writing to clipboard: upload local preview images through the active image host, replace copied `<img src>` values with HTTPS URLs, and cache unchanged images to avoid repeated uploads.
- If WeMD shows `复制失败: Failed to fetch`, first check whether the local image proxy server is running on port 4000. Do not change article text while debugging copy failures.
- If the user says they edited the article in the browser, read/copy the current editor Markdown from WeMD and write it to `articles/<slug>/article-wechat-layout.md`; treat browser content as newer than the file.
- If the browser still shows old content, rebuild and restart preview. Also check whether browser-side saved history is overriding the default article.

## Verification Checklist

Before reporting completion:

1. Confirm the uploaded source copy was not modified.
2. Compare normalized layout text against `source.md` after removing images, separators, blockquote markers, and layout-only emphasis markers.
3. Confirm the app builds.
4. Inspect the browser preview and confirm:
   - article title and body are the user's original content;
   - featured summary appears after the cover image and before the body intro;
   - no literal `**` appears in rendered content;
   - no "配图建议" or internal notes appear in the article body;
   - images load successfully;
   - copied image URLs are HTTPS, not `localhost`;
   - H2 titles use the minimalist left-line style;
   - list cards use the selected tag-card/list-card style.
