# VS Code · Module 01 — Why Quality Matters 🟢

**Goal:** *feel* the cost of the "agent gambling" anti-pattern by deliberately doing it, then doing it right, and compare the scorecards.

Concepts: [Agent ROI](../../concepts/c1-agent-roi.md) ·
[Compounding error](../../concepts/c2-compounding-error.md)

---

## Part A : Gamble on purpose (the wrong way)

1. New Chat session, **Agent** mode, model **Auto**.
2. Give it this deliberately weak prompt, **no file context, vague ask**:

   ```text
   the tasks thing is broken, fix it
   ```

3. Whatever it does, resist helping. If it asks questions or guesses wrong, give equally vague nudges ("still broken", "no that's wrong"). **Stop after 3 retries** even if unsolved.

   `Note: Part A can occasionally succeed on the first shot, but it usually burns more tokens/credits because the agent is guessing.`

Record the scorecard for Part C.

---

## Part B1 : Invest up front (the right way)

1. **Start a brand-new Chat session** (clean context, important).
2. **Agent** mode. Add precise context: drag and drop [`sample-app/src/tasks.ts`](../../sample-app/src/tasks.ts) and [`sample-app/src/tasks.test.ts`](../../sample-app/src/tasks.test.ts) into the chat.
3. Use a precise prompt with a **stop condition**:

   ```text
   In sample-app, the test "includes tasks exactly equal to the threshold" is failing. The function filterByMinPriority should treat minPriority as INCLUSIVE (>=), not exclusive (>). Fix only that function, then tell me to run `npm test` and stop. Do not change anything else.
   ```

4. Run `npm test` in the terminal. Confirm **4/4 pass**.

Record the scorecard for Part C.

## Part B2 : Invest up front (variant using terminal output)

Do this after Part B1 so you can compare the scorecards; this variant uses the failing test output instead of spelling out the fix up front. In VS Code you can use #terminalLastCommand instead of copy/pasting the output.

1. **Start a brand-new Chat session** (clean context, important).
2. Open the terminal and run `cd sample-app && npm test`.
3. **Agent** mode. Add precise context: drag and drop [`sample-app/src/tasks.ts`](../../sample-app/src/tasks.ts) and [`sample-app/src/tasks.test.ts`](../../sample-app/src/tasks.test.ts) into the chat.
4. Use a precise prompt using the failing `npm test` output and a **stop condition**:
   ```text
   Use the #terminalLastCommand information to fix the failing test directly. Modify only the production-code function that is failing (do not change tests), then tell me to run `npm test` and stop. Do not change anything else.
   ```
5. Run `npm test` in the terminal. Confirm **4/4 pass**.

Record the scorecard for Part C.

---

## Part C : Compare

| Metric | Part A (gamble) | Part B1 (invest) | Part B2 (alternative) |
| --- | --- | --- | --- |
| Tokens / AI credits used | | | |
| Retries to success | | | |
| Agent turns | | | |
| Tests green? | | | |

**Reflection:** Parts B1 and B2 almost always win on *every* axis, fewer tokens *and* a correct result. That's the ROI principle in action: the "bigger" first prompt was the cheaper path.

---

## Compounding-error tie-in

Part A failed partly because the agent had to *guess* several things in a row (which file, which bug, how to verify). Each guess is a step with `p < 1`, and `p^n` collapses fast. Parts B1 and B2 removed the guesses, pushing each step's `p` toward 1.0.

---

## Expected outcome

You have three scorecards proving that an up-front investment in context + a stop condition beats retry-until-it-works on retries, turns, *and* correctness.

➡️ Next: [02 — How the model thinks](02-how-the-model-thinks.md)
