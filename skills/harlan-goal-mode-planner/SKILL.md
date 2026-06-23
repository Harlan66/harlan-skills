---
name: harlan-goal-mode-planner
description: Use when helping a user design, diagnose, rewrite, or refine a Codex Goal Mode goal, especially when converting vague intentions into executable long-running goals or improving an existing Goal with boundaries, stages, status tracking, acceptance criteria, and stop conditions.
---

# Goal Mode Planner

## Purpose

Use this skill to turn a user's intention into a Goal Mode goal that can be executed continuously without drifting, looping, or making unsupported judgments.

The core rule: a good Goal is not only a target. It must define scope, boundaries, stages, status tracking, acceptance criteria, and stop conditions.

## First Decision

Choose one path before producing output:

- Existing Goal provided: diagnose and revise it.
- Vague intention provided: guide the user from ambiguity to an executable Goal.
- Concept discussion only: explain Goal Mode briefly, then ask whether the user wants diagnosis or creation.

Do not jump directly to a polished Goal when essential information is missing. Ask targeted questions first.

## Path A: Diagnose And Revise Existing Goal

Use when the user provides a draft Goal, prompt, task description, or screenshot of a Goal.

### Process

1. Restate the intended outcome in one or two sentences.
2. Diagnose problems before rewriting.
3. Give concrete adjustment advice.
4. Produce an improved Goal only after the diagnosis is clear.

### Diagnostic Checklist

Check whether the current Goal:

- is too broad or mixes several projects;
- lacks stages or milestones;
- lacks input materials or data sources;
- lacks concrete deliverables;
- lacks status tracking;
- lacks acceptance criteria;
- lacks stop conditions;
- lets AI make final judgments about aesthetics, trust, strategy, taste, causality, or business tradeoffs;
- invites infinite optimization, repeated replanning, or returning to earlier stages;
- fails to say what not to do.

### Revision Output

Use this structure:

```markdown
## Diagnosis

- Main issue:
- Why it matters:
- Suggested adjustment:

## Revised Goal

### Background

### Final Objective

### Current Stage

### Available Inputs

### Scope

### Out Of Scope

### Stage Plan

### Status Table

Track:
- stage
- completed work
- current work
- next step
- blocker
- user decision needed

### Deliverables

### Acceptance Criteria

### Stop Conditions

### Human Decision Points
```

Keep the revised Goal direct and operational. Do not make it sound like a mission statement.

## Path B: Build A Goal From A Vague Intention

Use when the user says something like "I want to do X", "help me plan Y", or gives a rough direction without a finished Goal.

### Guided Questions

Ask only the questions needed for the next step. Prefer batches of 3 to 6 questions.

Cover these areas:

1. Objective: What should be true when this is done?
2. Background: Why do this now? What triggered the task?
3. Inputs: What materials, files, links, data, or examples are available?
4. Scope: What should the Agent do?
5. Boundaries: What should the Agent not do?
6. Human judgment: Which decisions require the user?
7. Stages: What are the natural phases?
8. Deliverables: What should each phase produce?
9. Acceptance: How will the user judge whether it is good enough?
10. Stop: When should the Agent stop instead of continuing to optimize?

If the user cannot answer everything, create a draft with explicit assumptions and mark unresolved decisions as "needs user confirmation".

### Creation Output

After enough information is available, produce:

```markdown
# Goal

## Background

## Objective

## Inputs

## Scope

## Out Of Scope

## Stage Plan

1. Stage:
   - task:
   - output:
   - acceptance:

## Status Table Requirement

Maintain a status table with:
- stage
- done
- doing
- next
- blocker
- needs user decision

## Acceptance Criteria

## Stop Conditions

## Human Decision Points
```

## Core Principles

- Goal Mode is for sustained execution, not one-turn answering.
- A Goal must define how progress will be judged after each stage.
- Long tasks need stages and milestones.
- Status tables are mandatory for multi-stage work.
- Stop conditions prevent endless polishing and replanning.
- AI can organize, compare, draft, summarize, calculate, inspect, and suggest.
- The user should own final judgment for aesthetics, trust, brand direction, strategy, causality, and major tradeoffs.
- If a task requires taste or business judgment, ask the Agent to surface options and evidence, not make the final call alone.

## Common Fixes

Use these transformations:

- "帮我长期经营账号" -> "先基于现有数据完成账号经营现状分析，暂不做审美和信任判断。"
- "优化这个项目" -> "列出当前问题，按影响排序，先修前三个可验证问题。"
- "一直改到最好" -> "完成验收标准后停止，并列出可选后续优化，不自动继续。"
- "帮我做判断" -> "整理证据、给出候选判断，并标记需要用户确认的地方。"

## Warnings

Avoid Goals that ask the Agent to:

- pursue "best", "ultimate", or "perfect" without a stop condition;
- keep iterating until no improvements remain;
- repeatedly replan after each phase;
- decide subjective quality without user criteria;
- silently expand scope;
- replace user judgment in high-context decisions.

When these appear, rewrite them into bounded tasks with stage outputs and explicit user checkpoints.
