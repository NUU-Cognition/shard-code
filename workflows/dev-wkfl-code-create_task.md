---
description: "Create an implementable code task — wraps the Projects create-task workflow and adds the code loop layer (target repo, verifier, success criteria)"
---

> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

Run `flint shard start code` if you haven't already.

# Workflow: Create Task

Spec a single, bounded code task to be implemented later. This is a **thin wrapper** over the Projects shard's create-task workflow — it does not reinvent the task lifecycle; it delegates and adds the code loop layer.

# Input

- Context of the code task (often a `(Notepad)` from [[dev-wkfl-code-start_code]])
- (Optional) Target repo

# Actions

## Stage 1: Delegate to Projects

- Ensure the Projects shard is loaded, then run [[wkfl-proj-create_task]] to create the `(Task)` with its full lifecycle, requirements, and definition-of-done. Do not duplicate the Projects task machinery.
- Once the task exists, progress to the next stage.

## Stage 2: Add the Code Layer

On the created task, fill in the code-specific fields so it is ready for a loop to execute:

- **`git-repos`** — set to the target repo (codebase reference wikilink or plain name). This drives WIP commits during execution.
- **Verifier** — in the task's Notes (or Definition of Done), state *how the work will be checked* independent of whoever implements it: the test/lint/typecheck commands, or a review pass.
- **Success criteria** — make the Definition of Done a *verifiable stopping condition* (binary, checkable) per [[dev-knw-code-loops]]. Sharpen any vague criterion now.
- Link back to the originating notepad in Related Documents.
- This is the **human checkpoint**: present the augmented task and confirm the verifier and success criteria are right.
- Once the user confirms, progress to the next stage.

## Stage 3: Finalise

- Leave the task in `todo` (Projects' create-task default) — execution happens via [[dev-wkfl-code-do_task]] or [[wkfl-proj-do_task]].
- Confirm the task is ready to work on.

# Output

- A `(Task)` in `todo` status with target repo, verifier, and verifiable success criteria
