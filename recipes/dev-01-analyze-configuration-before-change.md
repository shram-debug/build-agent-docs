---

# 📄 File 8 of 14

### Path / filename: `recipes/dev-01-analyze-configuration-before-change.md`

```markdown
# DEV-01 — Understand what a change will impact before making it

| | |
|---|---|
| **Area** | Development & Configuration |
| **Status** | 🟡 **Unverified starting point** — not yet proven on real work |
| **Owner** | Shyam Ram |
| **Last validated** | — |
| **Proven on** | Not yet. Be the first — see [How to verify](../README.md#how-to-verify-a-recipe). |
| **Published as** | KB0030613 (CoE Internal → AI Delivery Acceleration) |

---

## When to use this

Before changing a table, field, integration, or process, when you need to know what else
depends on it. Replaces the 30-minutes-to-3-hours of manual archaeology across business
rules, client scripts, ACLs, flows, UI policies, and transform maps.

Particularly valuable during an **upgrade cycle**, where the question "what regression
does this touch?" has to be answered repeatedly.

**Do not use this for:** proving a *negative* in production. It tells you what it found in
the instance you pointed it at. It cannot prove nothing else exists, and DEV drifts from
PROD — hard, immediately after a clone.

## Prerequisites / inputs

- The **target**: table, field, integration, or process name
- The **scope(s)** in play — or say "all scopes including global" if you do not know
- A description of **the change you are considering** (the impact assessment is only as
  good as this)
- Correct instance for the question. DEV findings are not PROD truth.

## Starter prompt

```text
I need to understand the full impact of a change before I make it.
Analysis only - do not change anything.

Target: [table / field / integration / process]
Scope(s): [scope name, or "all scopes including global"]
Change I am considering: [describe the change concretely]

Please:

1. Inventory every configuration artifact that reads, writes, validates, or
   reacts to this target. Include business rules, client scripts, UI policies,
   data policies, ACLs, flows and workflows, script includes called by any of
   them, scheduled jobs, transform maps, inbound actions, and notifications.

2. For each one give me: name, table, scope, sys_id, when it runs
   (trigger / condition / order), and one sentence on what it actually does.

3. Call out the specific risks for my proposed change - execution-order
   conflicts, before vs after vs async timing, ACL overlap, and anything that
   would silently stop working rather than fail loudly.

4. Tell me what you could NOT check, and where your inventory may be
   incomplete.

5. Recommend the order I should review these in, highest risk first.
Expected output
An inventory table of dependent artifacts with sys_ids, scope, and trigger detail
A risk list naming specific failure modes for your change, not generic cautions
An explicit gaps section describing what was not checked
A recommended review order
Good output names things you did not know existed. Output that only lists what you already
knew usually means the target or scope was too narrowly specified.

Validation checklist
 Open 2–3 of the listed artifacts in the platform and confirm they exist and do
what the summary says
 Confirm the output includes a gaps / "could not check" section. If it is missing,
ask for it — a clean bill of health with no stated limits is a warning sign
 Ask yourself: is there anything I know about that is missing? If yes, the scope
given was probably too narrow — re-run with it widened
 Confirm global scope was included, not just the app scope
 If this informs a PROD change, confirm whether DEV reflects PROD for these
artifacts
 Sanity-check at least one execution-order claim — order and timing are where
impact assessments are most often wrong
Guardrails
See GOVERNANCE.md for the standing rules. Specific to this recipe:

Read-only by intent. The prompt says "analysis only". Keep analysis and change in
separate conversations so a discovery session cannot drift into an unreviewed edit.
Recall, not proof. Semantic search finds a lot and guarantees nothing. Treat the
inventory as a strong lead list, never as a completeness certificate.
Instance-specific. State which instance the analysis came from whenever you share it.
Do not paste the output into a change record as justification without completing the
validation checklist. It reads authoritative whether or not it is right.
Appendix
Follow-up prompts
What could you not check, and what would it take to check it?
Of everything you found, which three are most likely to break silently
rather than throw an error? Explain why.
Draft the regression test scenarios this change would need, based on the
artifacts you found.
Which of these artifacts are customizations that an upgrade might skip
or revert?
Lessons learned
Append-only. Date every entry. Do not rewrite.

(empty — add the first entry when this recipe is first used on real work)
Example artifact
(link a real impact assessment here once one exists)
