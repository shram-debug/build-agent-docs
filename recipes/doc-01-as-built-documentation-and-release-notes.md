# DOC-01 — Produce as-built documentation and release notes

| | |
|---|---|
| **Area** | Documentation |
| **Status** | 🟡 **Unverified starting point** — not yet proven on real work |
| **Owner** | Shyam Ram |
| **Last validated** | — |
| **Proven on** | Not yet. Be the first — see [How to verify](../README.md#how-to-verify-a-recipe). |

---

## When to use this

When documentation is missing, stale, or needed for handover, audit, support, or a release.
Build Agent reads the **real configuration** rather than relying on anyone's memory, which
is why this is the cheapest win in the repository.

Three common uses: as-built documentation for an app or feature, release notes for an
update set or app version, and a support runbook.

**Do not use this** to document *why* the business wanted something. It can describe what
the configuration does; intent has to come from a human.

## Prerequisites / inputs

- The scope, app, update set, or specific records to document
- **Audience** — this changes the output more than anything else (developer, support,
  audit, business)
- Your documentation template, if you have one

## Starter prompt

```text
Analysis only - do not change anything.

Produce as-built documentation for the following.

What to document: [app / scope / update set / list of records]
Audience: [developer | support | audit | business stakeholder]
Format: [our template, or "sensible markdown structure"]

Please:

1. Read the actual configuration rather than assuming standard behavior.

2. Document: purpose, data model (tables and key fields), roles and who
   can do what, automation inventory (business rules, flows, scripts,
   scheduled jobs) with trigger conditions, integration points,
   notifications, and known constraints or quirks.

3. Pitch the depth and language at the audience I named.

4. Mark clearly anything you are inferring rather than reading directly
   from configuration.

5. List what you could not determine and what a human needs to fill in -
   especially business intent.

6. Flag anything sensitive that should not appear in shared documentation,
   such as endpoints, credential references, or embedded identifiers.
```

## Expected output

- Structured documentation pitched at the stated audience
- **Inferences clearly marked** as distinct from read configuration
- A list of **gaps a human must fill**, business intent first
- **Sensitive content flagged** before you share it anywhere

## Validation checklist

- [ ] Spot-check **2–3 documented behaviors** against the actual configuration
- [ ] Add the **business intent** it could not know — this is the human's main contribution
- [ ] Review for **sensitive detail** before sharing: endpoints, credential references,
      internal identifiers, anything that should not leave the team
- [ ] Confirm inferences are labeled as inferences
- [ ] Confirm the depth suits the audience — support runbooks and audit documents are not
      the same document

## Guardrails

See [GOVERNANCE.md](../GOVERNANCE.md). Specific to this recipe:

- **Describes what, not why.** Unlabeled intent statements are the main risk in generated
  documentation — they read authoritatively and may be invented.
- **Review before publishing anywhere shared.** Aggregated configuration detail is more
  sensitive than any single item in it.
- **Date it and name the instance.** Documentation without a date and source instance
  becomes misleading the moment configuration changes.

---

## Appendix

### Follow-up prompts

```text
Turn this into a support runbook: symptoms, likely causes, first
diagnostic steps.
```

```text
Draft release notes for this update set, for a business audience.
```

```text
What in this configuration would surprise a developer picking it up cold?
```

### Lessons learned

**Append-only. Date every entry.**

- _(empty)_


Global

