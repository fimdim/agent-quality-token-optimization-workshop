# CLI · Module 03 — Lever 1: Model Selection 🟡

**Goal:** match model size to task difficulty from the CLI.

> **Rule of thumb:** large = planning/debugging · medium = implementation · small = simple tasks · **Auto by default**.

Suggested starting point from [GitHub's model comparison page](https://docs.github.com/en/copilot/reference/ai-models/model-comparison):

- **Deep reasoning/debugging (large):** `GPT-5.5`, `GPT-5.4`, `Claude Opus 4.7`, `Gemini 2.5 Pro`
- **General implementation (medium):** `GPT-5 mini`, `GPT-4.1`, `Claude Sonnet 4.6`
- **Simple/repetitive tasks (small/fast):** `Claude Haiku 4.5`, `Gemini 3 Flash`

Pick one available in your org/plan. If a model isn't available, choose the closest option in the same category.

---

## Selecting a model in the CLI

Model selection varies by CLI version. Check what your install supports:

```bash
copilot --help        # look for a model flag, e.g. --model
```

Inside a session, run `/help` and look for a model command (often `/model`). Use whichever your version exposes. If neither exists, your CLI uses an automatic default, that's fine; do the exercises by comparing **task difficulty** and noting outcomes.

```bash
# Example shapes (confirm against your version):
copilot --model <large-model> -p "..."
# or, inside a session:
/model
```

Examples:

```bash
copilot --model "GPT-5.5" -p "..."          # deep reasoning/debugging
copilot --model "GPT-5 mini" -p "..."       # general coding
copilot --model "Claude Haiku 4.5" -p "..." # quick/simple edits
```

---

## Exercise A : A "planning/debugging" task (use a large model)

1. Start a session with a **capable** model (for example: `GPT-5.5`, `GPT-5.4`, `Claude Opus 4.7`, or `Gemini 2.5 Pro`). Don't let it edit yet:

   ```text
   Don't change code. Read @sample-app/src/tasks.ts and @sample-app/src/tasks.test.ts and explain why the "exactly equal to the threshold" test fails and exactly what the fix is. Be specific about the comparison operator.
   ```

Record: did it pinpoint `>` vs `>=`? How clear was the reasoning?

---

## Exercise B : A "simple" task (use a small/fast model)

1. New session with a **smaller/faster** model (for example: `Claude Haiku 4.5`, `Gemini 3 Flash`, or another fast model in your list) (or a one-shot):

   ```bash
   copilot --model <small-model> -p "In sample-app/src/tasks.ts, change the comparison in filterByMinPriority from > to >=. Nothing else."
   ```

2. `cd sample-app && npm test` → expect 4/4 green.

A small model handles a one-line mechanical edit perfectly, cheaper and faster.

---

## Exercise C : Compare (mismatch on purpose)

- Ask the **small** model to do Exercise A's *diagnosis*. Did it miss nuance?
- Ask the **large** model to do Exercise B's *one-liner*. Overkill?

| | Diagnosis (hard) | One-liner (easy) |
| --- | --- | --- |
| Large model | quality? speed? | overkill? |
| Small model | missed nuance? | fine? |

**Lesson:** big models earn their cost on ambiguous reasoning; small models win on well-specified mechanical work. The wrong-sized model either wastes value or causes retries.

---

## When in doubt

Use the **automatic/default** model. Choose deliberately only when the task is clearly very hard (planning/debugging) or clearly trivial (rename, format, one-liner).

---

## Expected outcome

You've matched three tasks to model choices from the CLI and can justify why right-sizing maximizes token value.

➡️ Next: [04 — Lever 2: Context optimization](04-context-optimization.md)
