# Code

Loop-based coding workflows over referenced codebases — code requirements, tasks, and long-running missions, with learnings compounded into the Mesh.

Built on **loop engineering**: coding work runs as feedback loops (*Plan → Search → Modify → Verify → Repair*) to a verifiable stopping condition. The codebase is the target; the Mesh is the output and the memory.

## Pipeline

```
discuss requirements        create a unit of work          run the loop engine
wkfl-code-start_code   →     wkfl-code-create_task    →     wkfl-code-create_mission
   (Notepad)                 wkfl-code-do_task              wkfl-code-do_mission
                                  │                              │
                                  └────── sk-code-compound ──────┘
                                          wkfl-code-debug
```

## Composition

- **Notepad** (`ntpd`) — requirements dialogue. `wkfl-code-start_code` always opens a notepad with code-aware recon.
- **Projects** (`proj`) — tasks. `create_task` / `do_task` are thin wrappers that add target repo, verifier, success criteria, and the compound step.
- **Code** (`code`) — owns the `(Mission)` and `(Phase)` types. A mission is a thin, durable loop spec (goal, target repo, environment, verifier, success criteria) that tracks repos like a task and runs in **phases**. Each `(Phase)` is a mission derivative with its own short-term memory, state, journal, and WIP commits — created on demand so the mission can adapt. Run by `do_mission` (headless under Orbh via the `hwkfl` variant).

## Capabilities

| Kind | File | Purpose |
|------|------|---------|
| Workflow | `wkfl-code-start_code` | Code-requirements notepad |
| Workflow | `wkfl-code-create_task` | Create an implementable code task (wraps Projects) |
| Workflow | `wkfl-code-do_task` | Execute a code task as a verify loop (wraps Projects) |
| Workflow | `wkfl-code-create_mission` | Author a Mission loop spec |
| Workflow | `wkfl-code-do_mission` / `hwkfl-code-do_mission` | Run the mission loop, phase by phase |
| Workflow | `wkfl-code-debug` | Debug sub-loop |
| Skill | `sk-code-add_phase` | Add a phase to a mission on demand (adapt) |
| Skill | `sk-code-compound` | Persist a learning into the Mesh |
| Template | `tmp-code-mission-v0.1` | Mission artifact (orchestrator) |
| Template | `tmp-code-phase-v0.1` | Phase artifact (work chunk w/ own memory + journal) |
| Knowledge | `knw-code-loops` | Loop-engineering doctrine |
| Knowledge | `knw-code-engineering` | General engineering knowledge |
| Type | `Mission` | Long-running coding loop |
| Type | `Phase` | A chunk of a mission |

## Structure

```
Shards/(Dev Local) Code/
  shard.yaml                    # Manifest (not prefixed)
  dev-init-code.md              # Init — shard context + doctrine
  dev-hinit-code.md             # Headless init
  skills/                       # dev-sk-code-{name}.md
  workflows/                    # dev-wkfl-code-{name}.md, dev-hwkfl-code-{name}.md
  templates/                    # dev-tmp-code-{name}-v<X.Y>.md
  knowledge/                    # dev-knw-code-{name}.md
  install/                      # type-code-{name}.md (NOT prefixed)
```
