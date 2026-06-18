---
description: "Add a new phase to a mission on demand — create the phase derivative, link it back, and register it in the mission so the mission can adapt"
---

> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

Run `flint shard start code` if you haven't already.

# Skill: Add Phase

Create a new phase for a mission. This is how a mission **adapts**: when the next chunk of work comes into focus, or the plan shifts, add a phase rather than overloading an existing one or rewriting the mission. Phases are emergent — you scope them when they become clear, not all at the start.

# Input

- The parent `(Mission)`
- The rough scope of the new phase — a chunk / milestone of the mission (several coherent groups of work), not a single change. It may be refined as the phase runs.

# Actions

1. **Determine the phase number.** Count the mission's existing phases (its `phases` frontmatter / Phases section) and use the next integer, M. Phase numbers are local to the mission (1, 2, 3 …), not global.
2. **Create the phase** as a mission derivative using [[dev-tmp-code-phase-v0.1]]:
   - Filename: `Mesh/Types/Missions/(Mission) NNN [Mission Name] . (Phase) M [Phase Name].md`
   - Set `status: pending`, `mission` to the parent wikilink, `phase-number: M`.
   - Copy `git-repos` from the mission so the phase edits the same repo(s).
   - Write the **Phase Goal** (the chunk this phase delivers — a rough milestone, several coherent groups of work — and what it defers). Keep it flexible; it can be refined as the phase runs.
   - Leave Short-Term Memory, Iteration Journal, and Phase Result empty — they fill in during execution.
3. **Register it on the mission:**
   - Append the phase wikilink to the mission's `phases` frontmatter list.
   - Add it to the mission's `# Phases` section with its status.
4. **Add an execution-log note** if the mission is mid-run: record in the active phase's journal (or the mission Result if between phases) that a new phase was created and why (the adaptation).

# Output

- A new `(Phase)` derivative in `pending` status, linked to its mission
- The mission's `phases` list and Phases section updated
