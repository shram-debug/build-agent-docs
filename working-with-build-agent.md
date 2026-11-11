# Working with Build Agent

Read once. Five minutes. Saves more than that.

---

## The first thing that matters: scope

Build Agent works inside an **application scope**. Before it can read or write files it
needs to know whether you are working in a specific app or platform-wide (`global`).

Get this wrong and you will get confusing results — it will look in the wrong place and
tell you something does not exist when it does. If you are unsure which scope your work
lives in, say so; it can find out.

**One scope per conversation.** To switch apps, start a new conversation.

---

## Why it asks you questions

It asks one focused question at a time when something ambiguous would change the answer.
This is a feature. The alternative is a confident, wrong result that costs you an hour to
discover.

If it asks something you do not know, say so — it can usually go and look.

---

## Approval gates

Nothing surprising happens silently:

- **Server-side scripts** require your explicit approval before running. Every run is
  recorded for audit, and data changes can be **rolled back**.
- **Installing** to the instance requires approval.
- **Deletions** of metadata definitions require explicit confirmation.

If you are asked to approve something you do not understand, **say no and ask what it
does.** That is a legitimate and expected answer.

---

## Capabilities you may not know exist

Most people underestimate Build Agent in the same way: they assume it writes new code.
Its more useful skill is understanding what already exists.

| Capability | Why it matters |
|---|---|
| **Brownfield round-tripping** | It can pull an **existing** instance record — business rule, script include, table, ATF test — down as editable source, change it, and redeploy. This is not a greenfield-only tool. Most under-appreciated capability by a wide margin. |
| **Semantic search across all metadata** | Ask "what validates incident state?" without knowing which tables to look in. Searches flows, business rules, ACLs, roles, script includes, notifications simultaneously. |
| **Real schema introspection** | Returns actual fields, types, and mandatory flags. The reason its generated code uses real field names instead of plausible-sounding ones. |
| **Audited, reversible script execution** | Approval-gated, recorded, and undoable. Changes the risk calculus for investigation work. |
| **Live page diagnostics** | Opens a page and captures console errors, network failures, and a DOM snapshot. A real smoke test, not a guess. |
| **ATF test + suite execution** | Runs tests and polls for results. |
| **Dedicated ATF failure triage** | A specialist sub-agent that correlates a failure with the metadata that caused it and proposes fixes — not just "step 4 failed". |
| **Component DOM inspection** | Reads real component sources so UI test selectors target what actually renders. A React `Button` component does not render as an HTML `button` element — this is why UI tests are usually brittle. |
| **Version-accurate SDK docs** | It reads the docs shipped with *your* installed SDK rather than relying on memory. Materially fewer invented APIs than general-purpose coding assistants. |
| **Skills** | Reusable procedures that activate themselves when they recognize the task — no searching, no copy-paste. Two ship today: `atf-run-test`, `update-system-property`. Our proven recipes can become skills. |
| **Parallel exploration sub-agents** | Large investigations run in isolated context without polluting your conversation. |
| **Approvable plans** | For multi-step work you can require a reviewed plan before any building starts. |
| **Named update sets + per-artifact install summaries** | Your audit trail and review material get produced as a by-product. |

---

## Known limitations — read these, they will save you time

- **No git or terminal access.** It cannot create a repo, commit, or push. It authors
  files; you carry them to GitHub.
- **The workspace is not durable.** Download your files. See the warning in the README.
- **Results are instance-specific.** What it finds in DEV reflects DEV. DEV drifts from
  PROD, and drifts hard right after a clone. Never present DEV findings as PROD truth.
- **Semantic search is recall-oriented, not exhaustive.** It finds a lot; it does not
  guarantee everything. Always ask what it could not check.
- **It cannot know your business context.** Licensing entitlements, roadmap, political
  constraints, why a weird customization exists. It will not know unless you tell it.
- **Confident tone ≠ correct.** Output reads fluently whether it is right or wrong. The
  validation checklist in each recipe exists for this reason.

---

## Prompting that actually works

1. **State the goal, not the steps.** "I need to know what breaks if I change X" beats
   "query sys_script where collection=X".
2. **Give it the scope.** Saves a round trip every time.
3. **Say what you have already ruled out.** Stops it re-treading your ground.
4. **Ask for the gaps.** "What could you not check?" is the single highest-value
   follow-up question available.
5. **Say "analysis only, change nothing"** when you are investigating. Removes ambiguity.
6. **Push back.** If output looks wrong, say so plainly. It will re-examine rather than
   defend.
7. **Iterate in one conversation.** Context accumulates; starting over discards it.

---

## When something goes wrong

- **Wrong scope** → say so; it can re-establish or you can start a fresh conversation.
- **Build fails** → report the errors, do not work around them. A broken source with a
  scripted workaround leaves the source broken.
- **Output looks plausible but you cannot verify it** → treat it as unverified. That is a
  legitimate outcome; record it in the recipe's Lessons learned.
- **Session auth errors (401)** → transient. Retry, or start a new conversation.
- **Plan mode blocks edits.** If the agent reports it cannot write files, the session is
  in plan mode. Reading and querying still work; editing does not. Switch mode or start a
  new conversation.
