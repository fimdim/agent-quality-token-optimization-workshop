# GitHub Copilot CLI Track : Agent Quality & Token Optimization

This track teaches the workshop using the **GitHub Copilot CLI** (`copilot`). Work through the modules in order using the [`sample-app`](../../sample-app/README.md).

> New to the ideas? Do the [tool-agnostic concepts](../../concepts/README.md) first.

---

## Setup checklist

- [ ] Copilot CLI installed (e.g. `npm install -g @github/copilot`) — run `copilot --version`
- [ ] Authenticated: run `copilot`, then `/login`
- [ ] Sample app dependencies installed (`cd sample-app && npm install`)
- [ ] You can start an interactive session by running `copilot` from the repo root

---

## Modules

| # | Module | Level |
| --- | --- | --- |
| 00 | [Setup & ROI mindset](00-setup.md) | 🟢 |
| 01 | [Why quality matters](01-why-quality-matters.md) | 🟢 |
| 02 | [How the model thinks](02-how-the-model-thinks.md) | 🟢 |
| 03 | [Lever 1 — Model selection](03-model-selection.md) | 🟡 |
| 04 | [Lever 2 — Context optimization](04-context-optimization.md) | 🟡 |
| 05 | [Lever 3 — Prompt engineering](05-prompt-engineering.md) | 🟡 |
| 06 | [Lever 4 — Workflow design](06-workflow-design.md) | 🟡 |
| 07 | [Lever 5 — Deterministic controls](07-deterministic-controls.md) | 🟡 |
| 08 | [Advanced controls](08-advanced-controls.md) | 🔴 |
| 09 | [Power-user tips](09-power-user-tips.md) | 🔴 |
| 10 | [Capstone](10-capstone.md) | 🔴 |

---

## CLI essentials you'll use throughout

| Action | How |
| --- | --- |
| Start interactive session | `copilot` (from the repo root) |
| In-session help | `/help` |
| Clear/reset context | `/clear` (or just exit and relaunch — a clean session) |
| Run a command inside Copilot | prefix it with `!`, e.g. `!npm test` (runs in the shell without leaving the session) |
| Check your usage | `/usage` (review AI credits / token usage — run it after every step) |
| Add a file to context | reference it by path in your prompt, e.g. `@sample-app/src/tasks.ts` |
| One-shot (non-interactive) | `copilot -p "your prompt"` |
| Resume a previous session | `copilot --resume` (or `--continue`) |
| Pick a model | model flag/slash command (see Module 03) |

---

## The scorecard (use it in every module)

Exact token counts aren't always shown, so track these **proxy metrics** per task. Run `/usage` **after every step** to watch your AI credit / token consumption move in real time, and keep a `my-scorecard.md` open in another window:

```text
Module: __
Task: ______________________________________

Retries to success       : ___
Agent turns / tool calls  : ___
Manual correction edits   : ___
Guardrails green 1st try? : yes / no
Model used                : ___

/usage output:
  Tokens used             : ___
  AI credits used         : ___

What I'd do differently next time: ______________
```

Watch these numbers **drop** as you apply each lever.

---

## Interactive vs. non-interactive — when to use which

| Mode | Command | Best for |
| --- | --- | --- |
| Interactive | `copilot` | Multi-step work, planning, iterating |
| Non-interactive | `copilot -p "..."` | Scripted one-shots, piping output, CI-like tasks |

Non-interactive mode is a power lever for this workshop, it composes with shell pipes so you can **filter context** and **collapse output** (Module 09).
