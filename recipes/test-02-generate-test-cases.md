# TEST-02 — Generate positive, negative, business, and regression test cases

| | |
|---|---|
| **Area** | Testing & ATF |
| **Status** | 🟡 **Unverified starting point** — not yet proven on real work |
| **Owner** | Shyam Ram |
| **Last validated** | — |
| **Proven on** | Not yet. Be the first — see [How to verify](../README.md#how-to-verify-a-recipe). |

---

## When to use this

When you have scenarios (ideally from [TEST-01](test-01-generate-qa-scenarios.md)) and
need them written up as executable test cases with steps, data, and expected results —
traceable back to acceptance criteria.

**Do not use this** before the scenario surface is agreed. Writing cases for the wrong
scenarios is wasted effort, however well-formatted.

## Prerequisites / inputs

- The agreed scenario list, or acceptance criteria
- Target table, form, catalog item, or flow
- **Test users and roles** available to you
- Test data strategy — what exists, what must be created
- Your team's test case format, if you have one

## Starter prompt

```text
Analysis only - do not change anything.

Write executable test cases for the following, categorized by type.

Scenarios / acceptance criteria:
[paste the scenario list or AC]

Target: [table / form / catalog item / flow]
Test users and roles available: [list them]
Test data available: [describe, or "needs to be created"]

Please:

1. Inspect the real configuration so steps reference actual fields,
   states, choice values, and roles.

2. Produce test cases in four categories:
   - Positive: intended behavior works
   - Negative: invalid input and misuse are handled correctly
   - Business: the business outcome is actually achieved end to end,
     not just that fields were set
   - Regression: adjacent functionality still works

3. For each case give: ID, category, preconditions, numbered steps,
   expected result, and the acceptance criterion it traces to.

4. Call out required test data that does not exist yet.

5. Flag cases that cannot be objectively verified, and why.

6. Tell me what you could NOT determine.
```

## Expected output

- Test cases in **four categories**, each with steps, expected results, and traceability
- **Required test data** identified, including what must be created
- Cases flagged as **unverifiable**
- A statement of what could not be determined

The business category is the one most often missing from hand-written suites — it checks
the outcome was achieved, not merely that a field changed.

## Validation checklist

- [ ] Execute **one case manually** end to end. If the steps do not work as written, the
      rest need review too
- [ ] Verify referenced fields, states, and roles **exist**
- [ ] Check traceability: is every acceptance criterion covered by at least one case?
- [ ] Confirm expected results are **specific and objective**, not "works correctly"
- [ ] Confirm required test data is realistic to create in your environment

## Guardrails

See [GOVERNANCE.md](../GOVERNANCE.md). Specific to this recipe:

- **Non-production only** for execution.
- **Synthetic test data only.** Never fabricate realistic-looking personal data, and never
  copy production PII into a test case.
- **A well-formatted case can still assert the wrong thing.** Format is not correctness.

---

## Appendix

### Follow-up prompts

```text
Which of these cases are worth automating in ATF, and which should stay
manual?
```

```text
Generate the test data setup steps needed before this suite can run.
```

### Lessons learned

**Append-only. Date every entry.**

- _(empty)_
