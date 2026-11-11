# DEV-02 — Develop or configure a solution from an approved story

| | |
|---|---|
| **Area** | Development & Configuration |
| **Status** | 🟡 **Unverified starting point** — not yet proven on real work |
| **Owner** | Shyam Ram |
| **Last validated** | — |
| **Proven on** | Not yet. Be the first — see [How to verify](../README.md#how-to-verify-a-recipe). |

---

## ⚠️ This is the only Phase 1 recipe that changes the instance

Everything else here is analysis. Read the guardrails before using it.

## When to use this

When a story is approved with clear acceptance criteria and you want the build accelerated
— fields, business rules, script includes, client scripts, notifications, UI policies.
Works on **existing** records as well as new ones: Build Agent can pull a live record down
as editable source.

**Run [DEV-01](dev-01-analyze-configuration-before-change.md) first.** Building before
you know what depends on the target is how regressions happen.

**Do not use this for:** ACLs, roles, data policies, data-model-breaking changes, or
anything on a critical production path without a named reviewer.

## Prerequisites / inputs

- Approved story with **specific, testable acceptance criteria**
- Target scope, confirmed
- The specific records to change (name or sys_id) for brownfield work
- A **non-production** instance
- A **named update set** — not Default
- A human who will review the source diff

## Starter prompt

```text
Implement the following approved story. Work in small increments and
show me what you are changing before you install.

Story / acceptance criteria:
[paste the approved story and AC]

Scope: [scope name]
Existing records to modify: [names or sys_ids, or "none - new work"]
Update set: [named update set]

Please:

1. Confirm your understanding of the acceptance criteria before building,
   and ask about anything ambiguous rather than assuming.

2. Tell me what you intend to create or change, as a list, before you
   start.

3. Do NOT touch ACLs, roles, data policies, or make data-model-breaking
   changes. If the story needs them, stop and tell me.

4. Implement, validate with a build, and report exactly what changed.

5. After installing, tell me how to verify each acceptance criterion
   manually, and what you could not implement or verify.
```

## Expected output

- A **confirmed understanding** and clarifying questions before any building
- A **stated plan** of what will be created or changed
- Source changes, a successful build, and an install into your named update set
- A **report of what changed**, with per-artifact summaries
- **Manual verification steps** per acceptance criterion
- An explicit list of anything not implemented

## Validation checklist

- [ ] **Review the source diff**, not just the outcome. This is non-negotiable
- [ ] Verify each acceptance criterion manually in the UI
- [ ] Confirm nothing outside the stated plan was changed
- [ ] Confirm no ACL, role, or data policy was touched
- [ ] Confirm the change landed in your **named update set**, not Default
- [ ] Run [DEV-01](dev-01-analyze-configuration-before-change.md) against anything it
      modified, to check for impact it did not mention
- [ ] Peer review before promotion

## Guardrails

See [GOVERNANCE.md](../GOVERNANCE.md). Specific to this recipe:

- **Non-production only.**
- **Named update set, always.** Default makes the change hard to find and hard to promote.
- **Deletions need explicit confirmation.** Removing a `Table()`, `Record()`, or
  `BusinessRule()` definition can cascade and destroy installed metadata.
- **Security artifacts are excluded**, regardless of how reasonable the generated code looks.
- **Start small.** A single field or one business rule for your first use. Do not open with
  a multi-record feature.
- **A successful build is not a correct implementation.** It means the code compiles.

---

## Appendix

### Follow-up prompts

```text
What did you change that I did not explicitly ask for, and why?
```

```text
What are the three most likely ways this implementation breaks in
production?
```

```text
Generate ATF tests for the acceptance criteria you just implemented.
```

### Lessons learned

**Append-only. Date every entry.**

- _(empty)_
