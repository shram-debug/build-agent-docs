---

# 📄 File 6 of 14

### Path / filename: `recipes/req-02-improve-acceptance-criteria.md`

```markdown
# REQ-02 — Improve acceptance criteria

| | |
|---|---|
| **Area** | Requirements & Story Quality |
| **Status** | 🟡 **Unverified starting point** — not yet proven on real work |
| **Owner** | Shyam Ram |
| **Last validated** | — |
| **Proven on** | Not yet. Be the first — see [How to verify](../README.md#how-to-verify-a-recipe). |

---

## When to use this

When a story has acceptance criteria that are vague, untestable, or only cover the happy
path. Turns "it should work correctly" into criteria QA can actually execute against.

Pairs naturally with [TEST-01](test-01-generate-qa-scenarios.md) — good criteria make
good test scenarios nearly automatic.

**Do not use this** to invent criteria for a requirement nobody has agreed yet. Fix the
requirement first with [REQ-01](req-01-analyze-story-for-missing-information.md).

## Prerequisites / inputs

- The story and its current acceptance criteria
- Who the affected users/roles are
- Any known constraints or non-functional expectations

## Starter prompt

```text
Analysis only - do not change anything.

Rewrite and strengthen the acceptance criteria for this story so they are
specific, testable, and complete.

Story:
[paste the story]

Current acceptance criteria:
[paste what exists, or "none"]

Affected roles / users: [e.g. requester, fulfiller, approver, manager]

Please:

1. Rewrite the criteria so each one is independently testable and states a
   clear expected outcome. Use Given / When / Then.

2. Add missing coverage for: negative paths, boundary and edge cases,
   role and permission differences, required vs optional fields,
   notifications, and what happens to existing records.

3. Flag any criterion that cannot be objectively verified, and say why.

4. Note any criterion that implies work the story does not currently
   mention, so scope creep is visible rather than hidden.

5. Keep it proportionate - do not pad. Flag any criterion you think is
   unnecessary.
