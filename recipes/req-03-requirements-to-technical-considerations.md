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
Expected output
An inventory of reusable existing capability (the most valuable part)
2–3 options with trade-offs and upgrade-safety assessment
A recommendation with explicit reasoning
Metadata inventory for the recommended option
Data model sketch where relevant
Open decisions for humans
Validation checklist
 Verify the "already exists" findings by opening at least one — reuse claims are the
highest-value and highest-risk part of this output
 Challenge the recommendation: does it default to custom where OOB would do?
 Confirm upgrade-safety reasoning is specific, not boilerplate
 Check the metadata inventory against your own expectation — what is missing?
 Confirm it flagged what it could not determine
Guardrails
See GOVERNANCE.md. Specific to this recipe:

Architecture stays human-owned. This is input to a decision, never the decision.
It does not know your licensing entitlements. A proposal using a product you are not
entitled to will look perfectly reasonable. Verify.
Instance-specific. Findings reflect the instance it looked at — DEV drifts from PROD.
Appendix
Follow-up prompts
What would make you change your recommendation?
Which parts of this are reversible, and which are one-way doors?
Break the recommended option into stories with acceptance criteria.
Lessons learned
Append-only. Date every entry.

(empty)
