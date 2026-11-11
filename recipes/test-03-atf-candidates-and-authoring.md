# TEST-03 — Determine ATF candidates and create ATF tests

| | |
|---|---|
| **Area** | Testing & ATF |
| **Status** | 🟡 **Unverified starting point** — not yet proven on real work |
| **Owner** | Shyam Ram |
| **Last validated** | — |
| **Proven on** | Not yet. Be the first — see [How to verify](../README.md#how-to-verify-a-recipe). |

---

## When to use this

When you want automated regression coverage and need to decide **what is worth automating**
before building anything. Automating the wrong tests produces a brittle suite nobody
trusts, which is worse than no suite.

Two phases: **decide candidates**, then **author the chosen ones**. Do not skip phase one.

This instance already has **625 ATF tests** and the client test runner enabled — check for
existing coverage before adding more.

**Do not use this** for one-off exploratory testing, or for anything that will change
shape next sprint.

## Prerequisites / inputs

- Agreed test cases or scenarios
- Target table, form, catalog item, or flow
- **Test user / role** the test should run as
- Test data strategy — ATF tests need predictable data
- A **non-production** instance
- Your existing test and suite naming conventions

## Starter prompt — phase 1: choose candidates

```text
Analysis only - do not create anything yet.

Assess which of these test cases are good ATF automation candidates.

Test cases / scenarios:
[paste them]

Target: [table / form / catalog item / flow]
Run-as user / role: [user or role]

Please:

1. Check whether ATF coverage already exists for any of this, so we do
   not duplicate. There are existing tests in this instance.

2. For each case, recommend Automate or Keep Manual, with reasoning.
   Favor automation for: stable, high-regression-risk, frequently
   repeated, deterministic server-side behavior. Favor manual for:
   subjective or visual checks, unstable UI, one-offs, anything needing
   complex external data.

3. Rank the automation candidates by payback - regression value per unit
   of authoring and maintenance effort.

4. Flag anything likely to be brittle, and why.

5. Tell me what test data each candidate needs.
```

## Starter prompt — phase 2: author the chosen tests

```text
Create ATF tests for the candidates we agreed. Non-production only.

Candidates to automate:
[list the agreed ones]

Target: [table / form / catalog item / flow]
Run-as user / role: [user or role]
Naming convention: [your convention]
Test data: [what exists / what to create]

Please:

1. Inspect the real schema, choice values, and - for UI steps - the
   actual rendered DOM, so steps target what genuinely exists.

2. Create the tests with meaningful assertions. An assertion that
   cannot fail is worse than no test.

3. Make test data setup and teardown explicit so tests are repeatable.

4. Run them and report results.

5. For any failure, tell me whether the test is wrong or the
   configuration is wrong - do not just report the step number.

6. Tell me what you could not automate and why.
```

## Expected output

**Phase 1:** an Automate / Keep Manual recommendation per case with reasoning, a payback
ranking, brittleness warnings, and test data requirements.

**Phase 2:** created ATF tests with real field and choice references, meaningful
assertions, explicit data setup, execution results, and failure analysis distinguishing a
bad test from a real defect.

## Validation checklist

- [ ] **Read the assertions.** A green test that asserts nothing is the main failure mode
      of generated ATF. This is the most important check here
- [ ] Confirm each test **can actually fail** — break something deliberately and see it go red
- [ ] Confirm it checks the **business outcome**, not just that a field was set
- [ ] Verify referenced fields, choices, and roles exist
- [ ] Re-run the test to confirm it is **repeatable**, not dependent on leftover state
- [ ] Confirm it ran in a **non-production** instance
- [ ] Check it did not duplicate existing coverage

## Guardrails

See [GOVERNANCE.md](../GOVERNANCE.md). Specific to this recipe:

- **NEVER run ATF against production.** It creates and modifies real records.
- **Assertion quality is everything.** Tests that pass vacuously create false confidence,
  which is more dangerous than no coverage.
- **UI tests are the brittle ones.** Build Agent can inspect real rendered DOM so selectors
  target what actually renders — but prefer server-side assertions where the choice exists.
- **Keep test data isolated** so tests do not depend on each other's leftovers.
- The `atf-run-test` skill covers execution and failure triage — it activates automatically
  when you ask to run a test.

---

## Appendix

### Follow-up prompts

```text
Break something this test should catch, then confirm it actually fails.
```

```text
Which of these tests will break for reasons unrelated to real defects?
```

```text
What coverage gaps remain after these tests?
```

### Lessons learned

**Append-only. Date every entry.**

- _(empty)_
