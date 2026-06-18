---
description: "Persist a coding learning into the Mesh so the next loop starts smarter — distil a fix, convention, or gotcha into a record or concept note"
---

> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

Run `flint shard start code` if you haven't already.

# Skill: Compound

Capture what a coding loop learned and write it into the Mesh. This is the doctrine's "compound on the way out" step ([[dev-knw-code-loops]]) — the persistence move that turns one-off work into accumulating knowledge and is the Flint's answer to loop engineering's external-memory requirement.

# Input

- A resolved task, mission, or debug loop
- The learning worth keeping (a non-obvious fix, a discovered convention, a gotcha, a reusable pattern)

# Actions

1. **Decide if there is a real learning.** Compound only durable, reusable knowledge — not routine work. If nothing generalises beyond this one change, skip and say so.
2. **Pick the form:**
   - A **record note** (`#note/record`, [[tmp-f-record]]) for a fact, gotcha, or observation (e.g. "Repo X's test suite needs `DATABASE_URL` set or auth tests hang").
   - A **concept note** (`#note/concept`, [[tmp-f-concept]]) for a reusable idea or pattern worth linking densely.
   - If the learning sharpens a target repo's domain model, prefer updating an existing note over creating a duplicate.
3. **Write it standalone.** The note must make sense to a future loop with zero context from this session — state the situation, the learning, and when it applies. Link the source task/mission.
4. **Place it** in `Mesh/Notes/` with the right tag, and add `authors` from `.flint/identity.json` (omit if no identity).
5. **Link back:** add the new note to the source task/mission's Related Documents (and `artifacts-created` on a task, if present).

# Output

- A record or concept note in the Mesh capturing the learning
- The source artifact linked to it
