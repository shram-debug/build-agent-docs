# Governance & Guardrails

Deliberately short. If this document gets long, it stops being read, and an unread
guardrail is not a guardrail.

---

## Hard rules

These are not guidelines.

| Rule | Why |
|---|---|
| **Non-production only** | No Build Agent recipe in this repository targets PROD. Analysis of PROD data may be acceptable; changes are not. |
| **Never put credentials in a prompt** | No passwords, PATs, API keys, client secrets. Use credential records. Prompts are logged. |
| **Never paste PII or customer data** | Use synthetic or already-anonymized examples. |
| **Never run ATF against production** | It creates and modifies real records. |
| **Security artifacts always get human review** | ACLs, roles, data policies. No exceptions, regardless of how confident the output looks. |
| **Deletions require explicit confirmation** | Removing a `Table()`, `Record()`, or `BusinessRule()` definition can cascade and destroy installed metadata. Confirm before, never after. |
| **Agent output is a draft** | Every recipe has a validation checklist. Running it is the user's job, not optional. |

### Excluded from unsupervised use

Do not use Build Agent to make these changes without a named reviewer:

- ACLs, roles, data policies, and anything else access-controlling
- Data-model-breaking changes (removing fields, changing types, changing table extension)
- Anything on a critical production path
- Integrations handling credentials or outbound data

---

## Status model

Uses four states. Nothing custom was built for this — it is a line in each recipe file,
and the matching native fields on the knowledge article.

| Status | Means | Who sets it |
|---|---|---|
| **Draft** | Worked once, for its author, on one piece of real work | Author |
| **Under Review** | Awaiting a second person's independent use | Author |
| **Trusted** | A **different** person got a usable result on **different** work | Area owner |
| **Retired** | Superseded, unreliable, or unused. Kept visible, not deleted. | Area owner |

In the KB these map to native fields: `workflow_state` (draft / review / published /
retired) and `confidence` (`work_in_progress` / `validated`). Use the platform's fields
rather than inventing a parallel status system.

### The second-user rule

This is the only quality gate that matters: **Trusted requires a second person, on
different work.** The author is the worst judge of their own prompt — they have context
the next person won't. If it only works for the person who wrote it, it is not a recipe,
it is a memory.

---

## Keeping it from becoming a catch-all

Mechanisms chosen to be structural rather than administrative. Nobody has time to police
a repository.

1. **No speculative recipes.** Must cite real delivery work that it produced a result on.
2. **Second-user rule for Trusted.** Above.
3. **Hard cap of ~12 Trusted recipes in Phase 1.** Scarcity is the cheapest quality
   control available. A new recipe must displace or merge with an existing one.
4. **Merge-first default.** First question on any submission: does this extend something
   we already have? Catch-alls grow by accretion of near-duplicates, not by one bad entry.
5. **180-day validity.** The SDK, the platform, and the agent all move faster than an
   annual review. Lapsed → back to `Under Review`, not retired.
6. **Usage signal, not analytics.** View counts, mark-as-helpful and comments are already
   enabled natively. If a recipe has not been used in a quarter and nobody can remember
   using it, it is a retirement candidate. No dashboards needed.
7. **Retire visibly, never delete.** Keeps the lesson and stops the same idea being
   resubmitted next quarter.
8. **Every recipe names what it could NOT do.** A recipe that claims total coverage is
   lying, and teaches users not to check.

---

## Roles

| Role | Who | Can |
|---|---|---|
| Maintainer | Shyam Ram | Everything; owns the durable copy and downloads |
| Area owner — Requirements & Story Quality | _TBD_ | Move Draft → Trusted in that area |
| Area owner — Development & Configuration | _TBD_ | Same |
| Area owner — Testing & ATF | _TBD_ | Same |
| Contributor | Anyone on the delivery team | Propose Drafts, append lessons learned |

Phase 1 runs with the maintainer holding all three area-owner slots. Split them when
contribution volume justifies it — not before.

**Not a review board.** One named person per area, able to say yes.

### A note on article ownership

`kb_knowledge.ownership_group` is set to **SN Leaders**. Verified: this field grants **no
read or write access** — it appears in zero `kb_knowledge` ACLs. It is stewardship
labeling only.

Actual access comes from the KB's user criteria: **SMO KB Can Read/Write**, **IT Support**,
and **PNT** can read and contribute. SN Leaders sits inside SMO KB Can Read/Write, so the
owning group can read and edit what it owns.

⚠️ `SN Testers` is **not** in those criteria. Any QA member who is only in that group
cannot open these articles.

---

## Review cadence

- **Per recipe:** 180 days from last validation.
- **Whole repository:** once per quarter — 30 minutes, check the cap, merge duplicates,
  retire the unused.
- **After every platform upgrade:** re-validate Trusted recipes. Behavior changes.

Each recipe records *last validated against* a platform/SDK version, not just a date.
A date alone does not tell you whether the thing it depended on still exists.

---

## A note on this instance

`redhathubdev` is DEV and is **refreshed from PROD during upgrade cycles.**

- Knowledge data (`kb_knowledge`) is **not** clone-excluded and **not** preserved —
  verified: 400 clone exclusions and 332 data preservers, none covering `kb_` tables.
- Therefore: anything that exists only in this instance will be destroyed by a clone,
  without warning and with no in-instance recovery.
- Articles promoted to PROD *do* survive, because clones flow PROD → DEV and bring them
  back down. But DEV edits made since the last export are lost.
- **The files are the asset. The instance is disposable.**

---

## Authoring note: HTML safety

Knowledge article bodies are stored as HTML (`kb_knowledge.text` is an `html` field).

- **Use `[square bracket]` placeholders, never angle brackets.** Angle brackets are parsed
  as tags and silently stripped — destroying the most important content in the recipe.
- **Author prompt blocks via the HTML source view or script, not the WYSIWYG editor.**
  TinyMCE reformats `<pre>` content and strips inline styling.
- Copy-out fidelity was tested on KB0030613 and passed: placeholders, line breaks,
  indentation and straight quotes all survived the round trip.
