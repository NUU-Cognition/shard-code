---
id: 3f9a2c7e-8b1d-4e6a-9c4f-7d2e5a8b1f3c
tags:
  - "#f/metadata"
  - "#f/type"
---

# Mission

A mission is a single, extremely long-running unit of coding work expressed as a complete *loop specification* — everything an autonomous agent loop needs to run unattended toward a goal and know when it is done. Unlike a Task, which is one bounded change worked to completion in a session, a Mission carries a goal, a target repository and environment, an independent verifier, and explicit success criteria, plus an append-only iteration journal that serves as the loop's durable memory across context resets. Reach for a Mission when the work is too large or too long-lived to hold in one session and must survive being resumed cold; reach for a Task when a single agent can finish the change in one pass.
