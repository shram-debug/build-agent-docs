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
