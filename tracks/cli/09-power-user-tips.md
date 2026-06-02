# CLI · Module 09 — Power-User Tips 🔴

**Goal:** exploit the terminal's superpower, **pipes and scripts**, to filter inputs, collapse outputs, and analyze usage. This is where the CLI track shines.

> Use scripts to filter data · optimize CLI outputs · collapse tool calls · analyze usage patterns.

---

## 1. Filter data *before* it reaches the model

The CLI composes with the shell, so you can hand the agent a **pre-filtered** slice instead of a whole file:

```bash
# Feed only the relevant lines into a one-shot prompt
grep -n "RegExp" sample-app/src/*.ts | copilot -p "Explain the security risk in these lines and how to fix it. Do not edit files."

# Summarize only the failing test output, not the full log
cd sample-app && npm test 2>&1 | tail -n 20 | copilot -p "Why is this test failing and what's the minimal fix? Do not edit files."

# Just the dependency names
node -p "Object.keys(require('./sample-app/package.json').dependencies)" | copilot -p "Are any of these unnecessary for a basic Express API? Do not edit files."
```

You decide what's relevant, the model never wades through noise.

---

## 2. Keep tool output lean

When the agent runs commands, noisy output is tokens. Prefer quiet commands:

| Noisy | Lean |
| --- | --- |
| `npm test` (full log) | `npm test 2>&1 \| tail -n 20` |
| `cat bigfile.ts` | `sed -n '40,80p' bigfile.ts` |
| `ls -R` | `git ls-files src` |

Tell the agent in your prompt: "run the quietest command that proves it works."

---

## 3. Collapse long sessions into a summary

When a session grows (and gets pricey), compress instead of extending:

```text
Summarize what we changed and the current state in 5 bullet points.
```

Save that summary, start a **new** session, and paste it as the seed. You've turned a huge
transcript into a few lines, a manual, high-leverage reset that fights "lost in the middle" and
recency bias.

> `copilot --resume` reloads a full transcript; a **summary-seeded new session** is often far cheaper for the same continuity.

**Or let the CLI do it in one command** with `/compact`:

```text
/compact
```

`/compact` compresses your conversation history in place, replacing the long transcript with a summary while keeping you in the same session. The CLI also **auto-compacts** in the background when you approach ~95% of the token limit, so sessions can run almost indefinitely. Use `/context` to see a token-usage breakdown and decide *when* a manual `/compact` is worth it. Press `Esc` to cancel a compaction if you change your mind.

> Rule of thumb: `/compact` to **continue** the same task cheaply; a summary-seeded **new** session to start a clean, unrelated task.

---

## 4. Script repeatable guardrail loops

Bundle a task with its verification so the agent's work is gated automatically:

```bash
copilot -p "Implement <change> in sample-app. Done when build, tests, and lint pass." \
  && cd sample-app && npm run build && npm test && npm run lint \
  && echo "ALL GREEN" || echo "NEEDS WORK"
```

This is Lever 5 (deterministic controls) expressed as a one-liner.

---

## 5. Analyze your usage patterns

Review your scorecards:

- Which tasks needed the most retries? Missing context, no stop condition, wrong model?
- Where did you over-stuff context?
- Which guardrail caught the most mistakes?

Promote recurring fixes into `AGENTS.md` (Module 08) so you never pay for that lesson twice. If your CLI exposes usage/billing info (`/help` or account dashboard), correlate big sessions with low-quality outcomes, those are your prime optimization targets.

---

## Expected outcome

You can pre-filter inputs with pipes, keep output and sessions lean, script guardrail loops,
compress context with `/compact` and use scorecard history to improve your defaults.

➡️ Next: [10 — Capstone](10-capstone.md)
