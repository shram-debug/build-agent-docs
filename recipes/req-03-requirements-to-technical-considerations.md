# REQ-03 — Translate requirements into technical implementation considerations

| | |
|---|---|
| **Area** | Requirements & Story Quality |
| **Status** | 🟡 **Unverified starting point** — not yet proven on real work |
| **Owner** | Shyam Ram |
| **Last validated** | — |
| **Proven on** | Not yet. Be the first — see [How to verify](../README.md#how-to-verify-a-recipe). |

---

## When to use this

When a story is agreed but the technical approach is not, and you need options with
trade-offs before committing. Grounds the design in what this instance already has
rather than generic ServiceNow theory.

Most valuable when the honest answer might be "configure what we already own" instead of
"build something new".

**Do not use this** as an architecture decision record. It produces options; an architect
chooses.

## Prerequisites / inputs

- The agreed story and acceptance criteria
- Target scope, or the fact that it is undecided
- Constraints: OOB-first policy, licensing, upgrade-safety expectations, timeline
- Any existing apps or tables you believe are related

## Starter prompt

```text
Analysis only - do not change anything.

Propose technical implementation options for this requirement, grounded in
what already exists in this instance.

Requirement / story:
[paste the story and acceptance criteria]

Scope: [scope name, or "undecided"]
Constraints: [OOB-first, licensing, upgrade-safety, timeline]

Please:

1. First, inventory what already exists here that is relevant - tables,
   fields, roles, script includes, flows, catalog items. Reuse before build.

2. Give me 2-3 implementation options. For each: approach, what gets
   created or changed, upgrade-safety, and the main trade-off.
   Explicitly consider out-of-the-box configuration before customization.

3. Recommend one, and say plainly why the others lose.

4. For the recommended option, list the metadata that would need to be
   created or changed.

5. Sketch the data model if new tables or fields are involved.

6. List the open questions and decisions a human must make before build,
   and anything you could not determine.
