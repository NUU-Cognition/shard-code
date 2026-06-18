---
required-reading:
  - "[[dev-knw-code-loops]]"
  - "[[dev-knw-code-engineering]]"
---

# Code (Headless)

Headless entry point for the Code shard, loaded in Orbh sessions. Same doctrine as the interactive init ([[dev-init-code]]) — the difference is autonomy: headless loops run without human checkpoints and report via Orbh session keys and the mission iteration journal.

## Doctrine (unchanged)

1. **Loops, not stage-lists** — run Plan → Search → Modify → Verify → Repair to a verifiable stopping condition.
2. **The verifier is never the implementer.**
3. **The Mesh is the memory** — the mission iteration journal is the durable state; resume cold from it.
4. **Compound on the way out** — persist learnings via [[dev-sk-code-compound]].

## Headless Operation

- Prefer the headless workflow [[dev-hwkfl-code-do_mission]] over its interactive counterpart — it has no human gates and reports progress via `flint orbh session set` keys.
- When a loop genuinely cannot proceed unattended, set the mission to `blocked`, journal the reason, set a session key flagging it for an operator, and stop — do not guess past a real blocker.
- Tasks still delegate to the Projects shard; use its headless variants (`hwkfl-proj-*`) where available.

## Mission Lifecycle

```
drafting → running → succeeded
              ↓
           blocked → running (resume)

Any status → failed (terminal)
```
