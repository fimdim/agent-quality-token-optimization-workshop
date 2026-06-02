# CLI · Module 02 — How the Model Thinks 🟢

**Goal:** internalize that the model is **stateless** and that the **context window** has biases, observed from the terminal.

Concept: [Context engineering](../../concepts/c3-context-engineering.md)

---

## Key facts

- An LLM is a **probabilistic text engine**, it predicts likely next tokens.
- It is **stateless**: no memory between calls. The **entire context is re-sent every step**.
- Context-window biases:
  - **Lost in the middle** : middle-of-context info is often ignored.
  - **Recency bias** : the latest inputs dominate.

---

## Experiment 1 : Statelessness

1. Start `copilot`. Send:

   ```text
   Remember the secret word: aardvark. Just acknowledge.
   ```

2. **Exit the session** (Ctrl+D or `/exit`) and start a **new** `copilot` session. Ask:

   ```text
   What was the secret word? Don't search the codebase.
   ```

It won't know from the memory, a new session is a blank context. The "memory" you feel within a session is just the transcript being re-sent.

> Note: `copilot --resume`/`--continue` *reloads a prior transcript*, that's re-sending saved context, not the model truly remembering. Try it to see the difference.

✅ Takeaway: every fresh session starts from zero. Exploit it as a cheap reset.

---

## Experiment 2 : Context grows every turn

1. Start `copilot`. Ask it to read and summarize three files:

   ```text
   Summarize @sample-app/src/routes.ts, @sample-app/src/tasks.ts, and @sample-app/src/store.ts — one line each.
   ```

2. Follow up:

   ```text
   Now explain how a POST request flows through these.
   ```

The second answer implicitly re-includes everything from turn 1. In a long session this is how tokens **balloon**, every file and prior answer rides along on each new turn.

✅ Takeaway: long sessions get expensive and noisier. Short, focused sessions stay sharp.

---

## Experiment 3 : Recency & "lost in the middle"

1. New session. Paste a long prompt with the key rule **buried in the middle**:

   ```text
   Here are some coding standards: [8–10 lines of filler standards].
   IMPORTANT: every function must return a Result type, never throw.
   [8–10 more lines of filler standards]
   Now write a TypeScript function that divides two numbers.
   ```

2. Did it honor the buried "never throw" rule?
3. New session: move that rule to the **end**, right before the request. Compare compliance.

   ```text
   Here are some coding standards: [write 8–10 lines of filler standards].
   [write 8–10 more lines of filler standards]
   Now, write a TypeScript function that divides two numbers.
   IMPORTANT: every function must return a Result type, never throw.
   ```

You'll usually get better adherence when the critical rule is **last** (recency) rather than buried in the **middle**.

---

## Expected outcome

You've seen, from the CLI: (1) sessions are stateless, (2) context accumulates per turn, and (3) placement within the window changes compliance, the basis for every lever ahead.

➡️ Next: [03 — Lever 1: Model selection](03-model-selection.md)
