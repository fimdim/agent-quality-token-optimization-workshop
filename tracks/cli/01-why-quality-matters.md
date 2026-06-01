# CLI · Module 01 — Why Quality Matters 🟢

**Goal:** feel the "agent gambling" anti-pattern in the terminal, then do it right, and compare scorecards.

Concepts: [Agent ROI](../../concepts/c1-agent-roi.md) ·
[Compounding error](../../concepts/c2-compounding-error.md)

---

## Part A : Gamble on purpose (the wrong way)

1. Start a fresh session from the repo root: `copilot`
2. Give it a deliberately weak, context-free prompt:

   ```text
   the tasks thing is broken, fix it
   ```

3. Respond to any questions with equally vague nudges ("still broken", "nope"). **Stop after 3 retries** even if unsolved.

   `Note: Part A can occasionally succeed on the first shot, but it usually burns more tokens/credits because the agent is guessing.`

Record the scorecard for Part B.

---

## Part B : Invest up front (the right way)

1. Exit and relaunch (or `/clear`) for a **clean session**.
2. Use a precise prompt that names the file, the bug, and a **stop condition**:

   ```text
   In @sample-app/src/tasks.ts, the test "includes tasks exactly equal to the threshold" (in @sample-app/src/tasks.test.ts) is failing. filterByMinPriority should treat
   minPriority as INCLUSIVE (>=), not exclusive (>). Fix only that function, then tell me to run `npm test` and stop. Do not change anything else.
   ```

3. In a normal terminal: `cd sample-app && npm test` → expect **4/4 pass**.

Record the scorecard for Part B.

---

## Part C : Compare

| Metric | Part A (gamble) | Part B (invest) |
| --- | --- | --- |
| Tokens | | |
| AI Credits | | |
| Retries to success | | |
| Agent turns | | |
| Tests green? | | |

Part B almost always wins on every axis, fewer tokens *and* a correct result. The "bigger" first prompt was the cheaper path. That's the ROI principle.

---

## One-shot variant (bonus)

Try the same correct fix as a single non-interactive command and compare the effort:

```bash
copilot --allow-all-tools --allow-all-paths -p "update tasks file"
cd sample-app && npm test
```

The extra flags avoid non-interactive permission blocks when the command needs to edit files.

A well-specified one-shot can solve a clear task in a single, cheap call.

---

## Compounding-error tie-in

Part A failed because the agent had to *guess* several things in a row (which file, which bug, how to verify). Each guess is a step with `p < 1`, and `p^n` collapses fast. Part B removed the guesses.

---

## Expected outcome

Two scorecards proving that up-front context + a stop condition beats retry-until-it-works.

➡️ Next: [02 — How the model thinks](02-how-the-model-thinks.md)
