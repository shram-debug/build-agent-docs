# TEST-01 — Generate comprehensive QA scenarios

| | |
|---|---|
| **Area** | Testing & ATF |
| **Status** | 🟡 **Unverified starting point** — not yet proven on real work |
| **Owner** | Shyam Ram |
| **Last validated** | — |
| **Proven on** | Not yet. Be the first — see [How to verify](../README.md#how-to-verify-a-recipe). |

---

## When to use this

When you have acceptance criteria and need the full scenario surface before writing test
cases — including the negative, permission, and data-state scenarios that get forgotten
until UAT.

Also valuable for **upgrade regression scoping**: "what scenarios does this touched
configuration need re-tested?"

**Do not use this** as the test cases themselves — this produces the *scenario list*.
Use [TEST-02](test-02-generate-test-cases.md) to turn them into executable cases.

## Prerequisites / inputs

- Acceptance criteria, or the configuration being changed
- The **roles and personas** involved
- Target table, form, catalog item, or flow
- Known integrations or downstream dependencies

## Starter prompt

```text
Analysis only - do not change anything.

Generate a comprehensive QA scenario list for the following.

What is being tested:
[paste acceptance criteria, or describe the configuration change]

Target: [table / form / catalog item / flow]
Roles involved: [e.g. requester, fulfiller, approver, admin]
Known integrations or downstream impacts: [or "none known"]

Please:

1. Inspect the actual configuration in this instance so the scenarios
   reflect real fields, states, choices, and roles rather than assumptions.

2. Produce scenarios grouped by: happy path, negative / invalid input,
   boundary and edge cases, role and permission variations, data-state
   variations (existing vs new records, empty vs populated), notification
   and integration effects, and regression risk to adjacent functionality.

3. For each scenario give a one-line description and why it matters.

4. Rank by risk - what would hurt most if it broke and went unnoticed.

5. Flag which scenarios are hard or impossible to test, and why.

6. Tell me what you could NOT determine about the configuration.
```

## Expected output

- Scenarios **grouped by category**, grounded in real fields and choice values
- A **risk ranking**
- Scenarios flagged as **hard or impossible to test**
- A statement of what could not be determined

Good output includes permission and data-state scenarios you would have missed. If it only
produces happy-path variations, the target was described too narrowly.

## Validation checklist

- [ ] Spot-check that referenced **fields, states, and choice values actually exist** —
      this is the fastest way to catch invented detail
- [ ] Confirm the **roles** named are real roles in this instance
- [ ] Check coverage against the acceptance criteria — is any criterion untested?
- [ ] Apply judgment on volume: 80 scenarios for a small change means it padded. Cut
- [ ] Confirm it flagged untestable scenarios rather than quietly including them

## Guardrails

See [GOVERNANCE.md](../GOVERNANCE.md). Specific to this recipe:

- **Scenario count is not coverage.** A long list can still miss the one that matters.
- **Instance-specific.** Scenarios reflect the instance inspected; DEV drifts from PROD.
- **Do not include real customer data** in scenario descriptions.

---

## Appendix

### Follow-up prompts

```text
Which of these scenarios would fail silently rather than visibly?
```

```text
If I could only run five of these, which five and why?
```

```text
Which of these are good ATF candidates versus manual-only?
```

### Lessons learned

**Append-only. Date every entry.**

- _(empty)_
