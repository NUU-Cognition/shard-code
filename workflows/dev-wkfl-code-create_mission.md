---
description: "Author a Mission — a long-running coding loop spec with goal, target repo, environment, verifier, and success criteria"
---

> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

Run `flint shard start code` if you haven't already.

# Workflow: Create Mission

Write a **Mission** — a really long-running coding task expressed as a complete loop specification. A mission is for work too large or too long-lived to finish in one session; everything a loop needs to run unattended and know when it is done goes in the artifact.

# Input

- The goal (or an existing `(Task)` to attach) and any context
- Target repo
- (Optional) Target environment, verifier, and success-criteria details

# Actions

## Stage 1: Draft the Loop Spec

- Get the next number: `flint helper type newnumber Mission`.
- Create the mission at `Mesh/Types/Missions/(Mission) NNN [Name].md` using [[dev-tmp-code-mission-v0.1]].
- Set status to `drafting`.
- Fill every section — these ARE the loop spec (see [[dev-knw-code-loops]]):
  - **Goal** — what to achieve and why; link the attached `(Task)` if there is one.
  - **Target Repo** — the codebase reference or path.
  - **Target Goal** — the concrete end-state in that repo.
  - **Target Environment** — where it runs/verifies, plus the exact build/test/lint/typecheck commands.
  - **Verifier** — who/what checks the work, independent of the implementer (free text for now).
  - **Success Criteria** — the verifiable stopping condition for the whole mission, binary and checkable (free text for now).
  - **Set `git-repos`** to the target repo(s) — a mission tracks repos like a task does (WIP commits land on its phases; the final PR/checkpoint on the mission).
- Leave the Phases list empty — do **not** try to pre-plan the phases. They are emergent: the work breaks into phases (and coherent groups of work within them) only as the mission runs. The first phase is created when the mission starts, or seeded in Stage 3.
- Once the draft is complete, progress to the next stage.

## Stage 2: Sharpen with the User

- Present the mission. The most important review: **is the success criteria actually verifiable, and is the verifier independent of whoever runs the loop?**
- Resolve any vague goal or unverifiable criterion now — a mission that cannot be checked cannot end.
- This is the human checkpoint. Once the user confirms the spec, progress to the next stage.

## Stage 3: Finalise

- Optionally seed the first phase now with [[dev-sk-code-add_phase]] (scope it to the first chunk / milestone you can see — not the whole mission). Otherwise the do-mission loop creates it on start. Only the first phase, not a full phase plan.
- Leave status as `drafting` (run it later via [[dev-wkfl-code-do_mission]]), or set `running` and populate `orbh-sessions` if a loop is starting immediately.
- Confirm the mission is ready.

# Output

- A `(Mission) NNN` artifact in `Mesh/Types/Missions/` with a complete, verifiable loop spec
- Optionally a seeded first `(Phase)`
