# REQ-01 — Analyze a story for missing information

| | |
|---|---|
| **Area** | Requirements & Story Quality |
| **Status** | 🟡 **Unverified starting point** — not yet proven on real work |
| **Owner** | Shyam Ram |
| **Last validated** | — |
| **Proven on** | Not yet. Be the first — see [How to verify](../README.md#how-to-verify-a-recipe). |

---

## When to use this

During grooming or before picking up a story, when you suspect it is not actually ready
to build. Surfaces ambiguities, unstated assumptions, and missing acceptance criteria
*before* they become mid-sprint clarification loops.

**Do not use this** as a substitute for talking to the requester. It finds the questions;
only a human can get the answers.

## Prerequisites / inputs

- The story text (description, acceptance criteria if any)
- The process area or module it affects
- Target scope, if known
- Any constraints you already know about (licensing, OOB-first policy, deadlines)

## Starter prompt

```text
Analysis only - do not change anything.

Review this story for readiness to build and tell me what is missing or
ambiguous.

Story:
[paste the story description and any acceptance criteria]

Process area / module: [e.g. Incident, HR Case, Procurement]
Scope: [scope name, or "unknown"]
Known constraints: [licensing, OOB-first, deadline, or "none stated"]

Please:

1. List the specific questions that must be answered before this can be
   estimated or built. Order them by how much they would change the design.

2. Identify unstated assumptions the story is relying on.

3. Flag anything missing around: data model, who can see or do what
   (roles/permissions), notifications, reporting, integrations, error and
   edge-case handling, and what happens to existing records.

4. Check this instance for capability that already exists and could satisfy
   some or all of this, so we do not build something we already own.

5. Tell me what you could NOT determine from the story or the instance.
