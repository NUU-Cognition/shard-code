---
description: "Run a Mission phase by phase — each phase runs its own loop with its own memory and journal, new phases are added on demand, until the verifier confirms the mission's success criteria"
orbh-sessions:
  - "[[d98d16ae-1388-4228-8610-6954998a395a]]"
orb:
  - "@v1/nuucognition/session/9f552ce0-0455-44ed-b8ec-d749c3ae9b2f#flint/nuu-orbh"
---

> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

Run `flint shard start code` if you haven't already.

# Workflow: Do Mission

Execute a Mission until its success criteria hold. This is the **loop engine**. A mission runs in **phases**: each phase is an emergent chunk of the mission — a milestone holding *multiple* coherent groups of work — with its own short-term memory, state, and iteration journal ([[dev-tmp-code-phase-v0.1]]). Phases keep the mission file small over a long run and let the mission adapt. Crucially, the phases (and the groups of work inside them) are **not known upfront** — they emerge as the mission runs, so scope each phase only when it comes into focus and refine it as you go.

For unattended execution under Orbh, run this workflow in a headless Orbh session, and follow the `> [!headless]` callouts.

> [!headless]
> In a headless or subagent Orbh session, no person is at the terminal. The mission runs as an unattended, phase-based loop with no human checkpoints. Do each stage, and follow the `> [!headless]` callout in it.
> - Report progress with Orbh session keys and with the journal of each phase, in place of a person. The keys are in the section `# Headless` of [[dev-init-code]].
> - End the turn with `flint orbh session return --finish "<result>"`.

# Input

- An existing `(Mission)` (from [[dev-wkfl-code-create_mission]])

> [!headless]
> - The Orbh session that runs the mission.

# Actions

## Stage 1: Load the Spec

- Read the mission fully: Goal, Target Repo, Target Goal, Target Environment, Verifier, Success Criteria, and its Phases list.
- Identify the current phase: the first phase not yet `done`. If there are no phases yet, create the first one with [[dev-sk-code-add_phase]] (scope it to the first chunk / milestone you can see toward the goal — not the whole mission, not a single change).
- **Resume cold from the current phase's Short-Term Memory and Iteration Journal** — these are the memory; trust them over assumptions about prior state.
- Confirm the target environment is reachable and the verifier command(s) run. Branch-guard the repo before editing (never edit `dev`/`main` directly).
- Set the mission status to `running`. Stamp your session in `orb:`: run `flint address me`, and append its `by` address (quoted) to `orb:`. Add nothing only when `orb:` or `orbh-sessions` has an item that is exactly your `by` address, the short form `@v1/<org>/session/<uuid>`, `[[<uuid>]]`, or your bare `<uuid>`. Old notes keep `orbh-sessions`: never remove it, and add no new item to it. The full rule is in [[knw-f-artifacts]] § Session Tracking.
- Once loaded and the environment verifies clean, progress to the next stage.

> [!headless]
> After you set the mission status to `running` and stamp your session in `orb:`, set a session key: `flint orbh session set mission-status running`.

## Stage 2: Run the Current Phase

Set the phase to `active`, then repeat this loop within the phase until the phase's goal is delivered:

1. **Plan** — the next step toward the phase goal.
2. **Search** — locate the relevant files and conventions.
3. **Modify** — do **a coherent group of work**. A mission is not chipping away one line at a time — make a meaningful, self-consistent set of changes that moves the phase forward.
4. **Verify** — run the mission's **Verifier**. It is independent of this loop's reasoning — trust its output, not your intention.
5. **Repair** — read the verifier output and fix what failed. If stuck on the same failure across iterations, run [[dev-wkfl-code-debug]].
6. **Record** — append a cycle entry to the phase's Iteration Journal, refresh its Short-Term Memory, and commit repo work as WIP commits (record SHAs in the phase's `wip-commits`).

When the phase goal is delivered and verified, set the phase to `done`, write its Phase Result, and progress to the next stage.

> [!headless]
> Run the loop unattended: no person reviews a cycle.
> - Run the mission's **Verifier** every cycle, and trust its output.
> - After each cycle, report progress with session keys, for example `flint orbh session set phase "<phase>"`, `flint orbh session set iteration <n>`, and `flint orbh session set last-verifier-result "<result>"`.

## Stage 3: Advance or Adapt

- If the mission's **Success Criteria** now hold, progress to Close.
- Otherwise decide the next phase — its shape emerges now that the previous phase is done:
  - If the plan still fits, scope the next chunk / milestone that has come into focus and create it with [[dev-sk-code-add_phase]], then return to Stage 2.
  - If the plan needs to change (new direction, discovered constraint), **adapt**: add a new phase that reflects the new plan via [[dev-sk-code-add_phase]], note why in the journal, and return to Stage 2.
- Blocking: if work cannot proceed without human input, set the mission to `blocked`, journal the reason, and present the blocker. This interactive variant pauses at this **human checkpoint** — confirm with the user before continuing or closing. On resolution, return to `running`.

> [!headless]
> There is no human checkpoint. Do not wait for a person to confirm before you continue or close: when the Success Criteria hold, go to Close; else add the next phase with [[dev-sk-code-add_phase]], note why in the journal, and return to Stage 2.
> - If the loop genuinely cannot proceed unattended, set the mission to `blocked`, journal the reason, set a session key that flags the blocker for an operator (for example `flint orbh session set blockers "<the blocker>"`), and stop. Do not guess past a real blocker.
> - To stop, end the turn with `flint orbh session return --finish "<result>"`. The result names the mission, the current phase, and the blocker.

## Stage 4: Close & Compound

- Set the mission status to `succeeded` (or `failed` if the criteria are judged unreachable) and write the **Result** section — the synthesis across phases, the final verifier verdict, and the PR.
- Run [[dev-sk-code-compound]] to persist the mission's learnings into the Mesh.

> [!headless]
> - After you write the **Result** section, set a final session key, for example `flint orbh session set mission-status succeeded`.
> - After [[dev-sk-code-compound]], end the turn with `flint orbh session return --finish "<result>"`. The result gives the status of the mission, the final verifier verdict, and the PR.

# Output

- A `(Mission)` in `succeeded` or `failed` status, with completed phase derivatives each holding their own journal
- Learnings compounded into the Mesh

> [!headless]
> - The mission can also end in `blocked` status, when the loop cannot proceed unattended.
> - The progress and the final state are in the Orbh session keys.
