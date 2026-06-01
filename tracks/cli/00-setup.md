# CLI · Module 00 — Setup & ROI Mindset 🟢

**Goal:** get the Copilot CLI working, run the sample app, and adopt the workshop's core principle before your first prompt.

> **Don't minimize tokens, maximize their value.** Better quality → fewer retries → lower total cost.

---

## 1. Verify the CLI

```bash
copilot --version
```

Then start a session and authenticate if needed:

```bash
copilot
```

Inside the session:

```text
/login        # if not already signed in
/help         # see available slash commands
```

Ask a trivial question to confirm it responds:

```text
What can you help me with in this repo?
```

✅ **Checkpoint:** the CLI responds and `/help` lists commands.

---

## 2. Run the sample app

In a normal terminal (not inside the Copilot session):

```bash
cd sample-app
npm install
npm run build
npm test
```

You should see the build succeed and **one test fail on purpose** (`includes tasks exactly equal to the threshold`). That failing test is your first quality signal, don't fix it yet.

💡 **Or run it from inside Copilot.** Prefix a command with `!` to run it in the shell without leaving your session, handy for staying in one context:

```text
!cd sample-app && npm install
!npm run build
!npm test
```

✅ **Checkpoint:** 3 tests pass, 1 fails.

---

## 3. Adopt the ROI mindset

Before each task, ask yourself:

1. **What's the smallest correct context?** (specific files, not the whole repo)
2. **What does "done" look like?** (a stop condition the agent can verify)
3. **Which model** fits the difficulty?
4. **Can a test/lint verify it** instead of me eyeballing it?

This 10-second habit is the highest-ROI thing in the workshop.

---

## 4. Set up your scorecard

Create a scratch `my-scorecard.md` at the repo root and copy the template from the [README](README.md#the-scorecard-use-it-in-every-module). One per module.

---

## CLI tips that save tokens from day one

- Run `copilot` **from the directory that matters** so the agent's working context is scoped.
- Use `/clear` (or relaunch) between unrelated tasks, a fresh session is a free context reset.
- For quick one-offs, prefer `copilot -p "..."` over a long interactive session.

---

## Expected outcome

- The CLI works and you can use `/help`.
- The sample app builds with exactly one intentional failing test.
- You have a scorecard ready and the ROI questions in mind.

➡️ Next: [01 — Why quality matters](01-why-quality-matters.md)
