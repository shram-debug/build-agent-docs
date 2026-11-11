# Recipe NN — [Task or outcome, written as something you want to achieve]

> Copy this file into `recipes/` and fill it in. Delete these quoted instruction lines.
>
> **Design constraint: eight fields.** Earlier drafts of this repository had fifteen.
> Generation is cheap, but every published field has to be *verified* by a human, *scanned*
> by a reader, and *re-validated* at review. Fifteen fields × twelve recipes is 180 things
> to keep true. Keep it to eight. Put anything else in the appendix.

| | |
|---|---|
| **Area** | Requirements & Story Quality \| Development & Configuration \| Testing & ATF \| Documentation |
| **Status** | Draft \| Under Review \| Trusted \| Retired |
| **Owner** | [name] |
| **Last validated** | [date] against [platform release / SDK version] |
| **Proven on** | [the real story, incident, or artifact this produced a result for — required] |

---

## When to use this

> Two or three sentences. The reader is deciding in five seconds whether this is their
> recipe. Also state when **not** to use it — that is often more useful.

## Prerequisites / inputs

> What the user must have ready before starting. Be specific and listable.
> - Target scope
> - Specific record, table, or story
> - Access or role required
> - Which instance is appropriate

## Starter prompt

> The quick-copy payload. This is the whole point of the recipe — put it in a code block
> so it copies cleanly, and use `[square bracket]` placeholders.
>
> **Never use angle brackets for placeholders.** Knowledge article bodies are stored as
> HTML (`kb_knowledge.text` is an `html` field), so a placeholder wrapped in angle
> brackets is parsed as a tag and silently stripped or mangled — destroying the most
> important content in the recipe. Square brackets are HTML-safe everywhere.
>
> Also start analysis-only prompts with an explicit "do not change anything" line, and end
> with "tell me what you could NOT check". Those two lines do more for output quality than
> anything else in the recipe.

```text
[the prompt]
Expected output
What good looks like, so the user can tell whether they got it. Describe shape and
content, not length.

Validation checklist
Non-negotiable. How does a human confirm this is correct? Make it concrete and finite —
a checklist nobody can finish will not be used.

 Spot-check N items against the platform
 Confirm the output states what it could not check
 [domain-specific check]
Guardrails
Risks specific to this recipe. Do not restate GOVERNANCE.md — link it and add only
what is particular here.

Appendix (optional)
Follow-up prompts
Useful next moves, only where they genuinely add something.

Lessons learned
Append-only. Date each entry and never silently rewrite history — the corrections
are the most valuable content in the file, because they are the things the prompt alone
does not teach.

YYYY-MM-DD [what went wrong, what you changed, what to watch for]
Example artifact
Link, do not embed. Embedded examples go stale and bloat the page.

