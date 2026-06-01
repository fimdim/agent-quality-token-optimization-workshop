# CLI · Module 06 — Lever 4: Workflow Design 🟡

**Goal:** split a non-trivial change into **Research → Plan → Implement**, each in its own clean session, and see why this beats one-shot "do everything."

> Benefits: cleaner context · better quality · lower token usage. Shorter chains keep `p^n` high (see [compounding error](../../concepts/c2-compounding-error.md)).

---

## The task

Refactor the sample app so business logic, routing, and storage are cleanly separated, and add validation, **without breaking existing tests**. Too big for one prompt.

---

## Phase 1 : Research (read-only)

1. Start `copilot`. Capable model. Ask for analysis only, and **save it to a file**:

   ```text
   Don't change code. Map how a POST /tasks request flows through @sample-app/src/routes.ts, @sample-app/src/tasks.ts, @sample-app/src/store.ts, and @sample-app/src/types.ts. List the responsibilities currently mixed together and the smallest set of changes to separate routing, validation, business logic, and storage. Write your analysis to RESEARCH.md.
   ```

You now have `RESEARCH.md` as a durable artifact (and it cost one focused session).

---

## Phase 2 : Plan (still read-only, fresh session)

1. Exit `/clear` for a clean window, or use `/plan`. Then:

   ```text
   Read @RESEARCH.md and produce PLAN.md: a numbered checklist of small, independently testable steps, ordered so tests stay green throughout. Do not write code.
   ```

Review `PLAN.md` and edit it directly if needed, it's cheap to fix a list, expensive to redo code.

If you use `/plan`, point it at `@RESEARCH.md`, then choose option 2 (`Exit plan mode and I will prompt myself`) so you keep the same constraint: produce `PLAN.md`, stay read-only, and do not write code.

---

## Phase 3 : Implement (fresh session, one step at a time)

1. Exit `/clear` again. Then feed **one step**, with only the files it needs:

   ```text
   From @PLAN.md, do step 1 only: extract POST /tasks validation into a validateCreateTask function in a new file sample-app/src/validation.ts, called from @sample-app/src/routes.ts. Keep behavior identical for valid input. Done when `npm run build` passes and existing tests stay green.
   ```

2. After each step, verify in a normal terminal:

   ```bash
   cd sample-app && npm run build && npm test
   ```

   Only advance when green.

---

## Compare against one-shot

In a fresh session, try the whole refactor in a single prompt and compare:

| | Research→Plan→Implement | One-shot |
| --- | --- | --- |
| Tests stayed green throughout? | | |
| Retries / corrections | | |
| Could you review before code? | | |

The phased approach yields reviewable diffs and fewer surprises. Bonus: `RESEARCH.md`/`PLAN.md` are reusable artifacts.

---

## Expected outcome

You ran a real change through Research → Plan → Implement with session resets between phases and can explain how shorter, verified steps stop errors from compounding.

➡️ Next: [07 — Lever 5: Deterministic controls](07-deterministic-controls.md)
