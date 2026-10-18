---
required-reading:
  - "[[dev-knw-code-loops]]"
  - "[[dev-knw-code-engineering]]"
orbh-sessions:
  - "[[d98d16ae-1388-4228-8610-6954998a395a]]"
---

# Code

Loop-based coding workflows over referenced codebases. The Code shard turns coding work into **loops, not stage-lists** — each unit of work runs *Plan → Search → Modify → Verify → Repair* until a verifiable stopping condition holds. The **codebase is the target; the Mesh is the output and the memory** between iterations.

## Doctrine

Four rules govern everything this shard does. They come from loop engineering (see [[dev-knw-code-loops]]):

1. **Loops, not stage-lists.** Author and run work as feedback loops with an explicit, *verifiable* stopping condition — never a one-shot generation.
2. **The verifier is never the implementer.** Whatever grades the work (a test suite, an eval, a separate review pass) is independent of whatever produced it. No agent grades its own homework.
3. **The Mesh is the memory.** State that must survive context loss between iterations lives in the artifact and the Mesh — not in a single context window. This is what lets a long mission resume cold.
4. **Compound on the way out.** Every loop that resolves writes its learning back into the Mesh so the next loop starts smarter ([[dev-sk-code-compound]]).

## The Pipeline

```
discuss requirements        create a unit of work          run the loop engine
wkfl-code-start_code   →     wkfl-code-create_task    →     wkfl-code-create_mission
   (Notepad)                 wkfl-code-do_task              wkfl-code-do_mission
                                  │                              │
                                  └────── sk-code-compound ──────┘
                                          wkfl-code-debug
```

- **Requirements** are discussed in a Notepad (this shard depends on Notepad). `wkfl-code-start_code` always starts a notepad.
- **Tasks** are thin code-specialised wrappers over the **Projects** shard — `wkfl-code-create_task` / `wkfl-code-do_task` call the Projects workflows and add the code layer (target repo, verifier, success criteria) plus the compound step.
- **Missions** are this shard's own artifact — a *really long-running task* authored as a complete loop specification, run by `wkfl-code-do_mission` (typically headless under Orbh).

## Missions Run in Phases

A mission does not hold all its work in one file — over a long run that file would bloat. Instead a mission is a thin, durable **orchestrator** that runs in **phases**, and the structure is **emergent**: you do not know the phases — or the coherent groups of work inside them — before the mission starts. They are discovered as the work unfolds, which is why everything here is created on demand and stays flexible.

Three levels of work:

| Level | What it is | Known upfront? |
|-------|-----------|----------------|
| **Mission** | The whole long-running goal | Yes — the durable spec |
| **Phase** | An emergent chunk / milestone of the mission. Contains **multiple** coherent groups of work — not one. | No — discovered as you go |
| **Coherent group of work** | The unit of a single loop iteration (the *Modify* step). Many happen within one phase. | No — emerges during a phase |

- The **Mission** holds the loop spec (goal, target repo/goal/environment, verifier, success criteria), tracks repos like a task (`git-repos`, plus OrbRepo-written `checkpointed` / `pr`), and lists its phases.
- A **Phase** (`[[dev-tmp-code-phase-v0.1]]`) is a mission derivative `(Mission) NNN Name . (Phase) M [Name]` with its **own short-term memory, state, iteration journal, and WIP commits**. Inside a phase, the loop runs many cycles — each cycle does one coherent group of work. A phase resumes cold from its own memory + journal.
- Phases are created **on demand** ([[dev-sk-code-add_phase]]) so a mission can **adapt**: a phase's scope is a rough milestone that may be refined as it runs, and a new phase is added when the next chunk of work comes into focus — never pre-planned in full at the start.

| Concern | Mission | Phase |
|---------|---------|-------|
| Holds | durable loop spec + phase list + repo/PR tracking | a chunk of the mission — many coherent groups of work |
| Memory | Result (synthesis across phases) | short-term memory + append-only journal |
| Commits | `git-repos`, final `pr` / `checkpointed` | `wip-commits` for its own work |
| Lifecycle | `drafting → running → succeeded/failed` | `pending → active → done` (`blocked`/`abandoned`) |

## Composition

| Concern | Owned by | This shard adds |
|---------|----------|-----------------|
| Requirements dialogue | Notepad (`ntpd`) | code-aware recon on start |
| Tasks | Projects (`proj`) | target repo, verifier, success criteria, compound-on-close |
| Missions (loop engine) | **Code (`code`)** | the `(Mission)` type + create/do mission loops |

## Mission Lifecycle

```
drafting → running → succeeded
              ↓
           blocked → running (resume)

Any status → failed (terminal — success criteria unreachable)
```

| Status | Meaning |
|--------|---------|
| `drafting` | The loop spec is being written; not yet started |
| `running` | The loop is executing — Plan → Modify → Verify → Repair |
| `blocked` | Paused for human input; the loop cannot proceed unattended |
| `succeeded` | The verifier confirmed the success criteria — terminal |
| `failed` | Success criteria judged unreachable — terminal |

## Rules

- Load this init before using the shard. Read the required-reading knowledge files first.
- A Mission is for work too large or too long for a single task. For a single bounded change, use a task (`wkfl-code-create_task` / `wkfl-code-do_task`).
- Missions run headless under Orbh where possible — in that mode, load the shard with `flint shard start code`, and follow the `> [!headless]` callouts of the `wkfl-*` workflows (see `# Headless` below).
- For now, the verifier and success criteria in a Mission are free **text** — a human reads them, or a separate verifier pass interprets them. They are not yet executable specs.

# Headless

A headless or subagent Orbh session has no person at the terminal. It loads this init with `flint shard start code`, as an interactive session does. Follow the `> [!headless]` callouts of the workflows.

The doctrine, the phases, and the mission lifecycle do not change. The difference is autonomy: a headless loop runs with no human checkpoints, and it reports through Orbh session keys and the iteration journal of each phase. The journal is the durable state: resume cold from it.

## Headless Operation

- Run [[dev-wkfl-code-do_mission]] and follow its `> [!headless]` callouts. They have no human gates, and they report progress with `flint orbh session set` keys.
- When a loop genuinely cannot proceed unattended, set the mission to `blocked`, journal the reason, set a session key that flags it for an operator, and stop. Do not guess past a real blocker.
- Tasks still delegate to the Projects shard. Use its workflows (`wkfl-proj-*`), and follow their `> [!headless]` callouts: Projects has one workflow for each mode.

## Orbh Interface Keys

Report progress with `flint orbh session set <key> <value>`. [[dev-wkfl-code-do_mission]] sets these keys:

| Key | Description | When to update |
|-----|-------------|----------------|
| `mission-status` | The status of the mission | At `running` (Stage 1), and at the final status (Stage 4) |
| `phase` | The current phase of the mission | After each cycle |
| `iteration` | The current cycle of the loop | After each cycle |
| `last-verifier-result` | The result of the last run of the Verifier | After each cycle |
| `blockers` (for example) | The blocker that an operator must resolve | When the mission is `blocked` |

### Phase Values

The `phase` key holds the current phase of the mission: the `(Phase)` derivative that runs now ([[dev-tmp-code-phase-v0.1]]). The phases emerge as the mission runs, so the values are not fixed.

## Result Delivery

Each turn ends with `flint orbh session return --finish "<result>"`. The result gives the mission, its status, the current phase, and the last verifier result. When the mission is `blocked`, the result gives the blocker and the question for the operator. A subagent puts a blocker and its question in the result.
