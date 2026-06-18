---
description: "Headless phase-based mission loop — runs a Mission unattended under Orbh, one phase at a time with its own memory and journal, adding phases on demand, reporting via session keys"
---

> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

Run `flint shard hstart code` if you haven't already.

# Workflow: Do Mission (Headless)

Run a Mission as an unattended, phase-based loop under Orbh. Same engine as [[dev-wkfl-code-do_mission]], with no human checkpoints — progress is reported via Orbh session keys and the per-phase journals instead.

# Input

- An existing `(Mission)` to run
- The Orbh session driving it

# Actions

## Stage 1: Load the Spec

- Read the mission fully and identify the current phase (first not `done`). If none exist, create the first with [[dev-sk-code-add_phase]] — scope it to the first chunk / milestone you can see (phases are emergent, not pre-planned).
- **Resume cold from the current phase's Short-Term Memory and Iteration Journal** — they are the durable memory.
- Verify the target environment and verifier command(s) run; branch-guard the repo.
- Set mission status to `running`, append the session to `orbh-sessions`, and set a session key (e.g. `flint orbh session set mission-status running`).

## Stage 2: Run the Current Phase (unattended)

Set the phase to `active` and loop until its goal is delivered:

1. **Plan → Search → Modify → Verify → Repair.** At **Modify**, do **a coherent group of work** — a meaningful, self-consistent set of changes, not one-line chipping.
2. Run the mission's **Verifier** every cycle; trust its output.
3. Append a cycle entry to the phase's Iteration Journal, refresh its Short-Term Memory, and WIP-commit repo work (record SHAs in the phase's `wip-commits`).
4. Report progress via session keys after each cycle (e.g. `phase`, `iteration`, `last-verifier-result`).
5. If stuck on a repeated failure, run [[dev-wkfl-code-debug]].

When the phase goal is delivered and verified, set the phase `done`, write its Phase Result, and progress.

## Stage 3: Advance or Adapt (unattended)

- If the mission's **Success Criteria** hold, progress to Close.
- Otherwise add the next phase with [[dev-sk-code-add_phase]] — the next chunk / milestone that has come into focus, or an adapted plan if a constraint emerged — note why in the journal, and return to Stage 2.
- If the loop genuinely cannot proceed unattended, set the mission to `blocked`, journal the reason, set a session key flagging it for an operator, and stop.

## Stage 4: Close & Compound

- Set mission status to `succeeded` (or `failed`), write the **Result** section, and set a final session key.
- Run [[dev-sk-code-compound]] to persist learnings into the Mesh.

# Output

- A `(Mission)` in `succeeded`, `failed`, or `blocked` status, with completed phase derivatives
- Progress and final state reported via Orbh session keys
- Learnings compounded into the Mesh
