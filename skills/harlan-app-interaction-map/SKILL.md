---
name: harlan-app-interaction-map
description: Use when turning App screenshots, screen recordings, reverse-engineered page lists, routes, APIs, or navigation notes into a reliable interaction map for product, design, QA, or Figma handoff.
---

# App Interaction Map

## Overview

Use this skill to convert evidence from real App usage plus reverse-engineered structure into an interaction map: what the user sees, what they do, what happens, where it goes, and which parts are confirmed, inferred, or unknown.

The goal is not a screenshot wall. The goal is a stable product map that lets a designer, product person, or engineer understand flows, branches, states, and gaps without replaying the App.

Write user-facing summaries and final deliverables in the user's language unless they request another language.

## Input Contract

Ask for or discover these inputs:

- Screenshot folder, screen recording frames, or exported images.
- Reverse-engineered materials: page list, route map, APIs, view names, navigation notes, UI docs, architecture docs, or decompiled source folders.
- Target platform and version if known: iPhone, Android, simulator, real device, logged-in status, region, subscription state.
- Desired output target: Markdown, Figma, FigJam, spreadsheet, or both Markdown and Figma.

If some inputs are missing, continue with available evidence and mark gaps explicitly. Do not pretend inferred paths are confirmed.

## Completion Criteria

Before reporting completion, verify that:

- Every provided screenshot is cataloged or intentionally excluded with a reason.
- Every reverse-engineered page/route is covered as confirmed, inferred, unknown, or out of scope.
- Main flows, branch flows, error states, empty states, permissions, and destructive actions are represented.
- Each interaction node includes trigger, effect, destination/state, and evidence/confidence.
- Open questions and missing screenshots are listed separately from confirmed behavior.
- If Figma is requested, the canvas is organized by functional modules, not by upload order or "supplement" buckets.

## Workflow

### 1. Establish the Evidence Base

Inventory the assets first:

- List screenshot files, dimensions, timestamps, and naming patterns.
- Identify duplicate, near-duplicate, blank, or transitional screenshots.
- Read reverse-engineered docs with headings and route/API names first, then inspect source only when docs are insufficient.
- Create a short evidence summary: screenshot count, reverse files read, covered modules, missing context.

### 2. Build a Screen Catalog

For each distinct screen/state, assign a stable screen ID and a human-readable name.

Capture:

- Screenshot reference.
- Visible purpose.
- Entry points.
- Exit points.
- Important controls.
- State: empty, loading, success, failure, permission, modal, sheet, keyboard, destructive confirmation, offline, paywall.
- Confidence: confirmed from screenshot, inferred from route/source, or unknown.

Do not merge screens just because they look similar if their state or user consequence differs.

### 3. Extract Reverse-Engineered Structure

Use reverse materials to create a candidate map:

- Page/view names.
- Routes and navigation edges.
- API calls or backend events tied to user actions.
- Feature flags, login gates, subscription gates, permission gates.
- Lifecycle and system behavior: background/foreground, retry, cache, keyboard, deeplink, notification, share sheet.

Treat reverse-engineered structure as a guide, not final truth. Real screenshots confirm visual and behavioral reality.

### 4. Cross-Validate Screens Against Routes

Create four buckets:

- Confirmed: screenshot and reverse structure agree.
- Inferred: reverse structure exists but screenshot is missing.
- Screenshot-only: screen appears in captures but is not found in reverse docs yet.
- Conflict: screenshot and reverse structure disagree.

Resolve easy conflicts by checking neighboring screenshots or docs. Leave unresolved conflicts in the gap list.

### 5. Write Interaction Nodes

Every meaningful interaction should be written in this shape:

```markdown
### 4.2 Tap shutter

- Status: Confirmed
- From: Camera sheet
- Trigger: User taps shutter
- Effect: Captures image, enters analyzing state
- Destination/state: Analysis in progress
- Route/API/event: POST /example or unknown
- Motion/feedback: sheet remains open; loading indicator appears
- Evidence: IMG_0012 -> IMG_0013; route AnalyzeView
- Notes: mark uncertain timing or missing error path
```

Prefer complete but compact nodes. Avoid writing vague nodes like "user can interact with page" without a specific trigger and result.

### 6. Organize by Product Modules

Use functional modules, not file order:

- Launch / onboarding.
- Authentication.
- Home / dashboard.
- Primary creation or capture flow.
- Review / edit / confirm.
- Detail pages.
- History / archive.
- Settings / account.
- System states and global behavior.
- Destructive or high-risk flows.

Rename modules to match the actual product. Never use "supplement" or "misc" as a final module name; split new evidence into the correct modules.

### 7. Preserve Confidence and Gaps

Use explicit labels:

- `Confirmed`: directly visible in screenshots or reproduced.
- `Inferred`: supported by route/source/API but not visually confirmed.
- `Unknown`: mentioned or implied but not enough evidence.
- `Conflict`: evidence disagrees.

Put missing screenshots in a prioritized capture list. Destructive actions, payments, account deletion, permission first-run states, and error states should usually be high priority.

### 8. Produce Deliverables

Default deliverables:

- `INTERACTIONS.md`: the authoritative text map.
- Coverage table by module.
- Main path walkthrough.
- Gap list with capture priority.
- Optional Figma-ready layout plan or direct Figma update when a file URL and MCP access are available.

Use `references/output-template.md` when creating the Markdown artifact.

## Figma Guidance

When Figma output is requested:

- Keep the main canvas as a module map.
- Group screenshots by functional module.
- Put interaction nodes beside the relevant screenshots.
- Add a separate timeline for dense motion/state machines.
- Add a separate "Needs capture" area for unknowns.
- Use confidence markers visibly.
- Verify that all screenshots are on-canvas, module titles are meaningful, and no temporary upload groups remain.

Do not create a visually pretty screenshot wall that loses trigger/effect information.

## Quality Bar

Before final response:

- Compare screenshot count against catalog count.
- Compare reverse route/page count against coverage buckets.
- Spot-check at least the main path and one branch path.
- If a visual canvas was created, inspect the canvas or screenshot preview for missing images, overlap, and incorrect module placement.
- State what was verified and any unresolved blockers.

## Common Mistakes

- Treating route names as confirmed UI.
- Treating screenshots as complete coverage.
- Grouping new screenshots under "supplement" instead of real modules.
- Omitting empty, loading, error, permission, and destructive states.
- Drawing only page-to-page arrows without saying what user action caused them.
- Hiding uncertainty instead of marking it.
