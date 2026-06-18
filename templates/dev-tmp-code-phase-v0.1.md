---
description: "Phase — a chunk of a mission with its own short-term memory, state, and iteration journal; created on demand so a mission can adapt"
---

# Filename: Mesh/Types/Missions/(Mission) XXX [Mission Name] . (Phase) M [Phase Name].md

/* M is the phase number within the mission (1, 2, 3 ...) — local to the mission, not global.
   The file is a derivative of the mission, so it lives in the same folder and carries the
   mission's full name before the " . (Phase) M " segment. */

```markdown
---
id: [generate-uuid4]
tags:
  - "#code/phase"
status: [pending|active|blocked|done|abandoned]
mission: "[[(Mission) XXX [Mission Name]]]" /* the parent mission */
phase-number: [M] /* this phase's position within the mission */
git-repos: /* inherited from the mission — the repo(s) this phase edits */
  - "[[rf-cb-example]]"
  - (continued)
wip-commits: /* append SHA after each WIP commit made during this phase. Annotate with repo name if multiple: "a1b2c3d (rf-cb-flint)". */
orbh-sessions:
  - "[[session-id]]"
  - (continued)
template: "[[tmp-code-phase-v0.1]]"
authors: /* from .flint/identity.json; omit if no identity set */
  - "[[@Person Name]]"
---

# Phase Goal

[The chunk / milestone of the mission this phase delivers — typically several coherent groups of work, not the whole mission and not a single change. State the rough scope; it may be refined as the phase runs (the work is emergent). Note what is explicitly deferred to a later phase.]

# Short-Term Memory

/* The phase's working state — the scratchpad an agent needs to resume THIS phase cold.
   Current focus, open threads, decisions made, files in flight, what to do next.
   Overwrite freely as the phase progresses; this is mutable working memory, not a log. */

[current working state for this phase]

# Iteration Journal

/* Append-only log of this phase's loop cycles (Plan → Modify → Verify → Repair).
   One entry per cycle: what was planned, what changed, what the verifier reported.
   Never edit previous entries. This is the durable record; Short-Term Memory is the live scratchpad. */

- YYYY-MM-DD: [iteration entry — plan → change → verifier result]
- (continued)

# Phase Result

/* Written when the phase reaches done or abandoned. What this phase accomplished,
   the verifier verdict for its scope, commits made, and what the next phase should pick up. */

[phase outcome summary]
```
