# Build Agent Prompt Repository

Reusable starting points for using Build Agent during real ServiceNow delivery work.

**Phase:** 1 (pilot) · **Instance:** `redhathubdev` (DEV) · **Maintainer:** Shyam Ram

---

## 🟡 Every recipe here is an unverified starting point

Ten recipes, written to give the team something concrete to use from day one. **None has
been proven on real delivery work yet.**

That is deliberate and it is honest. Use them, expect to correct them, and record what you
corrected. Verification happens through use — see
[How to verify a recipe](#how-to-verify-a-recipe).

> A recipe becomes **Trusted** only when a second person gets a usable result on different
> work. Until then the 🟡 stays.

---

## ⚠️ Durability — read once

These files are the **canonical copy**. They live in a Build Agent workspace, which is
**not a durable store**.

- **Download or commit after every change.** Your local copy or GitHub repo is the backup.
- A DEV **clone will wipe anything that exists only in this instance.** DEV is refreshed
  during upgrade cycles — verified: 400 clone exclusions and 332 data preservers on this
  instance, none covering knowledge tables.
- Nothing here is installed to the instance. See [Why no app yet](#why-there-is-no-scoped-app-yet).

---

## How to use this

**Find → Understand → Copy → Use**

1. Find your task in the index below.
2. Read *When to use* and *Prerequisites*. Nothing else is required.
3. Copy the **Starter prompt** into Build Agent and fill in the `[placeholders]`.
4. Work the **Validation checklist**. Always.

New to Build Agent? Read [WORKING-WITH-BUILD-AGENT.md](WORKING-WITH-BUILD-AGENT.md) once.
Five minutes, and it covers capabilities most people never discover plus limitations that
will otherwise cost you an afternoon.

---

## Recipe index

### Requirements & Story Quality

| ID | Task / outcome | Status |
|---|---|---|
| [REQ-01](recipes/req-01-analyze-story-for-missing-information.md) | Analyze a story for missing information | 🟡 Unverified |
| [REQ-02](recipes/req-02-improve-acceptance-criteria.md) | Improve acceptance criteria | 🟡 Unverified |
| [REQ-03](recipes/req-03-requirements-to-technical-considerations.md) | Translate requirements into technical implementation considerations | 🟡 Unverified |

### Development & Configuration

| ID | Task / outcome | Status |
|---|---|---|
| [DEV-01](recipes/dev-01-analyze-configuration-before-change.md) | Understand what a change will impact before making it | 🟡 Unverified |
| [DEV-02](recipes/dev-02-develop-or-configure-from-story.md) | Develop or configure a solution from an approved story ⚠️ *changes the instance* | 🟡 Unverified |
| [DEV-03](recipes/dev-03-troubleshoot-and-root-cause.md) | Troubleshoot a defect and find root cause | 🟡 Unverified |

### Testing & ATF

| ID | Task / outcome | Status |
|---|---|---|
| [TEST-01](recipes/test-01-generate-qa-scenarios.md) | Generate comprehensive QA scenarios | 🟡 Unverified |
| [TEST-02](recipes/test-02-generate-test-cases.md) | Generate positive, negative, business, and regression test cases | 🟡 Unverified |
| [TEST-03](recipes/test-03-atf-candidates-and-authoring.md) | Determine ATF candidates and create ATF tests | 🟡 Unverified |

### Documentation

| ID | Task / outcome | Status |
|---|---|---|
| [DOC-01](recipes/doc-01-as-built-documentation-and-release-notes.md) | Produce as-built documentation and release notes | 🟡 Unverified |

**Status key:** 🟡 Unverified · 🔵 Under Review · 🟢 Trusted · ⚪ Retired.
Definitions in [GOVERNANCE.md](GOVERNANCE.md).

---

## Suggested starting points

| If you are… | Start with |
|---|---|
| A developer picking up a change | [DEV-01](recipes/dev-01-analyze-configuration-before-change.md) |
| Chasing a defect nobody understands | [DEV-03](recipes/dev-03-troubleshoot-and-root-cause.md) |
| A BSA grooming a vague story | [REQ-01](recipes/req-01-analyze-story-for-missing-information.md) |
| QA facing a change with no test coverage | [TEST-01](recipes/test-01-generate-qa-scenarios.md) |
| Asked "what does this app actually do?" | [DOC-01](recipes/doc-01-as-built-documentation-and-release-notes.md) |
| Preparing upgrade regression scope | [DEV-01](recipes/dev-01-analyze-configuration-before-change.md) then [TEST-01](recipes/test-01-generate-qa-scenarios.md) |

**Easiest first win:** DEV-01 or DOC-01. Both are read-only, neither can break anything,
and both produce something you can check in minutes.

---

## Where this lives

| Copy | Purpose |
|---|---|
| **This GitHub repo** | Canonical source of truth. Version history, diffs, durable. |
| **ServiceNow CoE Internal KB** | Published front door for the team. Category: **AI Delivery Acceleration** |

The KB articles are the readable surface; these files are the record. If they ever
disagree, this repo wins.

---

## How to verify a recipe

This is how 🟡 becomes 🟢. It takes about two minutes beyond the work you were doing anyway.

1. **Use it on real work.** Not a test case — actual delivery work.
2. **Work the validation checklist.** If you skip it, you have not verified anything.
3. **Append to Lessons learned** in the recipe file: date, what you had to change about the
   prompt, what the output got wrong, what to watch for.
4. **Fill in `Proven on`** with the real story, incident, or artifact.
5. **Tell the maintainer.** Status moves:
   - First successful use → 🔵 **Under Review**
   - A **different** person succeeds on **different** work → 🟢 **Trusted**

If it did not work, that is equally valuable — record why. A recipe that fails honestly is
more useful than one that quietly misleads.

---

## Contributing

Anyone on the delivery team may propose a recipe. Area owners publish.

**The one hard rule: no speculative recipes.** Beyond this initial ten, a new recipe may
only be proposed *after* it has produced a real result on real delivery work. Cite the
story, incident, or artifact. Ideas for prompts are infinite; prompts that worked on
Tuesday are not.

1. Use Build Agent successfully on real work.
2. Copy [RECIPE-TEMPLATE.md](RECIPE-TEMPLATE.md) into `recipes/`.
3. Fill it in, including what you had to correct.
4. Mark it 🟡 and tell an area owner.

**Improving an existing recipe:** append to Lessons learned. Never silently rewrite a
Trusted recipe — append, then flag for re-review.

**Cap:** ~12 Trusted recipes in Phase 1. A new one must displace or merge with an existing
one. Scarcity is the cheapest quality control available.

---

## Why there is no scoped app yet

A scoped application is the right eventual vehicle: one reinstall restores DEV after a
clone, and it promotes natively to TEST/QA → STAGE → PROD.

But all of those benefits are about *moving content between instances*, and Phase 1 moves
nothing. Creating it now would cost a permanent scope name and new metadata during an
upgrade cycle, for deferred benefit.

**Create the app when any of these becomes true:**
- The team needs to see recipes inside DEV
- A clone is approaching and you want one-action restore
- You are ready to promote to TEST/QA, STAGE, or PROD

Until then, these files plus your GitHub repo are the system of record.

---

## Open items

- [ ] **Verify the ten recipes through real use** — the whole point of Phase 1
- [ ] Name three area owners (currently all held by the maintainer)
- [ ] Move the durable copy to a **Red Hat org GitHub repo** — a personal account is a
      continuity and credential-ownership risk, and it must stay **private**
- [ ] After go-live: ask platform admins (Saul Eduardo Delgado Gonzalez, Juan Rodriguez Cruz)
      about instance↔GitHub source control linkage
- [ ] Convert the first 🟢 Trusted recipe into a **skill**, so it activates itself and
      nobody has to find or copy anything
- [ ] Decide whether PROD KB publication is wanted for wider discoverability# build-agent-docs
