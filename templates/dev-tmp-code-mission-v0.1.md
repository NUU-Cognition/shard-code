---
description: "Mission — a long-running coding loop spec: goal, target repo, environment, verifier, success criteria, OrbRepo tracking, and a list of phases"
---

# Filename: Mesh/Types/Missions/(Mission) XXX [Mission Name].md

/* XXX is a 3-digit number. Get it with: flint helper type newnumber Mission */

```markdown
---
id: [generate-uuid4]
tags:
  - "#code/mission"
status: [drafting|running|blocked|succeeded|failed]
task: /* optional — wikilink to a (Task) this mission's goal is attached to; leave blank if the goal is stated inline */
phases: /* wikilinks to this mission's phase derivatives, in order — appended on demand as phases are created */
  - "[[(Mission) XXX Name . (Phase) 1 ...]]"
  - (continued)
git-repos: /* the repo(s) this mission edits — codebase reference wikilinks (e.g. "[[rf-cb-flint]]") or plain names. Drives WIP commits in phases. */
  - "[[rf-cb-example]]"
  - (continued)
checkpointed: /* do not set — written by the OrbRepo checkpoint agent with checkpoint commit SHA(s) */
pr: /* do not set — written by the OrbRepo close agent with the PR reference */
orbh-sessions: /* every orbh session that runs this mission — append as the loop runs */
  - "[[session-id]]"
  - (continued)
template: "[[tmp-code-mission-v0.1]]"
authors: /* from .flint/identity.json; omit if no identity set */
  - "[[@Person Name]]"
---

# Goal

[What this mission must achieve, and why. If a (Task) is attached, summarise it here and link it. Include any additional context the loop needs to start — this is the brief an agent reads cold.]

# Target Repo

[The codebase the loop operates on — matches `git-repos` above. Codebase reference wikilink or plain name/path.]

# Target Goal

[The concrete end-state in that repo. What does the repository look like when this is done?]

# Target Environment

[Where the loop runs and verifies — the harness, the runtime, required services, dependencies, and the exact build/test/lint/typecheck commands the verify step uses.]

# Verifier

[Who or what checks the work — independent of whatever runs the loop. A test suite, a command, an eval, a separate review pass, or a human. For now this is free text. Per doctrine: the verifier is never the implementer.]

# Success Criteria

[The verifiable stopping condition for the WHOLE mission — binary and checkable. The mission succeeds when this holds. For now this is free text.]

# Phases

/* A mission runs in phases. Each phase is its own derivative artifact (its own short-term
   memory, state, and iteration journal) holding MULTIPLE coherent groups of work — this
   keeps the mission file small over a long run. Phases are EMERGENT: do not pre-plan them.
   They appear on demand (via sk-code-add_phase) as the work breaks into chunks, so the
   mission can adapt. List them here in order as wikilinks with their status as they are
   created, and keep `phases` frontmatter in sync. */

1. [[(Mission) XXX Name . (Phase) 1 [Name]]] — `[status]`
2. (continued)

# Result

/* Written when the mission reaches succeeded or failed. What was accomplished, the final
   verifier verdict, the PR, artifacts produced, and any follow-ups. The per-phase journals
   hold the detail; this is the synthesis. */

[mission outcome summary]
```
