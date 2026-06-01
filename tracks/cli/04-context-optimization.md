# CLI · Module 04 — Lever 2: Context Optimization 🟡

**Goal:** give the CLI agent **only the relevant files** and use session resets to keep context clean.

> **Provide as little as possible, but as much as necessary.** Avoid full-repo context. Reset sessions frequently.

Concept: [Context engineering](../../concepts/c3-context-engineering.md)

---

## How context enters a CLI session

- Files you **reference by path** (e.g. `@sample-app/src/routes.ts`) are pulled in.
- The agent can also **explore** the working directory on its own, which is powerful but can drag in irrelevant files. Scope it by running `copilot` from a **subfolder** when appropriate, or by naming the exact files.

---

## Exercise A : Minimal context wins

Task: add input validation to `POST /tasks`.

1. Decide the minimal set first: likely just `routes.ts` and `types.ts`.
2. Start `copilot` and reference **only** those:

   ```text
   In @sample-app/src/routes.ts, validate the POST /tasks body before creating a task:
   - title: required, non-empty string, max 200 chars
   - priority: required integer 1–5
   Return HTTP 400 with a clear message if invalid. Use the types in    @sample-app/src/types.ts. Don't touch other endpoints. Stop after editing routes.ts.
   ```

Record the scorecard.

---

## Exercise B : Over-stuffed context (anti-pattern)

1. New session **from the repo root**. This time, tell the agent to read broadly:

   ```text
   Read the whole repo including the README and concepts, then add validation to POST /tasks.
   ```

2. Compare: slower? Did it wander into unrelated files or restate things it didn't need?

Extra context isn't free, it dilutes signal and invites "lost in the middle" errors.

---

## Exercise C : Reset discipline + scoping

- After Exercise A, **don't** pile the next unrelated task into the same session. `/clear` or relaunch.
- Try scoping by directory: `cd sample-app && copilot`, now the agent's default exploration is limited to the app, not the whole workshop repo.

> Habit: **one task, one session.** When a task is done, reset.

---

## How to pick the minimal set (heuristic)

1. The file(s) you're changing.
2. The type/interface definitions they depend on.
3. **One** example of the pattern you want imitated (if any).
4. Stop. Add more only if the agent asks or guesses wrong.

---

## Expected outcome

You can assemble a minimal, relevant context from the CLI, you've seen over-context hurt, and you scope sessions by directory and reset between tasks.

➡️ Next: [05 — Lever 3: Prompt engineering](05-prompt-engineering.md)
