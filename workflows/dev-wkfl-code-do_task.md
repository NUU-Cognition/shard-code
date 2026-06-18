---
description: "Execute a code task as a verify loop — wraps the Projects do-task workflow, runs Plan→Modify→Verify→Repair, and compounds the learning on close"
---

> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

Run `flint shard start code` if you haven't already.

# Workflow: Do Task

Work an existing code task to completion as a feedback loop. This is a **thin wrapper** over the Projects shard's do-task workflow — it delegates the task lifecycle and adds the loop discipline and the compound step.

# Input

- An existing `(Task)` (often from [[dev-wkfl-code-create_task]])
- (Optional) Aiding context on how to complete it

# Actions

## Stage 1: Execute as a Loop

- Ensure the Projects shard is loaded, then run [[wkfl-proj-do_task]] to drive the task through its lifecycle (`in-progress → review → done`), including its WIP-commit convention for `git-repos`.
- While working, run the core loop from [[dev-knw-code-loops]] rather than one-shotting: **Plan → Search → Modify → Verify → Repair**.
  - **Verify** with the task's stated verifier (its test/lint/typecheck commands) after each coherent change — do not declare done until the success criteria hold.
  - If verification keeps failing on the same point, hand off to [[dev-wkfl-code-debug]].
- Tick checkboxes as requirements are met and keep the Task Log current.
- Once the success criteria hold and the task reaches review/done in Projects, progress to the next stage.

## Stage 2: Compound

- Run [[dev-sk-code-compound]] to distil what was learned (a non-obvious fix, a convention discovered, a gotcha) into the Mesh so the next loop starts smarter.
- This is the doctrine's "compound on the way out" step — do not skip it.

# Output

- A completed `(Task)` (per Projects' lifecycle)
- A learning persisted to the Mesh via the compound step
