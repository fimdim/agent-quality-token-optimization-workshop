# CLI · Module 07 — Lever 5: Deterministic Controls 🟡

**Goal:** add **tests, linters, and security checks** so the agent's work is machine-verified, stopping errors before they compound. In the CLI these double as scriptable gates.

> Deterministic guardrails effectively reset per-step accuracy toward 1.0 by catching mistakes immediately. See [compounding error](../../concepts/c2-compounding-error.md).

---

## Why guardrails change agent economics

An agent that can **run a command and see it fail** fixes its own mistake before it propagates.
Without that signal, a wrong step becomes the foundation for the next, the `p^n` collapse.
Guardrails make agent output trustworthy at scale.

---

## Exercise A : Add a linter (a new guardrail)

The sample app has **no ESLint config**.

```bash
copilot --allow-all-tools --allow-all-paths -p "In sample-app, add ESLint for TypeScript: install needed dev deps, create a flat eslint config that lints src/**/*.ts with recommended TypeScript rules, and make `npm run lint` work. Done when `npm run lint` runs and reports results."

cd sample-app && npm run lint
```

Triage the findings with the agent's help. You've given every future task a new automatic check.

---

## Exercise B : Tests as the contract

```bash
copilot --allow-all-tools --allow-all-paths -p "In sample-app, write Jest + supertest tests in src/routes.test.ts for POST /tasks: valid input -> 201; missing title -> 400; empty title -> 400; priority out of 1–5 -> 400. Use src/tasks.test.ts as a style reference. It's fine if some fail because validation isn't implemented yet."

cd sample-app && npm test
```

Failing tests now **define** the validation to implement. Tests-first turns a fuzzy requirement into a deterministic target.

---

## Exercise C : Security check (fix the ReDoS)

`GET /tasks/search` builds a `RegExp` from raw user input, a DoS vector.

```bash
copilot --allow-all-tools --allow-all-paths -p "In sample-app/src/routes.ts, GET /tasks/search passes user input into new RegExp(), allowing ReDoS. Replace it with a safe case-insensitive substring match. Add a test in src/routes.test.ts that a normal query still works. Done when no `new RegExp` remains and tests pass."

cd sample-app && npm test

curl "http://localhost:3000/tasks/search?q=ship"
```

Start the server with `npm run dev` in another terminal for the curl.

---

## Wire guardrails into your loop

End implementation prompts with a verifiable check, e.g.:

```text
...Done when `npm run build`, `npm test`, and `npm run lint` all pass.
```

That single clause makes the agent self-correct instead of handing you broken work. In CI-like scripts you can even chain them:

```bash
copilot -p "...your task... Done when the build, tests, and lint pass." \
  && cd sample-app && npm run build && npm test && npm run lint
```

---

## Expected outcome

The sample app now has a linter, validation tests, and a fixed security hole, and "green checks" are your default stop condition.

➡️ Next: [08 — Advanced controls](08-advanced-controls.md)
