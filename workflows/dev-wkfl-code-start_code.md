---
description: "Start a code-requirements notepad — code-aware recon, then a requirements-first brainstorm that converges on a task or mission"
---

> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

Run `flint shard start code` if you haven't already.

# Workflow: Start Code

Begin discussing **code requirements** in a Notepad. This is a code-specialised front-end over the Notepad shard's start workflow: it always opens a notepad, gathers code-aware context first, and steers the conversation toward *what to build and how we'll know it's done*.

# Input

- Topic / feature idea for the code work
- (Optional) Target repo (codebase reference or path)
- (Optional) Initial message or constraints

# Actions

## Stage 1: Open the Notepad

- Run the Notepad shard's start workflow ([[wkfl-ntpd-start]]) to create a new `(Notepad)` for this topic. Ensure the Notepad shard is loaded first.
- This workflow **always** starts a notepad — requirements discussion is the point. (If the user already knows exactly what to build, they should skip straight to [[dev-wkfl-code-create_task]] instead of running this.)
- Once the notepad exists, progress to the next stage.

## Stage 2: Code-Aware Recon

- If a target repo is known, gather context before the first response (the loop's recon step — see [[dev-knw-code-engineering]] § Recon Before Judging):
  - Languages, frameworks, package manager.
  - The exact **build / test / lint / typecheck** commands (these become the verifier later).
  - Conventions, and any `README` / `AGENTS.md` / `CLAUDE.md` / ADRs / design docs.
- Search the Mesh for related notepads, tasks, missions, and concepts.
- Fold the findings into the opening response so the discussion starts grounded.
- Once recon is synthesised, progress to the next stage.

## Stage 3: Requirements Dialogue

- Drive the conversation toward requirements, not open chat: what to build, constraints, and the **definition of done** (these become success criteria later).
- Grill where the requirement is vague (see [[dev-knw-code-engineering]]). Surface ambiguities and resolve them with the user.
- This is a **human checkpoint loop** — continue the notepad with the user via [[wkfl-ntpd-continue]] until requirements are sharp.
- Once the user confirms the requirements are sharp enough to act on, progress to the next stage.

## Stage 4: Hand Off

- Offer the exit ramp based on scope:
  - Single bounded change → [[dev-wkfl-code-create_task]] (or [[wkfl-proj-create_and_do_task]] to create and execute at once).
  - Large / long-running work → [[dev-wkfl-code-create_mission]].
- Capture the agreed requirements so the downstream task or mission can reference this notepad.

# Output

- A `(Notepad)` with code-aware context and sharpened requirements
- A clear hand-off to a task or mission
