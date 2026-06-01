# CLI · Module 10 — Capstone 🔴

**Goal:** combine all five levers to ship one clean, verified feature on the sample app from the terminal, and prove the difference with your scorecard.

---

## The brief

> Add a **`PATCH /tasks/:id`** endpoint that lets a client update a task's `title`, `priority`, or `done` status. It must validate input, reject unknown IDs with 404, follow project conventions, and keep all checks green.

This touches routing, validation, business logic, and storage, a realistic multi-step change.

---

## Run it through all five levers

1. **Model selection (Lever 1)** : capable model for research/plan; you may drop to a smaller    model (or one-shot) for mechanical edits.

2. **Workflow design (Lever 4)** : phases with resets between each:
   - **Research:** `copilot` →
     ```text
     Don't change code. Analyze how updates should flow through @sample-app/src/routes.ts, @sample-app/src/store.ts, @sample-app/src/tasks.ts, and @sample-app/src/types.ts, and what the store needs to support update-by-id. Write it to RESEARCH.md.
     ```
   - **Plan:** fresh session → `Read @RESEARCH.md and write PLAN.md as a small, ordered, testable checklist. No code.` Review and edit `PLAN.md`.
   - **Implement:** fresh session → feed one step at a time.

3. **Context optimization (Lever 2)** :reference only the files each phase needs; `/clear` between phases; consider `cd sample-app && copilot` to scope exploration.

4. **Prompt engineering (Lever 3)** : every implement prompt includes explicit constraints and a verifiable **Done when** stop condition.

5. **Deterministic controls (Lever 5)** : write tests first in `src/routes.test.ts` (valid patch → 200; unknown id → 404; invalid priority → 400), and gate each step:
   ```bash
   cd sample-app && npm run build && npm test && npm run lint
   ```

If you created `AGENTS.md` in Module 08, the agent should honor conventions without restating them.

---

## Acceptance checklist

- [ ] `PATCH /tasks/:id` updates `title`, `priority`, and/or `done`
- [ ] Invalid input → `400`; unknown id → `404`; success → `200`
- [ ] New tests cover all three cases and pass
- [ ] `npm run build`, `npm test`, `npm run lint` all green
- [ ] No `any`, no `new RegExp` on user input, conventions followed
- [ ] You completed it in phases with session resets

---

## Final scorecard + reflection

Fill in one last scorecard for the whole capstone, then answer:

1. How many retries did this take vs. the "gamble" task in Module 01?
2. Which lever saved you the most rework?
3. What will you add to `AGENTS.md` so it's free next time?

---

## Top 5 actions : your takeaway

1. **Choose the right model.**
2. **Write clear prompts.**
3. **Split tasks.**
4. **Add deterministic guardrails.**
5. **Maintain concise instructions.**

👉 **Make every token count.**

---

🎉 You've finished the Copilot CLI track. Want the same lessons in the editor? Try the
[VS Code track](../vscode/README.md).
