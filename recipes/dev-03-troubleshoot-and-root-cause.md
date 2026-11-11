# DEV-03 — Troubleshoot a defect and find root cause

| | |
|---|---|
| **Area** | Development & Configuration |
| **Status** | 🟡 **Unverified starting point** — not yet proven on real work |
| **Owner** | Shyam Ram |
| **Last validated** | — |
| **Proven on** | Not yet. Be the first — see [How to verify](../README.md#how-to-verify-a-recipe). |

---

## When to use this

When something fails and nobody knows why. Replaces the manual correlation of logs, data
state, and configuration that normally eats hours.

Works for server-side failures, unexpected record behavior, notifications that did not
send, flows that stalled, and UI errors.

**Do not use this** when you already know the cause and just want it fixed — go straight
to [DEV-02](dev-02-develop-or-configure-from-story.md).

## Prerequisites / inputs

- A clear **symptom** — what you expected vs what happened
- The affected **record, table, or user**, ideally with a sys_id
- **When** it happened (a timeframe narrows log searching enormously)
- **Reproduction steps**, if known
- Which **instance and environment**
- What you have already ruled out

## Starter prompt

```text
Investigation only - do not change anything yet.

Help me find the root cause of this defect.

Symptom: [what you expected vs what actually happened]
Affected record / table / user: [sys_id or identifier]
When it happened: [date and time, or timeframe]
Environment: [instance name]
Reproduction steps: [steps, or "not reliably reproducible"]
Already ruled out: [what you have checked, or "nothing yet"]
Error message, if any: [paste it]

Please:

1. Give me ranked hypotheses for the cause, most likely first, with the
   evidence for each.

2. Investigate using read-only queries and by reading the configuration
   and scripts actually involved. Tell me what you find, including
   anything that contradicts a hypothesis.

3. Identify the specific artifact responsible - name, table, sys_id,
   and the line or condition that matters.

4. Explain the failure mechanism in plain terms, so I can tell someone
   else what went wrong.

5. Propose fix options with trade-offs. Do not implement anything yet.

6. Tell me what you could NOT check and what evidence is missing.
```

## Expected output

- **Ranked hypotheses** with supporting evidence, including disconfirming evidence
- The **specific artifact** responsible, identified precisely
- A plain-language **failure mechanism** you can relay to others
- **Fix options** with trade-offs, not implemented
- A statement of **missing evidence**

Good output rules things *out* as well as in. A single confident hypothesis with no
alternatives considered deserves skepticism.

## Validation checklist

- [ ] **Reproduce the failure** against the stated cause if you can — this is the real test
- [ ] Open the named artifact and confirm the mechanism described is actually what the code
      or condition does
- [ ] Check the disconfirming evidence: did it consider and reject alternatives, or just
      pick the first plausible answer?
- [ ] Confirm any script it ran was **read-only** if you intended investigation only
- [ ] Confirm it stated what it could not check

## Guardrails

See [GOVERNANCE.md](../GOVERNANCE.md). Specific to this recipe:

- **Keep investigation and remediation separate.** The prompt says investigation only, on
  purpose. Decide on the fix deliberately, not in investigative momentum.
- **Script execution is approval-gated, audited, and reversible** — but approve read-only
  diagnostics and nothing more during investigation. If asked to approve a script you do
  not understand, say no and ask what it does.
- **Never paste PII or customer data** into the symptom description. Reference record
  sys_ids instead.
- **Plausible ≠ proven.** An unreproduced root cause is a hypothesis. Label it as one.

---

## Appendix

### Follow-up prompts

```text
What evidence would disprove your top hypothesis?
```

```text
Has this failed silently before now, and how would we know?
```

```text
What would prevent this class of defect in future?
```

### Lessons learned

**Append-only. Date every entry.**

- _(empty)_
