# CLI · Module 05 — Lever 3: Prompt Engineering 🟡

**Goal:** turn vague asks into **precise prompts with explicit context and stop conditions**, which matters even more in non-interactive one-shots.

> Be precise · add stop conditions · provide context explicitly.

---

## The anatomy of a strong prompt

```text
[INTENT]      What you want, in one sentence.
[CONTEXT]     Which files/facts matter (@path references or stated rules).
[CONSTRAINTS] What NOT to touch; rules to follow.
[DONE WHEN]   The stop condition the agent can verify.
```

A **stop condition** is the biggest single upgrade, it stops the agent from wandering into unrelated changes (which compounds errors and burns tokens). In `copilot -p "..."` one-shots, it's essential because you're not there to interrupt.

---

## Exercise A : Rewrite a weak prompt

Weak:

```text
make the search better
```

Rewrite it for `GET /tasks/search` in `routes.ts`.

<details>
<summary>Sample strong rewrite (as a one-shot)</summary>

```bash
copilot --allow-all-tools --allow-all-paths -p "In sample-app/src/routes.ts, the GET /tasks/search endpoint builds a RegExp directly from the user's q param, allowing ReDoS. Replace it with a safe case-insensitive substring match (includes on lower-cased values). Do not change other endpoints. Done when q=review still returns the 'Review pull request' task and no 'new RegExp' remains in the file."
```

</details>

Run it, then verify the "Done when" clause:

```bash
cd sample-app && npm run build && grep -n "new RegExp" src/routes.ts   # should print nothing
```

---

## Exercise B : Stop conditions prevent scope creep

1. One-shot **without** a stop condition:

   ```bash
   copilot --allow-all-tools --allow-all-paths -p "clean up sample-app/src/tasks.ts"
   ```

   Inspect the diff (`cd sample-app && git diff`). How far did it roam?
2. Revert (`git checkout -- src/tasks.ts`), then one-shot **with** a tight stop condition:

   ```bash
   copilot --allow-all-tools --allow-all-paths -p "In sample-app/src/tasks.ts, add a one-line JSDoc comment above topTasks describing what it returns. Change nothing else. Done when only that comment is added."
   ```

Compare scope and correction effort.

---

## Exercise C : Make context explicit, not assumed

State conventions instead of hoping the agent infers them:

```text
Follow these rules: 2-space indentation; prefer const; no `any`; functions return values rather than throwing for expected cases.
```

The model can't read your team wiki, explicit beats implicit.

---

## Prompt checklist

- [ ] One clear intent
- [ ] The *right* files referenced (not too many)
- [ ] Explicit constraints / "don't touch X"
- [ ] A verifiable **Done when** stop condition

---

## Expected outcome

You can write precise, bounded prompts (especially for one-shots) and have seen stop conditions shrink scope creep and rework.

➡️ Next: [06 — Lever 4: Workflow design](06-workflow-design.md)
