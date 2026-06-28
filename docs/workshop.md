---
published: false
type: workshop
title: Agent Quality & Token Optimization
short_title: Agent Quality & Token Optimization
description: Hands-on workshop for improving agent output quality while reducing total token waste through better model choice, context, prompts, workflow, and deterministic guardrails.
level: intermediate
authors:
  - Firas Mdimagh
  - Juan Manuel Servera
contacts:
  - "@fimdim"
  - "@jmservera"
duration_minutes: 180
tags: github-copilot, ai-agent, prompt-engineering, context-engineering, token-optimization
navigation_levels: 3
navigation_numbering: false
sections_title:
  - "Agent Quality & Token Optimization : Hands-On Workshop"
  - "Concepts : Tool-Agnostic Mini-Labs"
  - "Track 01 : GitHub Copilot CLI"
  - "Track 02 : VS Code"
---

# Agent Quality & Token Optimization : Hands-On Workshop

## Introduction

> **Core principle:** Don't minimize tokens - **maximize their value.**
> Better quality → fewer retries → lower total cost.

This workshop turns the _Agent Quality & Token Optimization_ workshop into a set of **hands-on labs**. You will not just read about the techniques, you will _practice_ them and **measure** the difference they make.

## Run in GitHub Codespaces (zero local setup)

The fastest way to start is a Codespace, Node.js, the sample app dependencies, and the Copilot extensions are all pre-configured by [.devcontainer/devcontainer.json](https://github.com/fimdim/sample-app/blob/main/.devcontainer/devcontainer.json).

This workshop uses [fimdim/sample-app](https://github.com/fimdim/sample-app): a tiny TypeScript + Express task API. It works well enough to run, but it contains planted problems that you will discover and fix during the workshop. Do not fix them ahead of time; each module asks you to drive the agent to find and resolve them.

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/fimdim/sample-app)

1. Click the badge (or **Code ▸ Codespaces ▸ Create codespace**).
2. Wait for the container to build, `npm ci` runs automatically at the repo root.
3. Open a terminal and verify: `npm run build && npm test`
   (the build passes; **one** test fails on purpose, that's your first exercise).

> Prefer local? Any machine with **Node.js 20+** works too, see the track setup module.

## Who this is for

A mixed audience, from developers new to AI agents through to experienced Copilot users.
Modules are ordered by increasing difficulty. Each module clearly marks its level:

| Badge | Level        | Meaning                                   |
| ----- | ------------ | ----------------------------------------- |
| 🟢    | Beginner     | Safe to do with no prior agent experience |
| 🟡    | Intermediate | Assumes you've done the beginner modules  |
| 🔴    | Advanced     | Power-user techniques, deeper config      |

## Two tracks — pick one (or do both)

The workshop ships as **two fully separate tracks** covering the same concepts with
tool-native instructions:

| Track                  | Tool                                        | Start here                                           |
| ---------------------- | ------------------------------------------- | ---------------------------------------------------- |
| **VS Code**            | GitHub Copilot Chat / Agent mode in VS Code | VS Code track          |
| **GitHub Copilot CLI** | `copilot` command-line agent in a terminal  | GitHub Copilot CLI track |

Both tracks share:

- `concepts` : short, **tool-agnostic** thinking exercises (no tool required).
- [`sample-app`](https://github.com/fimdim/sample-app) : a small, deliberately imperfect TypeScript API you will
  improve throughout the labs. It lives in its own repo: [github.com/fimdim/sample-app](https://github.com/fimdim/sample-app).

> You can complete the **concepts** with pen and paper. The **track modules** use the
> sample app so your prompts have something real to work on.

## Workshop structure

The workshop has three parts; the labs follow the same arc:

1. **Why agent quality matters** → Modules 00–01
2. **LLM & agent fundamentals** → Module 02
3. **Optimization techniques** (the 5 levers) → Modules 03–07
4. **Advanced controls & power-user habits** → Modules 08–09
5. **Capstone** → Module 10

| #   | Module                           | Concept                                       | Level |
| --- | -------------------------------- | --------------------------------------------- | ----- |
| 00  | Setup & ROI mindset              | Maximize token value                          | 🟢    |
| 01  | Why quality matters              | Agent ROI + compounding error                 | 🟢    |
| 02  | How the model "thinks"           | Stateless LLM, context window                 | 🟢    |
| 03  | Lever 1 : Model selection        | Right model for the job                       | 🟡    |
| 04  | Lever 2 : Context optimization   | As little as possible, as much as necessary   | 🟡    |
| 05  | Lever 3 : Prompt engineering     | Precise prompts + stop conditions             | 🟡    |
| 06  | Lever 4 : Workflow design        | Research → Plan → Implement                   | 🟡    |
| 07  | Lever 5 : Deterministic controls | Tests, linters, security gates                | 🟡    |
| 08  | Advanced controls                | Instructions, agents, skills, MCP, sub-agents | 🔴    |
| 09  | Power-user tips                  | Scripting, filtering, usage analysis          | 🔴    |
| 10  | Capstone                         | Put all 5 levers together                     | 🔴    |

## Prerequisites

**Common**

- [Node.js 20+](https://nodejs.org/) and npm (for the sample app)
- [Git](https://git-scm.com/)
- A GitHub account with **GitHub Copilot** enabled
- The [`sample-app`](https://github.com/fimdim/sample-app) repository — clone it from [github.com/fimdim/sample-app](https://github.com/fimdim/sample-app), or use the Codespace (which already includes it)

**VS Code track**

- [Visual Studio Code](https://code.visualstudio.com/)

**CLI track**

- [GitHub Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/about-copilot-cli) installed
  (`npm install -g @github/copilot` or the official installer) and authenticated
  (`copilot` then `/login`).

> Verify your setup in **Module 00** of your chosen track before continuing.

## How to measure "quality" without raw token counts

Throughout the labs you'll use these **proxy metrics** to make the abstract idea of "token value" concrete:

- **Retries to success** : how many times you had to re-prompt before the result was correct.
- **Turns / tool calls** : how many round-trips the agent took.
- **Correction edits** : how many manual fixes you made afterward.
- **Guardrail signal** : did tests / lint / type-check pass on the first agent attempt?

Lower numbers = higher token value. You'll record these in a simple scorecard in each module.

## The 5 levers at a glance

```text
1. Model selection       → large = plan/debug · medium = implement · small = trivial · Auto by default
2. Context optimization  → only relevant files · reset sessions often
3. Prompt engineering    → be precise · add stop conditions · supply context explicitly
4. Workflow design       → Research → Plan → Implement (separate, clean contexts)
5. Deterministic control → tests · linters · security checks to stop compounding errors
```

## Top 5 actions (the takeaway you should leave with)

1. Choose the right model.
2. Write clear prompts.
3. Split tasks.
4. Add deterministic guardrails.
5. Maintain concise instructions.

> **→ Make every token count.**

---

# Concepts : Tool-Agnostic Mini-Labs

## Introduction

These three short exercises build the **mental models** behind the workshop. They need no
tools, just thinking, a calculator, and a couple of minutes each. Do them before (or
alongside) your chosen track.

| #   | Concept                                          | Section                       | Time    |
| --- | ------------------------------------------------ | ----------------------------- | ------- |
| C1  | Agent ROI           | Agent ROI model               | ~5 min  |
| C2  | Compounding error   | Compounding error problem     | ~5 min  |
| C3  | Context engineering | Context engineering & windows | ~10 min |

> Each section ends with an **Expected takeaway** so you can self-check.

## C1 : Agent ROI 🟢

> **Agent ROI = Value of Output ÷ Token Cost**
>
> Key insight : _increasing quality often reduces token spend._

The naive reaction to usage-based billing is "use fewer tokens." This exercise shows why
that's the wrong optimization target.

> 💡 **How tokens map to cost.** GitHub Copilot prices every model **per 1 million tokens**,
> then converts that into **AI credits** (1 AI credit = $0.01 USD). So a model's rate of, say,
> $2.00 per 1M input tokens = **200 AI credits per 1M tokens**. We'll keep counting in
> **tokens** below, since tokens are the thing you actually control.
> See [Models and pricing for GitHub Copilot](https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing).

### The "agent gambling" anti-pattern

A common failure loop:

1. Write a **weak prompt** with **minimal context**.
2. Get a mediocre result.
3. **Retry** until something works.

Each retry re-sends the prompt, the files, and the growing conversation, so the cheap-looking first prompt quietly becomes the _most expensive_ path to the answer.

### Exercise

Imagine two developers solving the same task with the **same model**.

#### Developer A : "just retry"

| Attempt | Tokens sent | Outcome                 |
| ------- | ----------- | ----------------------- |
| 1       | 3,000       | Wrong — too vague       |
| 2       | 5,000       | Wrong — missing context |
| 3       | 7,000       | Wrong — agent guessed   |
| 4       | 9,000       | ✅ Finally correct      |

#### Developer B : "invest up front"

| Attempt | Tokens sent | Outcome                                       |
| ------- | ----------- | --------------------------------------------- |
| 1       | 6,000       | ✅ Correct (clear prompt + the 2 right files) |

**Your turn — fill in the blanks:**

1. Total tokens for Developer A = `3,000 + 5,000 + 7,000 + 9,000` = **\_\_** Tokens → **\_\_** AI credits
2. Total tokens for Developer B = **\_\_** Tokens → **\_\_** AI credits
3. If both produce the same correct output (same "Value of Output"), whose **ROI is higher**, and by roughly what factor on cost?

<details>
<summary>Answer</summary>

1. Developer A = **24,000 tokens → 4.8 AI credits** ($0.048).
2. Developer B = **6,000 tokens → 1.2 AI credits** ($0.012).
3. Same value of output, but A spent **4× the tokens** (and 4× the AI credits). Developer B's ROI is **~4× higher**, purely by investing a little more effort into the _first_ prompt. The "cheaper" first prompt was the more expensive strategy.

</details>

### Reflect

- Where in your own work do you "gamble", retrying instead of improving the prompt?
- **"Don't minimize tokens, maximize their value."** A 6,000-token prompt
  that works once beats a 3,000-token prompt you run four times.

## C2 : The Compounding Error Problem 🟢

> Multi-step agent workflows **amplify** errors. Per-step accuracy that looks "good enough"
> collapses over many steps.

This is the single most important reason quality matters _more_ for agents than for one-shot chat.

### The math

If each step succeeds independently with probability `p`, then completing `n` steps in a row succeeds with probability:

$$P_{\text{success}} = p^{\,n}$$

That exponent is brutal. Examples:

| Per-step accuracy | After 50 steps ($p^{50}$) |
| ----------------- | ------------------------- |
| 99%               | ~**61%**                  |
| 95%               | ~**8%**                   |

A 4-point drop in per-step accuracy (99% → 95%) turns a _probably fine_ workflow into a _almost certainly broken_ one.

### Exercise

Use $P = p^{n}$ (a calculator helps).

1. At **p = 0.90**, what is the success rate after **n = 10** steps?
2. At **p = 0.90**, what is it after **n = 50** steps?
3. A teammate says "my agent is 98% reliable per step, that's basically perfect." Over a **30-step** refactor, what's the end-to-end success rate?

<details>
<summary>Answers</summary>

1. $0.90^{10} \approx 0.349$ → about **35%**.
2. $0.90^{50} \approx 0.005$ → about **0.5%**, essentially never.
3. $0.98^{30} \approx 0.545$ → about **55%**, barely a coin flip. "98% per step" is _not_ basically perfect once you chain 30 steps.

</details>

### Why this changes how you work

Two ways to keep $p^n$ high:

- **Raise `p`** — better model choice, cleaner context, precise prompts, guardrails. (Levers 1–3 and 5.)
- **Lower `n`** — split a giant task into short, independently-verified phases so errors can't silently compound. (Lever 4: Research → Plan → Implement, plus frequent session resets.)

Deterministic guardrails (tests, linters, type-checks) effectively **reset `p` back toward 1.0** after each step by catching errors before they propagate, which is exactly why Module 07 exists.

### Expected takeaway

Quality compounds **exponentially**. Small per-step improvements and shorter chains produce huge swings in whether the whole task succeeds. "Good enough per step" is a trap.

## C3 : Context Engineering 🟢

> **Provide as little as possible, but as much as necessary.**

The model is a **stateless, probabilistic text engine**. It has no memory between calls, the _entire_ context is re-sent on every step. What you put in that context window (and what you leave out) determines quality.

### The two failure modes

| Too little context                     | Too much context                        |
| -------------------------------------- | --------------------------------------- |
| Model **hallucinates** missing details | Relevant signal is **buried in noise**  |
| Invents APIs, file names, behavior     | "Lost in the middle" — key info ignored |
| Confident but wrong                    | Slower, pricier, _and_ often wrong      |

The goal is the **narrow band in the middle**: exactly the files and facts needed, nothing more.

### Two context-window pitfalls

- **Lost in the middle** : models attend most to the **start** and **end** of a long context; information in the middle is frequently ignored.
- **Recency bias** : the model favors the **latest** inputs, so stale or contradictory earlier turns get over-weighted or forgotten.

**Best practice:** _reset sessions often_ and _split tasks_ so each context stays short and relevant.

### Exercise A : Trim the context

You ask an agent to "add input validation to the `createTask` endpoint." Below is everything you _could_ attach. Mark each ✅ **include** or ❌ **exclude**.

| Item                                           | Include? |
| ---------------------------------------------- | -------- |
| `routes/tasks.ts` (contains `createTask`)      |          |
| The project's `validation`/schema utility file |          |
| `README.md` (project intro & badges)           |          |
| The entire `node_modules/` tree                |          |
| An example of an existing validated endpoint   |          |
| The CI workflow YAML                           |          |
| The `Task` type/interface definition           |          |

<details>
<summary>Suggested answer</summary>

| Item                                           | Include? |
| ---------------------------------------------- | -------- |
| `routes/tasks.ts` (contains `createTask`)      |    ✅   |
| The project's `validation`/schema utility file |    ✅   |
| `README.md` (project intro & badges)           |    ❌   |
| The entire `node_modules/` tree                |    ❌   |
| An example of an existing validated endpoint   |    ✅   |
| The CI workflow YAML                           |    ❌   |
| The `Task` type/interface definition           |    ✅   |

</details>

### Exercise B : Order matters

You have a long session. The crucial constraint is _"never log request bodies, they contain PII."_ Where should it live to survive **lost-in-the-middle** and **recency bias**?

- (a) Buried in turn 3 of a 20-turn chat
- (b) In a persistent instructions file **and** restated in your latest prompt
- (c) Said once at the very start and never repeated

<details>
<summary>Answer</summary>

**(b).** Persistent instructions keep it always-present (it rides at a stable position every call), and restating it in the latest prompt exploits recency bias _in your favor_. Option (c) gets lost as the session grows; (a) sits in the ignored middle.

</details>

### Expected takeaway

You are an **editor of context**, not a hoarder. Curate the minimal relevant set, put critical constraints where the model actually looks (start/end + persistent instructions), and reset often so the window stays clean.

---

# Track 01 : GitHub Copilot CLI

## Introduction

This track teaches the workshop using the **GitHub Copilot CLI** (`copilot`). Work through the modules in order using the [`sample-app`](https://github.com/fimdim/sample-app).

> New to the ideas? Do the tool-agnostic concepts first.

### Setup checklist

- [ ] Copilot CLI installed (e.g. `npm install -g @github/copilot`) — run `copilot --version`
- [ ] Authenticated: run `copilot`, then `/login`
- [ ] Sample app dependencies installed (`cd sample-app && npm install`)
- [ ] You can start an interactive session by running `copilot` from the repo root

### Modules

| # | Module | Level |
| --- | --- | --- |
| 00 | Setup & ROI mindset | 🟢 |
| 01 | Why quality matters | 🟢 |
| 02 | How the model thinks | 🟢 |
| 03 | Lever 1 — Model selection | 🟡 |
| 04 | Lever 2 — Context optimization | 🟡 |
| 05 | Lever 3 — Prompt engineering | 🟡 |
| 06 | Lever 4 — Workflow design | 🟡 |
| 07 | Lever 5 — Deterministic controls | 🟡 |
| 08 | Advanced controls | 🔴 |
| 09 | Power-user tips | 🔴 |
| 10 | Capstone | 🔴 |

### CLI essentials you'll use throughout

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

### The scorecard (use it in every module)

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

### Interactive vs. non-interactive — when to use which

| Mode | Command | Best for |
| --- | --- | --- |
| Interactive | `copilot` | Multi-step work, planning, iterating |
| Non-interactive | `copilot -p "..."` | Scripted one-shots, piping output, CI-like tasks |

Non-interactive mode is a power lever for this workshop, it composes with shell pipes so you can **filter context** and **collapse output** (Module 09).

## CLI · Module 00 — Setup & ROI Mindset 🟢

**Goal:** get the Copilot CLI working, run the sample app, and adopt the workshop's core principle before your first prompt.

> **Don't minimize tokens, maximize their value.** Better quality → fewer retries → lower total cost.

### 1. Verify the CLI

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

### 2. Run the sample app

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

### 3. Adopt the ROI mindset

Before each task, ask yourself:

1. **What's the smallest correct context?** (specific files, not the whole repo)
2. **What does "done" look like?** (a stop condition the agent can verify)
3. **Which model** fits the difficulty?
4. **Can a test/lint verify it** instead of me eyeballing it?

This 10-second habit is the highest-ROI thing in the workshop.

### 4. Set up your scorecard

Create a scratch `my-scorecard.md` at the repo root and copy the template from the README. One per module.

### CLI tips that save tokens from day one

- Run `copilot` **from the directory that matters** so the agent's working context is scoped.
- Use `/clear` (or relaunch) between unrelated tasks, a fresh session is a free context reset.
- For quick one-offs, prefer `copilot -p "..."` over a long interactive session.

### Expected outcome

- The CLI works and you can use `/help`.
- The sample app builds with exactly one intentional failing test.
- You have a scorecard ready and the ROI questions in mind.

➡️ Next: 01 — Why quality matters

## CLI · Module 01 — Why Quality Matters 🟢

**Goal:** feel the "agent gambling" anti-pattern in the terminal, then do it right, and compare scorecards.

Concepts: Agent ROI ·
Compounding error

### Part A : Gamble on purpose (the wrong way)

1. Start a fresh session from the repo root: `copilot`
2. Give it a deliberately weak, context-free prompt:

   ```text
   the tasks thing is broken, fix it
   ```

3. Respond to any questions with equally vague nudges ("still broken", "nope"). **Stop after 3 retries** even if unsolved.

   `Note: Part A can occasionally succeed on the first shot, but it usually burns more tokens/credits because the agent is guessing.`

Record the scorecard for Part C.

### Part B : Invest up front (the right way)

1. Exit and relaunch (or `/clear`) for a **clean session**.
2. Use a precise prompt that names the file, the bug, and a **stop condition**:

   ```text
   In @sample-app/src/tasks.ts, the test "includes tasks exactly equal to the threshold" (in @sample-app/src/tasks.test.ts) is failing. filterByMinPriority should treat minPriority as INCLUSIVE (>=), not exclusive (>). Fix only that function, then tell me to run `npm test` and stop. Do not change anything else.
   ```

3. In a normal terminal: `cd sample-app && npm test` → expect **4/4 pass**.

Record the scorecard for Part C.

### Part C : Compare

| Metric | Part A (gamble) | Part B (invest) |
| --- | --- | --- |
| Tokens | | |
| AI Credits | | |
| Retries to success | | |
| Agent turns | | |
| Tests green? | | |

Part B almost always wins on every axis, fewer tokens *and* a correct result. The "bigger" first prompt was the cheaper path. That's the ROI principle.

### One-shot variant (bonus)

Try the same correct fix as a single non-interactive command and compare the effort:

```bash
copilot --allow-all-tools --allow-all-paths -p "update tasks file"
cd sample-app && npm test
```

The extra flags avoid non-interactive permission blocks when the command needs to edit files.

A well-specified one-shot can solve a clear task in a single, cheap call.

### Compounding-error tie-in

Part A failed because the agent had to *guess* several things in a row (which file, which bug, how to verify). Each guess is a step with `p < 1`, and `p^n` collapses fast. Part B removed the guesses.

### Expected outcome

Two scorecards proving that up-front context + a stop condition beats retry-until-it-works.

➡️ Next: 02 — How the model thinks

## CLI · Module 02 — How the Model Thinks 🟢

**Goal:** internalize that the model is **stateless** and that the **context window** has biases, observed from the terminal.

Concept: Context engineering

### Key facts

- An LLM is a **probabilistic text engine**, it predicts likely next tokens.
- It is **stateless**: no memory between calls. The **entire context is re-sent every step**.
- Context-window biases:
  - **Lost in the middle** : middle-of-context info is often ignored.
  - **Recency bias** : the latest inputs dominate.

### Experiment 1 : Statelessness

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

### Experiment 2 : Context grows every turn

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

### Experiment 3 : Recency & "lost in the middle"

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

### Expected outcome

You've seen, from the CLI: (1) sessions are stateless, (2) context accumulates per turn, and (3) placement within the window changes compliance, the basis for every lever ahead.

➡️ Next: 03 — Lever 1: Model selection

## CLI · Module 03 — Lever 1: Model Selection 🟡

**Goal:** match model size to task difficulty from the CLI.

> **Rule of thumb:** large = planning/debugging · medium = implementation · small = simple tasks · **Auto by default**.

Suggested starting point from [GitHub's model comparison page](https://docs.github.com/en/copilot/reference/ai-models/model-comparison):

- **Deep reasoning/debugging (large):** `GPT-5.5`, `GPT-5.4`, `Claude Opus 4.7`, `Gemini 2.5 Pro`
- **General implementation (medium):** `GPT-5 mini`, `GPT-4.1`, `Claude Sonnet 4.6`
- **Simple/repetitive tasks (small/fast):** `Claude Haiku 4.5`, `Gemini 3 Flash`

Pick one available in your org/plan. If a model isn't available, choose the closest option in the same category.

### Selecting a model in the CLI

Model selection varies by CLI version. Check what your install supports:

```bash
copilot --help        # look for a model flag, e.g. --model
```

Inside a session, run `/help` and look for a model command (often `/model`). Use whichever your version exposes. If neither exists, your CLI uses an automatic default, that's fine; do the exercises by comparing **task difficulty** and noting outcomes.

```bash
# Example shapes (confirm against your version):
copilot --model <large-model> -p "..."
# or, inside a session:
/model
```

Examples:

```bash
copilot --model "GPT-5.5" -p "..."          # deep reasoning/debugging
copilot --model "GPT-5 mini" -p "..."       # general coding
copilot --model "Claude Haiku 4.5" -p "..." # quick/simple edits
```

### Exercise A : A "planning/debugging" task (use a large model)

1. Start a session with a **capable** model (for example: `GPT-5.5`, `GPT-5.4`, `Claude Opus 4.7`, or `Gemini 2.5 Pro`). Don't let it edit yet:

   ```text
   Don't change code. Read @sample-app/src/tasks.ts and @sample-app/src/tasks.test.ts and explain why the "exactly equal to the threshold" test fails and exactly what the fix is. Be specific about the comparison operator.
   ```

Record: did it pinpoint `>` vs `>=`? How clear was the reasoning?

### Exercise B : A "simple" task (use a small/fast model)

1. New session with a **smaller/faster** model (for example: `Claude Haiku 4.5`, `Gemini 3 Flash`, or another fast model in your list) (or a one-shot):

   ```bash
   copilot --model <small-model> -p "In sample-app/src/tasks.ts, change the comparison in filterByMinPriority from > to >=. Nothing else."
   ```

2. `cd sample-app && npm test` → expect 4/4 green.

A small model handles a one-line mechanical edit perfectly, cheaper and faster.

### Exercise C : Compare (mismatch on purpose)

- Ask the **small** model to do Exercise A's *diagnosis*. Did it miss nuance?
- Ask the **large** model to do Exercise B's *one-liner*. Overkill?

| | Diagnosis (hard) | One-liner (easy) |
| --- | --- | --- |
| Large model | quality? speed? | overkill? |
| Small model | missed nuance? | fine? |

**Lesson:** big models earn their cost on ambiguous reasoning; small models win on well-specified mechanical work. The wrong-sized model either wastes value or causes retries.

### When in doubt

Use the **automatic/default** model. Choose deliberately only when the task is clearly very hard (planning/debugging) or clearly trivial (rename, format, one-liner).

### Expected outcome

You've matched three tasks to model choices from the CLI and can justify why right-sizing maximizes token value.

➡️ Next: 04 — Lever 2: Context optimization

## CLI · Module 04 — Lever 2: Context Optimization 🟡

**Goal:** give the CLI agent **only the relevant files** and use session resets to keep context clean.

> **Provide as little as possible, but as much as necessary.** Avoid full-repo context. Reset sessions frequently.

Concept: Context engineering

### How context enters a CLI session

- Files you **reference by path** (e.g. `@sample-app/src/routes.ts`) are pulled in.
- The agent can also **explore** the working directory on its own, which is powerful but can drag in irrelevant files. Scope it by running `copilot` from a **subfolder** when appropriate, or by naming the exact files.

### Exercise A : Minimal context wins

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

### Exercise B : Over-stuffed context (anti-pattern)

1. New session **from the repo root**. This time, tell the agent to read broadly:

   ```text
   Read the whole repo including the README and concepts, then add validation to POST /tasks.
   ```

2. Compare: slower? Did it wander into unrelated files or restate things it didn't need?

Extra context isn't free, it dilutes signal and invites "lost in the middle" errors.

### Exercise C : Reset discipline + scoping

- After Exercise A, **don't** pile the next unrelated task into the same session. `/clear` or relaunch.
- Try scoping by directory: `cd sample-app && copilot`, now the agent's default exploration is limited to the app, not the whole workshop repo.

> Habit: **one task, one session.** When a task is done, reset.

### How to pick the minimal set (heuristic)

1. The file(s) you're changing.
2. The type/interface definitions they depend on.
3. **One** example of the pattern you want imitated (if any).
4. Stop. Add more only if the agent asks or guesses wrong.

### Expected outcome

You can assemble a minimal, relevant context from the CLI, you've seen over-context hurt, and you scope sessions by directory and reset between tasks.

➡️ Next: 05 — Lever 3: Prompt engineering

## CLI · Module 05 — Lever 3: Prompt Engineering 🟡

**Goal:** turn vague asks into **precise prompts with explicit context and stop conditions**, which matters even more in non-interactive one-shots.

> Be precise · add stop conditions · provide context explicitly.

### The anatomy of a strong prompt

```text
[INTENT]      What you want, in one sentence.
[CONTEXT]     Which files/facts matter (@path references or stated rules).
[CONSTRAINTS] What NOT to touch; rules to follow.
[DONE WHEN]   The stop condition the agent can verify.
```

A **stop condition** is the biggest single upgrade, it stops the agent from wandering into unrelated changes (which compounds errors and burns tokens). In `copilot -p "..."` one-shots, it's essential because you're not there to interrupt.

### Exercise A : Rewrite a weak prompt

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

### Exercise B : Stop conditions prevent scope creep

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

### Exercise C : Make context explicit, not assumed

State conventions instead of hoping the agent infers them:

```text
Follow these rules: 2-space indentation; prefer const; no `any`; functions return values rather than throwing for expected cases.
```

The model can't read your team wiki, explicit beats implicit.

### Prompt checklist

- [ ] One clear intent
- [ ] The *right* files referenced (not too many)
- [ ] Explicit constraints / "don't touch X"
- [ ] A verifiable **Done when** stop condition

### Expected outcome

You can write precise, bounded prompts (especially for one-shots) and have seen stop conditions shrink scope creep and rework.

➡️ Next: 06 — Lever 4: Workflow design

## CLI · Module 06 — Lever 4: Workflow Design 🟡

**Goal:** split a non-trivial change into **Research → Plan → Implement**, each in its own clean session, and see why this beats one-shot "do everything."

> Benefits: cleaner context · better quality · lower token usage. Shorter chains keep `p^n` high (see compounding error).

### The task

Refactor the sample app so business logic, routing, and storage are cleanly separated, and add validation, **without breaking existing tests**. Too big for one prompt.

### Phase 1 : Research (read-only)

1. Start `copilot`. Capable model. Ask for analysis only, and **save it to a file**:

   ```text
   Don't change code. Map how a POST /tasks request flows through @sample-app/src/routes.ts, @sample-app/src/tasks.ts, @sample-app/src/store.ts, and @sample-app/src/types.ts. List the responsibilities currently mixed together and the smallest set of changes to separate routing, validation, business logic, and storage. Write your analysis to RESEARCH.md.
   ```

You now have `RESEARCH.md` as a durable artifact (and it cost one focused session).

### Phase 2 : Plan (still read-only, fresh session)

1. Exit `/clear` for a clean window, or use `/plan`. Then:

   ```text
   Read @RESEARCH.md and produce PLAN.md: a numbered checklist of small, independently testable steps, ordered so tests stay green throughout. Do not write code.
   ```

Review `PLAN.md` and edit it directly if needed, it's cheap to fix a list, expensive to redo code.

If you use `/plan`, point it at `@RESEARCH.md`, then choose option 2 (`Exit plan mode and I will prompt myself`) so you keep the same constraint: produce `PLAN.md`, stay read-only, and do not write code.

### Phase 3 : Implement (fresh session, one step at a time)

1. Exit `/clear` again. Then feed **one step**, with only the files it needs:

   ```text
   From @PLAN.md, do step 1 only: extract POST /tasks validation into a validateCreateTask function in a new file sample-app/src/validation.ts, called from @sample-app/src/routes.ts. Keep behavior identical for valid input. Done when `npm run build` passes and existing tests stay green.
   ```

2. After each step, verify in a normal terminal:

   ```bash
   cd sample-app && npm run build && npm test
   ```

   Only advance when green.

### Compare against one-shot

In a fresh session, try the whole refactor in a single prompt and compare:

| | Research→Plan→Implement | One-shot |
| --- | --- | --- |
| Tests stayed green throughout? | | |
| Retries / corrections | | |
| Could you review before code? | | |

The phased approach yields reviewable diffs and fewer surprises. Bonus: `RESEARCH.md`/`PLAN.md` are reusable artifacts.

### Expected outcome

You ran a real change through Research → Plan → Implement with session resets between phases and can explain how shorter, verified steps stop errors from compounding.

➡️ Next: 07 — Lever 5: Deterministic controls

## CLI · Module 07 — Lever 5: Deterministic Controls 🟡

**Goal:** add **tests, linters, and security checks** so the agent's work is machine-verified, stopping errors before they compound. In the CLI these double as scriptable gates.

> Deterministic guardrails effectively reset per-step accuracy toward 1.0 by catching mistakes immediately. See compounding error.

### Why guardrails change agent economics

An agent that can **run a command and see it fail** fixes its own mistake before it propagates.
Without that signal, a wrong step becomes the foundation for the next, the `p^n` collapse.
Guardrails make agent output trustworthy at scale.

### Exercise A : Add a linter (a new guardrail)

The sample app has **no ESLint config**.

```bash
copilot --allow-all-tools --allow-all-paths -p "In sample-app, add ESLint for TypeScript: install needed dev deps, create a flat eslint config that lints src/**/*.ts with recommended TypeScript rules, and make `npm run lint` work. Done when `npm run lint` runs and reports results."

cd sample-app && npm run lint
```

Triage the findings with the agent's help. You've given every future task a new automatic check.

### Exercise B : Tests as the contract

```bash
copilot --allow-all-tools --allow-all-paths -p "In sample-app, write Jest + supertest tests in src/routes.test.ts for POST /tasks: valid input -> 201; missing title -> 400; empty title -> 400; priority out of 1–5 -> 400. Use src/tasks.test.ts as a style reference. It's fine if some fail because validation isn't implemented yet."

cd sample-app && npm test
```

Failing tests now **define** the validation to implement. Tests-first turns a fuzzy requirement into a deterministic target.

### Exercise C : Security check (fix the ReDoS)

`GET /tasks/search` builds a `RegExp` from raw user input, a DoS vector.

```bash
copilot --allow-all-tools --allow-all-paths -p "In sample-app/src/routes.ts, GET /tasks/search passes user input into new RegExp(), allowing ReDoS. Replace it with a safe case-insensitive substring match. Add a test in src/routes.test.ts that a normal query still works. Done when no `new RegExp` remains and tests pass."

cd sample-app && npm test

curl "http://localhost:3000/tasks/search?q=ship"
```

Start the server with `npm run dev` in another terminal for the curl.

### Wire guardrails into your loop

End implementation prompts with a verifiable check, e.g.:

```text
...Done when `npm run build`, `npm test`, and `npm run lint` all pass.
```

That single clause makes the agent self-correct instead of handing you broken work. In CI-like scripts you can even chain them:

```bash
copilot -p "...your task... Done when the build, tests, and lint pass." \
  && cd sample-app && npm run build && npm test && npm run lint
```

### Expected outcome

The sample app now has a linter, validation tests, and a fixed security hole, and "green checks" are your default stop condition.

➡️ Next: 08 — Advanced controls

## CLI · Module 08 — Advanced Controls 🔴

**Goal:** make quality **repeatable** with persistent instructions, custom agents, skills, MCP tools, and sub-agents, so you don't re-explain context every session.

> Persistent instructions · custom agents · skills (dynamic context) · MCP tools (use carefully) · sub-agents for research.

### 1. Persistent instructions (`AGENTS.md` / instructions file)

The Copilot CLI reads project instruction files (commonly `AGENTS.md`, and it also respects `.github/copilot-instructions.md`). The sample app has none, so the agent re-guesses conventions each time. Fix that:

```bash
copilot --allow-all-tools --allow-all-paths -p "Create AGENTS.md in sample-app capturing: TypeScript strict, 2-space indent, prefer const, no `any`; Express routes in src/routes.ts; business logic in src/tasks.ts; validate all request bodies and return 400 on bad input; never build a RegExp from user input; every change must keep `npm run build`, `npm test`, and `npm run lint` green. Keep it concise."
```

Open the file, trim anything bloated (instructions are re-sent every turn, keep them tight).

**Test it:** new session, ask the agent to add a small endpoint. It should follow the rules *without* you restating them. Run `/help` to confirm how your CLI surfaces loaded instructions.

Example prompt to try:

```text
Add POST /tasks/:id/complete. Put routing in src/routes.ts and business logic in src/tasks.ts. Validate request input and return 400 on invalid input. Keep the change minimal and run build, test, and lint.
```

> Keep instructions **concise**, a giant instructions file is itself a context tax.

### 2. Custom agents / saved configurations

Many CLI versions support custom agents or saved prompt configurations. Use this to lock in repeatable behavior, including token discipline. Example: a tiny `tdd-fixer` profile for bounded bug fixes.

```md
---
name: tdd-fixer
description: Smallest safe fix with minimal output.
---

Goal: fix only the reported failure with the smallest safe edit.

Rules:
1. Output max 5 bullets unless asked for more.
2. State the failing check in 1 line.
3. Change only files needed for that failure.
4. Run `npm test`.
5. Stop when green; do not refactor unrelated code.
```

Save that in your CLI's custom-agent location, then launch with `/tdd-fixer`.

Quick test prompt:

```text
Fix only the failing test for task completion; keep the patch minimal and stop when tests pass.
```

Why this helps token efficiency: you pre-commit to short output, minimal edits, and a strict stopping rule.

### 3. Skills : dynamic context loading

Skills let the agent load domain knowledge **only when relevant**, instead of pasting long guidance into every prompt.

Example skill (keep outside core instructions so it loads only when needed):

```md
---
name: api-validation-rules
description: Validation and error-response rules for task endpoints.
---

Use for endpoint edits in `src/routes.ts` and `src/tasks.ts`.

Rules:
1. Validate every request body and route param.
2. Return 400 with a short error message on invalid input.
3. Never build a RegExp from user input.
4. Keep changes minimal and avoid unrelated refactors.
```

Then ask:

```text
/skills list
```

Quick test prompt:

```text
Add POST /tasks/:id/complete. Keep output brief.
```

Why this helps token efficiency: heavy, domain-specific rules are loaded on demand, not carried in every turn.

### 4. MCP tools : powerful, use carefully

The CLI can connect to MCP servers (databases, browsers, issue trackers, etc.). Inspect/manage them (check `/help` for an `/mcp` command or your CLI's MCP config file).

**Caution:** every enabled MCP tool adds tool definitions to the context and can take real actions. Enable only what a task needs; disable the rest. More tools = more tokens + more ways to go wrong. Treat MCP tools like context: as few as necessary.

Example prompts:

```text
/mcp list
```

Use only the GitHub MCP for this task. Disable other MCP tools, then summarize open issues labeled "bug".

Before editing code, confirm which MCP tools are enabled and explain why each one is needed.

### 5. Sub-agents for research

Offload heavy read-only exploration so your main session stays clean. If your CLI exposes a research/sub-agent capability, ask it to "explore the codebase and report how validation is handled." The long exploration runs in its own context; only the **summary** returns, keeping your primary window lean.

If no dedicated sub-agent exists, emulate it: run a **separate** `copilot` session whose only job is to produce `RESEARCH.md`, then feed that summary into your main work.

Example prompts:

```text
Use a research sub-agent to scan `src/` and summarize where request validation happens. Return only: files, patterns, and gaps.
```

```text
Run a sub-agent to compare validation behavior between routes and tests, then give me a 5-bullet action plan.
```

```text
Do read-only exploration in a sub-agent first; after it returns, propose the smallest patch to add POST /tasks/:id/complete.
```

### Expected outcome

The sample app has concise persistent instructions, you've created a reusable agent/persona, and you know when skills, MCP tools, and sub-agents add value vs. noise.

➡️ Next: 09 — Power-user tips

## CLI · Module 09 — Power-User Tips 🔴

**Goal:** exploit the terminal's superpower, **pipes and scripts**, to filter inputs, collapse outputs, and analyze usage. This is where the CLI track shines.

> Use scripts to filter data · optimize CLI outputs · collapse tool calls · analyze usage patterns.

### 1. Filter data *before* it reaches the model

The CLI composes with the shell, so you can hand the agent a **pre-filtered** slice instead of a whole file:

```bash
# Feed only the relevant lines into a one-shot prompt
grep -n "RegExp" sample-app/src/*.ts | copilot -p "Explain the security risk in these lines and how to fix it. Do not edit files."

# Summarize only the failing test output, not the full log
cd sample-app && npm test 2>&1 | tail -n 20 | copilot -p "Why is this test failing and what's the minimal fix? Do not edit files."

# Just the dependency names
node -p "Object.keys(require('./sample-app/package.json').dependencies)" | copilot -p "Are any of these unnecessary for a basic Express API? Do not edit files."
```

You decide what's relevant, the model never wades through noise.

### 2. Keep tool output lean

When the agent runs commands, noisy output is tokens. Prefer quiet commands:

| Noisy | Lean |
| --- | --- |
| `npm test` (full log) | `npm test 2>&1 \| tail -n 20` |
| `cat bigfile.ts` | `sed -n '40,80p' bigfile.ts` |
| `ls -R` | `git ls-files src` |

Tell the agent in your prompt: "run the quietest command that proves it works."

### 3. Collapse long sessions into a summary

When a session grows (and gets pricey), compress instead of extending:

```text
Summarize what we changed and the current state in 5 bullet points.
```

Save that summary, start a **new** session, and paste it as the seed. You've turned a huge
transcript into a few lines, a manual, high-leverage reset that fights "lost in the middle" and
recency bias.

> `copilot --resume` reloads a full transcript; a **summary-seeded new session** is often far cheaper for the same continuity.

**Or let the CLI do it in one command** with `/compact`:

```text
/compact
```

`/compact` compresses your conversation history in place, replacing the long transcript with a summary while keeping you in the same session. The CLI also **auto-compacts** in the background when you approach ~95% of the token limit, so sessions can run almost indefinitely. Use `/context` to see a token-usage breakdown and decide *when* a manual `/compact` is worth it. Press `Esc` to cancel a compaction if you change your mind.

> Rule of thumb: `/compact` to **continue** the same task cheaply; a summary-seeded **new** session to start a clean, unrelated task.

### 4. Script repeatable guardrail loops

Bundle a task with its verification so the agent's work is gated automatically:

```bash
copilot -p "Implement <change> in sample-app. Done when build, tests, and lint pass." \
  && cd sample-app && npm run build && npm test && npm run lint \
  && echo "ALL GREEN" || echo "NEEDS WORK"
```

This is Lever 5 (deterministic controls) expressed as a one-liner.

### 5. Analyze your usage patterns

Review your scorecards:

- Which tasks needed the most retries? Missing context, no stop condition, wrong model?
- Where did you over-stuff context?
- Which guardrail caught the most mistakes?

Promote recurring fixes into `AGENTS.md` (Module 08) so you never pay for that lesson twice. If your CLI exposes usage/billing info (`/help` or account dashboard), correlate big sessions with low-quality outcomes, those are your prime optimization targets.

### Expected outcome

You can pre-filter inputs with pipes, keep output and sessions lean, script guardrail loops,
compress context with `/compact` and use scorecard history to improve your defaults.

➡️ Next: 10 — Capstone

## CLI · Module 10 — Capstone 🔴

**Goal:** combine all five levers to ship one clean, verified feature on the sample app from the terminal, and prove the difference with your scorecard.

### The brief

> Add a **`PATCH /tasks/:id`** endpoint that lets a client update a task's `title`, `priority`, or `done` status. It must validate input, reject unknown IDs with 404, follow project conventions, and keep all checks green.

This touches routing, validation, business logic, and storage, a realistic multi-step change.

### Run it through all five levers

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

### Acceptance checklist

- [ ] `PATCH /tasks/:id` updates `title`, `priority`, and/or `done`
- [ ] Invalid input → `400`; unknown id → `404`; success → `200`
- [ ] New tests cover all three cases and pass
- [ ] `npm run build`, `npm test`, `npm run lint` all green
- [ ] No `any`, no `new RegExp` on user input, conventions followed
- [ ] You completed it in phases with session resets

### Final scorecard + reflection

Fill in one last scorecard for the whole capstone, then answer:

1. How many retries did this take vs. the "gamble" task in Module 01?
2. Which lever saved you the most rework?
3. What will you add to `AGENTS.md` so it's free next time?

### Top 5 actions : your takeaway

1. **Choose the right model.**
2. **Write clear prompts.**
3. **Split tasks.**
4. **Add deterministic guardrails.**
5. **Maintain concise instructions.**

👉 **Make every token count.**

🎉 You've finished the Copilot CLI track. Want the same lessons in the editor? Try the
VS Code track.

---

# Track 02 : VS Code

## VS Code Track — Agent Quality & Token Optimization

This track teaches the workshop using **GitHub Copilot in Visual Studio Code** (Chat and Agent modes). Work through the modules in order, each builds on the last and uses the [`sample-app`](https://github.com/fimdim/sample-app).

> New to the ideas? Do the tool-agnostic concepts first.

### Setup checklist

- [ ] VS Code installed
- [ ] **GitHub Copilot** + **GitHub Copilot Chat** extensions installed and signed in
- [ ] Sample app dependencies installed (`cd sample-app && npm install`)
- [ ] You can open the Chat view (`Ctrl+Alt+I` / `⌃⌘I`) and see the **mode** dropdown (Ask · Plan · Agent) and the **model picker**

### Modules

| # | Module | Level |
| --- | --- | --- |
| 00 | Setup & ROI mindset | 🟢 |
| 01 | Why quality matters | 🟢 |
| 02 | How the model thinks | 🟢 |
| 03 | Lever 1 — Model selection | 🟡 |
| 04 | Lever 2 — Context optimization | 🟡 |
| 05 | Lever 3 — Prompt engineering | 🟡 |
| 06 | Lever 4 — Workflow design | 🟡 |
| 07 | Lever 5 — Deterministic controls | 🟡 |
| 08 | Advanced controls | 🔴 |
| 09 | Power-user tips | 🔴 |
| 10 | Capstone | 🔴 |

### The scorecard (use it in every module)

Because exact token counts aren't always visible, track these **proxy metrics** for each task. Copy this into a notes file and fill it in as you go:

```text
Module: __
Task: ______________________________________

Retries to success      : ___
Agent turns / tool calls : ___
Manual correction edits  : ___
Guardrails green 1st try?: yes / no
Model used               : ___
Tokens / AI credits used : ___

What I'd do differently next time: ______________
```

The whole point of the workshop: watch these numbers **drop** as you apply each lever.

### A note on Chat modes

| Mode | Use it for |
| --- | --- |
| **Ask** | Questions, explanations — no file edits |
| **Plan** | Research and planning: produces a plan/checklist, no code changes |
| **Agent** | Multi-step autonomous work: reads files, edits, runs tasks |

Choosing the right mode is itself an optimization: Ask/Plan for thinking, Agent for doing.

### VS Code essentials you'll use throughout

| Action | How |
| --- | --- |
| Open the Chat view | `Ctrl+Alt+I` / `⌃⌘I` |
| Switch mode | mode dropdown: Ask · Plan · Agent |
| Pick a model | model picker in the Chat input box |
| Add a file to context | type `#` and pick the file |
| Clear/reset context | start a new Chat session |
| Run a command | VS Code terminal (`` Ctrl+` ``) |
| Track your usage | review token / AI credit consumption after each step |

## VS Code · Module 00 — Setup & ROI Mindset 🟢

**Goal:** get Copilot working in VS Code, run the sample app, and adopt the workshop's core principle before you write a single prompt.

> **Don't minimize tokens, maximize their value.** Better quality → fewer retries → lower total cost.

### 1. Verify Copilot

### 1.1 Verify Copilot Chat

1. Open the Chat view: `Ctrl+Alt+I` (Windows/Linux) or `⌃⌘I` (macOS).
2. Confirm you can see:
   - the **mode** dropdown: **Ask · Plan · Agent**
   - the **model picker** (e.g. "Auto", plus named models)
3. In **Ask** mode, type: `What can you help me with in this workspace?` and confirm you get a response.

✅ **Checkpoint:** You received a reply and can switch between Ask/Plan/Agent.

### 1.2 Verify Agent Debug Logs

> Note: The content in [fimdim/sample-app](https://github.com/fimdim/sample-app) enables Agent Debug Log file logging via [.vscode/settings.json](https://github.com/fimdim/sample-app/blob/main/.vscode/settings.json). To disable writing logs to disk, set `"github.copilot.chat.agentDebugLog.fileLogging.enabled": false` in your workspace settings, but you won't be able to follow this step nor see metrics easily.

After your first conversation:

1. Click `Show Agent Debug Logs` in the three-dot menu next to the gear icon in the upper-right corner (Views and more actions...), or open the Command Palette and search for `Open Agent Debug Logs`.
1. Click `Show Agent Debug Logs` in the three-dot menu next to the gear icon in the upper-right corner (Views and more actions...), or open the Command Palette and run `Developer: Open Agent Debug Logs`.
2. Click the conversation title to see metrics such as turns, token usage, tool calls, etc.
3. If you don't see any numbers, restart your VS Code instance.

✅ **Checkpoint:** You can see your token usage for every conversation in the Agent Debug Logs.

> See [Agent Debug Log Panel](https://code.visualstudio.com/docs/agents/agent-troubleshooting/chat-debug-view) for guidance.

### 2. Run the sample app

In a VS Code terminal (`` Ctrl+` ``):

```bash
cd sample-app
npm install
npm run build
npm test
```

You should see the build succeed and **one test fail on purpose** (`includes tasks exactly equal to the threshold`). That failing test is your first quality signal, don't fix it yet.

✅ **Checkpoint:** 3 tests pass, 1 fails.

### 3. Adopt the ROI mindset

Before each task in this workshop, pause and ask:

1. **What's the smallest correct context** for this task? (not the whole repo)
2. **What does "done" look like?** (a stop condition the agent can check)
3. **Which model** fits the difficulty?
4. **Can a test/lint verify it** instead of me eyeballing it?

This 10-second habit is the highest-ROI thing in the whole workshop.

### 4. Set up your scorecard

Create a scratch file `my-scorecard.md` at the repo root (it's just for you). Copy the scorecard template from the track README. You'll fill one in per module.

### VS Code tips that save tokens from day one

- Start a **new Chat** between unrelated tasks, a fresh session is a free context reset.
- Add **only the files that matter**, not whole folders.
- Use **Ask** mode for thinking and **Agent** mode for doing, don't burn Agent turns on a question.

### Expected outcome

- Copilot Chat works and you can switch modes/models.
- The sample app builds, with exactly one intentional failing test.
- You have a scorecard ready and the ROI questions in mind.

➡️ Next: 01 — Why quality matters

## VS Code · Module 01 — Why Quality Matters 🟢

**Goal:** *feel* the cost of the "agent gambling" anti-pattern by deliberately doing it, then doing it right, and compare the scorecards.

Concepts: Agent ROI ·
Compounding error

### Part A : Gamble on purpose (the wrong way)

1. New Chat session, **Agent** mode, model **Auto**.
2. Give it this deliberately weak prompt, **no file context, vague ask**:

   ```text
   the tasks thing is broken, fix it
   ```

3. Whatever it does, resist helping. If it asks questions or guesses wrong, give equally vague nudges ("still broken", "no that's wrong"). **Stop after 3 retries** even if unsolved.

   `Note: Part A can occasionally succeed on the first shot, but it usually burns more tokens/credits because the agent is guessing.`

Record the scorecard for Part C.

### Part B : Invest up front (the right way)

1. **Start a brand-new Chat session** (clean context, important).
2. **Agent** mode. Add precise context: drag and drop [`sample-app/src/tasks.ts`](https://github.com/fimdim/sample-app/blob/main/src/tasks.ts) and [`sample-app/src/tasks.test.ts`](https://github.com/fimdim/sample-app/blob/main/src/tasks.test.ts) into the chat.
3. Use a precise prompt with a **stop condition**:

   ```text
   In sample-app, the test "includes tasks exactly equal to the threshold" is failing. The function filterByMinPriority should treat minPriority as INCLUSIVE (>=), not exclusive (>). Fix only that function, then tell me to run `npm test` and stop. Do not change anything else.
   ```

4. Run `npm test` in the terminal. Confirm **4/4 pass**.

Record the scorecard for Part C.

### Part C : Compare

| Metric | Part A (gamble) | Part B (invest) |
| --- | --- | --- |
| Tokens / AI credits used | | |
| Retries to success | | |
| Agent turns | | |
| Tests green? | | |

**Reflection:** Part B almost always wins on *every* axis, fewer tokens *and* a correct result. That's the ROI principle in action: the "bigger" first prompt was the cheaper path.

### Compounding-error tie-in

Part A failed partly because the agent had to *guess* several things in a row (which file, which bug, how to verify). Each guess is a step with `p < 1`, and `p^n` collapses fast. Part B removed the guesses, pushing each step's `p` toward 1.0.

### Expected outcome

You have two scorecards proving that an up-front investment in context + a stop condition beats retry-until-it-works on retries, turns, *and* correctness.

➡️ Next: 02 — How the model thinks

## VS Code · Module 02 — How the Model Thinks 🟢

**Goal:** internalize that the model is **stateless** and that the **context window** has biases, then observe both directly in VS Code.

Concept: Context engineering

### Key facts

- An LLM is a **probabilistic text engine**, it predicts likely next tokens.
- It is **stateless**: no memory between calls. The **entire context is re-sent every step**.
- The context window has two biases:
  - **Lost in the middle** : info in the middle of a long context is often ignored.
  - **Recency bias** : the latest inputs dominate.

### Experiment 1 : Statelessness

1. New Chat (**Ask** mode). Send:

   ```text
   Remember the secret word: aardvark. Just acknowledge.
   ```

2. Now **open a brand-new Chat session** and ask:

   ```text
   What was the secret word? Don't search the codebase.
   ```

It won't know, the new session is a blank context. Memory you *feel* in a session is just the **transcript being re-sent**, not the model remembering.

✅ Takeaway: every new session starts from zero. That's a feature you'll exploit (cheap resets).

### Experiment 2 : Context grows every turn

1. New Chat (**Agent** mode). Ask it to read three files (add [`sample-app/src/routes.ts`](https://github.com/fimdim/sample-app/blob/main/src/routes.ts), [`sample-app/src/tasks.ts`](https://github.com/fimdim/sample-app/blob/main/src/tasks.ts), [`sample-app/src/store.ts`](https://github.com/fimdim/sample-app/blob/main/src/store.ts)) and summarize each.
2. Then ask a follow-up: "now explain how a POST request flows through these."

Notice the second answer implicitly re-includes everything from turn 1. In a long session this is how tokens **balloon**, every file and every prior answer rides along on each new turn.

✅ Takeaway: long sessions get expensive *and* noisier. Short, focused sessions stay sharp.

### Experiment 3 : Recency & "lost in the middle"

1. New Chat (**Ask** mode). Paste a long prompt where a key instruction is **buried in the middle**:

   ```text
   Here are some coding standards: [write 8–10 lines of filler standards].
   IMPORTANT: every function must return a Result type, never throw.
   [write 8–10 more lines of filler standards]
   Now, write a TypeScript function that divides two numbers.
   ```

2. See whether it honored the buried "never throw / return a Result" rule.
3. Try again in a new session, but put that rule **last**, right before the request. Compare:

   ```text
   Here are some coding standards: [write 8–10 lines of filler standards].
   [write 8–10 more lines of filler standards]
   Now, write a TypeScript function that divides two numbers.
   IMPORTANT: every function must return a Result type, never throw.
   ```

You'll usually get better compliance when the critical rule is at the **end** (recency) rather than buried in the **middle**.

### Expected outcome

You've seen, hands-on: (1) sessions are stateless, (2) context accumulates per turn, and (3) placement within the window changes compliance. These three facts justify every lever that follows.

➡️ Next: 03 — Lever 1: Model selection

## VS Code · Module 03 — Lever 1: Model Selection 🟡

**Goal:** match model size to task difficulty using the VS Code **model picker**, and feel the tradeoff between capability, speed, and cost.

> **Rule of thumb:** large = planning/debugging · medium = implementation · small = simple tasks · **Auto by default**.

Suggested starting point from [GitHub's model comparison page](https://docs.github.com/en/copilot/reference/ai-models/model-comparison):

- **Deep reasoning/debugging (large):** `GPT-5.5`, `GPT-5.4`, `Claude Opus 4.7`, `Gemini 2.5 Pro`
- **General implementation (medium):** `GPT-5 mini`, `GPT-4.1`, `Claude Sonnet 4.6`
- **Simple/repetitive tasks (small/fast):** `Claude Haiku 4.5`, `Gemini 3 Flash`

Pick one available in your org/plan. If a model isn't available, choose the closest option in the same category.

### The model picker

In the Chat input box there's a model dropdown. You'll typically see **Auto** plus several named models of varying capability. **Auto** lets Copilot route the request, a great default, but choosing deliberately is a skill worth practicing.

### Exercise A : A "planning/debugging" task (use a large model)

The sample app's [`tasks.ts`](https://github.com/fimdim/sample-app/blob/main/src/tasks.ts) has a subtle correctness bug.

1. New Chat, **Ask** mode, pick a **large/most-capable** model.
2. Add [`tasks.ts`](https://github.com/fimdim/sample-app/blob/main/src/tasks.ts) and [`tasks.test.ts`](https://github.com/fimdim/sample-app/blob/main/src/tasks.test.ts).
3. Prompt:

   ```text
   Don't change code yet. Explain why the "exactly equal to the threshold" test fails, and what the correct fix is. Be specific about the comparison operator.
   ```

Record: did it pinpoint `>` vs `>=`? How clear was the reasoning?

### Exercise B : A "simple" task (use a small/fast model)

1. New Chat, **Agent** mode, pick a **smaller/faster** model.
2. Add [`tasks.ts`](https://github.com/fimdim/sample-app/blob/main/src/tasks.ts).
3. Prompt:

   ```text
   Change the comparison in filterByMinPriority from `>` to `>=`. Nothing else.
   ```

4. Run `npm test`. Expect 4/4 green.

A small model is perfectly capable of a one-line mechanical edit, and it's cheaper/faster.

### Exercise C : Compare

Repeat Exercise A's *diagnosis* with a small model, and Exercise B's *one-liner* with a large model. Note in your scorecard:

| | Diagnosis (hard) | One-liner (easy) |
| --- | --- | --- |
| Large model | quality? speed? | overkill? |
| Small model | missed nuance? | fine? |

**Lesson:** big models earn their cost on **ambiguous reasoning**; small models win on **well-specified mechanical** work. Using a big model for a one-liner wastes value; using a tiny model for a gnarly bug causes retries (which costs more overall).

### When in doubt

Leave it on **Auto**. Reach for a specific model when you *know* the task is unusually hard (reasoning/planning/debugging) or unusually trivial (rename, format, one-line change).

### Expected outcome

You've consciously matched three tasks to three model choices and can articulate why the right-sized model maximizes token value.

➡️ Next: 04 — Lever 2: Context optimization

## VS Code · Module 04 — Lever 2: Context Optimization 🟡

**Goal:** practice giving the agent **only the relevant files**, and use session resets to keep context clean.

> **Provide as little as possible, but as much as necessary.** Avoid full-repo context. Reset sessions frequently.

Concept: Context engineering

### Exercise A : Minimal context wins

Task: add input validation to `POST /tasks`.

1. New Chat, **Agent** mode.
2. **First, decide the minimal set.** Which files matter? Likely:
   - [`sample-app/src/routes.ts`](https://github.com/fimdim/sample-app/blob/main/src/routes.ts) (the endpoint)
   - [`sample-app/src/types.ts`](https://github.com/fimdim/sample-app/blob/main/src/types.ts) (the `CreateTaskInput`/`Priority` types)
3. Add **only those two**. Prompt:

   ```text
   In POST /tasks, validate the request body before creating a task:
   - title: required, non-empty string, max 200 chars
   - priority: required integer 1–5
   Return HTTP 400 with a clear message if invalid. Don't touch other endpoints.
   Stop after editing routes.ts and tell me to run the server.
   ```

Record the scorecard.

### Exercise B : Over-stuffed context (anti-pattern)

1. New Chat, **Agent** mode.
2. This time add **a lot** of irrelevant context: the whole `sample-app` folder, the workshop `README.md`, the `concepts/` files, then give the **same** prompt as Exercise A.
3. Compare: was the answer slower? Did it wander into unrelated files? Did it restate things it didn't need?

You'll usually see more drift and noise. Extra context isn't free, it dilutes the signal and invites "lost in the middle" mistakes.

### Exercise C : Reset discipline

1. After finishing Exercise A, **don't** keep piling new unrelated tasks into that session.
2. Start a **fresh Chat** for the next task. Notice how a clean window means you re-supply only what's relevant, and the agent isn't anchored to earlier, now-irrelevant decisions.

> Habit: **one task, one session.** When a task is done, reset.

### How to pick the minimal set (heuristic)

1. The file(s) you're changing.
2. The type/interface definitions they depend on.
3. **One** example of the pattern you want imitated (if any).
4. Stop. Add more only if the agent asks or guesses wrong.

### Expected outcome

You can assemble a minimal, relevant context for a real change, you've seen over-context hurt, and you've adopted the one-task-one-session reset habit.

➡️ Next: 05 — Lever 3: Prompt engineering

## VS Code · Module 05 — Lever 3: Prompt Engineering 🟡

**Goal:** turn vague asks into **precise prompts with explicit context and stop conditions**.

> Be precise · add stop conditions · provide context explicitly.

### The anatomy of a strong prompt

```text
[ROLE/INTENT]  What you want, in one sentence.
[CONTEXT]      Which files/facts matter.
[CONSTRAINTS]  What NOT to touch; rules to follow.
[DONE WHEN]    The stop condition the agent can verify.
```

A **stop condition** is the single biggest upgrade most people can make. It stops the agent from "helpfully" wandering into unrelated changes (which compounds errors and burns tokens).

### Exercise A : Rewrite a weak prompt

Weak prompt:

```text
make the search better
```

Rewrite it for the `GET /tasks/search` endpoint in [`routes.ts`](https://github.com/fimdim/sample-app/blob/main/src/routes.ts). Aim for all four parts above.

<details>
<summary>Sample strong rewrite</summary>

```text
In sample-app/src/routes.ts, the GET /tasks/search endpoint builds a RegExp directly
from the user's `q` query param, which allows ReDoS. Replace the regex matching with a
safe case-insensitive substring match (String.prototype.includes on lower-cased values).
Do not change any other endpoint. Done when: searching `q=review` still returns the
"Review pull request" task and no `new RegExp` remains in the file.
```

</details>

Run it (Agent mode, add only `routes.ts`). Verify the behavior in the "Done when" clause.

### Exercise B : Stop conditions prevent scope creep

1. New Chat, **Agent** mode. Add [`tasks.ts`](https://github.com/fimdim/sample-app/blob/main/src/tasks.ts).
2. Prompt **without** a stop condition:

   ```text
   clean up tasks.ts
   ```

   Observe how far it roams (renames? comments? reformat? touches other files?).
3. New Chat. Same file. Prompt **with** a tight stop condition:

   ```text
   In tasks.ts, add a one-line JSDoc comment above topTasks describing what it returns.
   Change nothing else. Done when only that comment is added.
   ```

Compare scope, edits, and your correction effort.

### Exercise C : Make context explicit, not assumed

Instead of "you know the conventions", state them:

```text
Follow these rules: use 2-space indentation; prefer `const`; no `any`; functions return
values rather than throwing for expected cases.
```

Notice the model can't read your mind or your team wiki, explicit beats implicit every time.

### Prompt checklist (keep handy)

- [ ] One clear intent
- [ ] The *right* files added (not too many)
- [ ] Explicit constraints / "don't touch X"
- [ ] A verifiable **Done when** stop condition

### Expected outcome

You can convert vague requests into precise, bounded prompts, and you've seen stop conditions visibly shrink scope creep and rework.

➡️ Next: 06 — Lever 4: Workflow design

## VS Code · Module 06 — Lever 4: Workflow Design 🟡

**Goal:** split a non-trivial change into **Research → Plan → Implement**, each with its own clean context, and see why this beats one-shot "do everything."

> Benefits: cleaner context · better quality · lower token usage. Shorter chains keep `p^n` high (see compounding error).

### The task

Refactor the sample app so business logic, routing, and storage are cleanly separated, and add proper validation, **without breaking the existing tests**. That's too big for one prompt.

### Phase 1 : Research (Agent mode, read-only by instruction)

1. New Chat, **Agent** mode, capable model.
2. Add [`routes.ts`](https://github.com/fimdim/sample-app/blob/main/src/routes.ts), [`tasks.ts`](https://github.com/fimdim/sample-app/blob/main/src/tasks.ts), [`store.ts`](https://github.com/fimdim/sample-app/blob/main/src/store.ts), [`types.ts`](https://github.com/fimdim/sample-app/blob/main/src/types.ts).
3. Prompt:

   ```text
   Don't change any source code. Map how a POST /tasks request flows through these files and list the responsibilities that are currently mixed together. Identify the smallest set of changes to separate routing, validation, business logic, and storage. Write your analysis to RESEARCH.md.
   ```

Agent mode can write files, so it saves `RESEARCH.md` directly, the "Don't change any source code" instruction keeps it read-only against the app. You now have a durable, reusable research artifact.

### Phase 2 : Plan (Agent mode, read-only by instruction)

1. **New Chat** (reset!). Stay in **Agent** mode. Add `RESEARCH.md` as context.
2. Prompt:

   ```text
   Read RESEARCH.md and write PLAN.md: a numbered checklist of small, independently testable steps, ordered so tests stay green throughout. Don't change any source code yet.
   ```

Agent mode writes `PLAN.md` for you while the instruction keeps it from touching the app. Review `PLAN.md` *before* spending tokens on implementation, it's cheap to fix a list, expensive to redo code.

> **Note:** VS Code also has a dedicated **Plan** mode that's purpose-built for this phase and stays read-only automatically (no "don't change code" reminder needed), but it renders the plan in chat rather than writing a file. We use **Agent** mode in all three phases here so you learn the underlying workflow, Research → Plan → Implement, with explicit control and durable `RESEARCH.md`/`PLAN.md` artifacts. Once the pattern is second nature, reach for Plan mode to do Phase 2 with less ceremony.

### Phase 3 : Implement (Agent mode, one step at a time)

1. **New Chat** (reset again). Switch to **Agent** mode.
2. Add `PLAN.md` plus only the files the first step needs, then prompt **one step**. Example:

   ```text
   From PLAN.md, do step 1 only: extract input validation for POST /tasks into a validateCreateTask function in a new file src/validation.ts, and call it from routes.ts. Keep behavior identical for valid input. Done when `npm run build` passes and existing tests stay green.
   ```

3. Run `npm run build` and `npm test` after **each** step. Only advance when green.

Because the plan lives in `PLAN.md`, the reset doesn't lose it, each Agent step reads the file instead of relying on a discarded chat.

### Compare against one-shot

For contrast, in a fresh session try the *whole* refactor in a single prompt
("separate everything and add validation"). Compare:

| | Research→Plan→Implement | One-shot |
| --- | --- | --- |
| Tests stayed green throughout? | | |
| Retries / corrections | | |
| Could you review before code? | | |

The phased approach almost always produces cleaner diffs you can actually review, with fewer surprises.

### Expected outcome

You ran a real change through Research → Plan → Implement with resets between phases, and you can explain how shorter, verified steps keep error from compounding.

➡️ Next: 07 — Lever 5: Deterministic controls

## VS Code · Module 07 — Lever 5: Deterministic Controls 🟡

**Goal:** add **tests, linters, and security checks** so the agent's work is verified by machines, not vibes, stopping errors before they compound.

> Deterministic guardrails effectively reset per-step accuracy back toward 1.0 by catching mistakes immediately. See compounding error.

### Why guardrails change agent economics

An agent that can **run a test and see red** will fix its own mistake before it propagates. Without that signal, a wrong step silently becomes the foundation for the next step, the classic `p^n` collapse. Guardrails are how you make agent output *trustworthy at scale*.

### Exercise A : Add a linter (a new guardrail)

The sample app has **no ESLint config** (`npm run lint` can't enforce anything yet).

1. New Chat, **Agent** mode. Add [`package.json`](https://github.com/fimdim/sample-app/blob/main/package.json) and [`tsconfig.json`](https://github.com/fimdim/sample-app/blob/main/tsconfig.json).
2. Prompt:

   ```text
   Add ESLint for this TypeScript project: install the needed dev dependencies, create a flat eslint config that lints src/**/*.ts with the recommended TypeScript rules, and make `npm run lint` work. Done when `npm run lint` runs and reports results.
   ```

3. Run `npm run lint`. Fix or triage what it flags (with the agent's help).

You just gave every future agent task a new automatic check.

### Exercise B : Tests as the contract

1. New Chat, **Agent** mode. Add [`routes.ts`](https://github.com/fimdim/sample-app/blob/main/src/routes.ts) and the existing [`tasks.test.ts`](https://github.com/fimdim/sample-app/blob/main/src/tasks.test.ts) as a style reference.
2. Prompt:

   ```text
   Write Jest + supertest tests for POST /tasks covering: valid input returns 201; missing title returns 400; empty title returns 400; priority out of 1–5 returns 400. Put them in src/routes.test.ts. Done when the tests run; it's fine if some fail because validation isn't implemented yet. That's the point.
   ```

3. Run `npm test`. Failing tests now **define** the validation you (or the agent) must make pass. Tests-first turns a fuzzy requirement into a deterministic target.

### Exercise C : Security check (fix the ReDoS)

`GET /tasks/search` builds a `RegExp` from raw user input, a denial-of-service vector.

1. New Chat, **Agent** mode. Add only [`routes.ts`](https://github.com/fimdim/sample-app/blob/main/src/routes.ts).
2. Prompt:

   ```text
   The GET /tasks/search endpoint passes user input straight into new RegExp(), which allows ReDoS. Replace it with a safe case-insensitive substring match. Add a test in src/routes.test.ts that a normal query still works. Done when no `new RegExp` remains and tests pass.
   ```

3. Confirm with `npm test` and a manual `curl "http://localhost:3000/tasks/search?q=ship"`.

Start the server with `npm run dev` in another terminal for the curl.

### Wire guardrails into your loop

From now on, end implementation prompts with a verifiable check, e.g.:

```text
...Done when `npm run build`, `npm test`, and `npm run lint` all pass.
```

That single clause makes the agent self-correct instead of handing you broken work.

### Expected outcome

The sample app now has a linter, validation tests, and a fixed security hole, and you've made "green checks" your default stop condition.

➡️ Next: 08 — Advanced controls

## VS Code · Module 08 — Advanced Controls 🔴

**Goal:** make quality **repeatable** with persistent instructions, custom agents, skills, MCP tools, and sub-agents, so you don't re-explain context every session.

> Tools covered: `copilot-instructions.md` · custom agents · skills (dynamic context) · MCP tools (use carefully) · sub-agents for research.

### 1. Persistent instructions (`.github/copilot-instructions.md`)

The sample app has **no** project instructions, so the agent re-guesses conventions each time. Fix that.

1. New Chat, **Agent** mode.
2. Prompt:

   ```text
   Create .github/copilot-instructions.md for the sample-app. Capture: TypeScript strict, 2-space indent, prefer const, no `any`; Express routes live in src/routes.ts; business logic in src/tasks.ts; validate all request bodies and return 400 on bad input; never build a RegExp from user input; every change must keep `npm run build`, `npm test`, and `npm run lint` green. Keep it concise.
   ```

3. Open the file, trim anything bloated (instructions are re-sent every turn, keep them tight).
4. **Test it:** new Chat, ask the agent to add any new endpoint. Notice it now follows the rules *without* you restating them. That's persistent context working for you.

Example prompt to try:

```text
Add POST /tasks/:id/complete. Put routing in src/routes.ts and business logic in src/tasks.ts. Validate request input and return 400 on invalid input. Keep the change minimal and run build, test, and lint.
```

> Keep instructions **concise**. A 300-line instructions file is itself a context tax.

### 2. Custom agents / saved configurations

Create a focused agent that locks in repeatable behavior, including token discipline. Example: a tiny `tdd-fixer` agent for bounded, test-driven bug fixes.

1. Command Palette → **Chat: New Custom Agent**.
2. Create one named `tdd-fixer` with content like:

```md
---
name: tdd-fixer
description: Smallest safe fix with minimal output.
---

Goal: fix only the reported failure with the smallest safe edit.

Rules:
1. Output max 5 bullets unless asked for more.
2. State the failing check in 1 line.
3. Change only files needed for that failure.
4. Run `npm test`.
5. Stop when green; do not refactor unrelated code.
```

3. Use it to fix any remaining issue in the app and notice the consistent, bounded behavior.

A custom agent is a saved bundle of your best prompt habits, reusable token value. Why this helps token efficiency: you pre-commit to short output, minimal edits, and a strict stopping rule.

Quick test prompt:

```text
Fix only the failing test for task completion; keep the patch minimal and stop when tests pass.
```

### 3. Skills : dynamic context loading

Skills let the agent pull in domain knowledge **only when relevant**, instead of you pasting it every time. Explore what's available:

1. Ask in Chat: `What skills are available and when would each be used?`
2. Note how a skill is loaded **on demand**, this is context engineering at the tooling level: the heavy instructions live in a file and enter the window only when needed.

Example skill file (kept out of core instructions so it loads only when relevant):

```md
---
name: api-validation-rules
description: Validation and error-response rules for task endpoints.
---

Use for endpoint edits in `src/routes.ts` and `src/tasks.ts`.

Rules:
1. Validate every request body and route param.
2. Return 400 with a short error message on invalid input.
3. Never build a RegExp from user input.
4. Keep changes minimal and avoid unrelated refactors.
```

### 4. MCP tools : powerful, use carefully

MCP servers give the agent extra tools (databases, browsers, issue trackers, etc.).

1. Review your MCP configuration (Command Palette → search **MCP**).
2. **Caution:** each enabled MCP tool adds tool definitions to the context and can take real-world actions. Enable only what a task needs; disable the rest. More tools = more tokens + more ways to go wrong.

> Treat MCP tools like context: as few as necessary.

### 5. Sub-agents for research

Offload heavy read-only exploration to a sub-agent so your main session stays clean.

1. Ask the agent to "explore the codebase and report how validation is currently handled" using a sub-agent capability.
2. The sub-agent's *long* exploration happens in its own context; only the **summary** returns to your main session, keeping your primary window lean.

Example prompts:

```text
Use a sub-agent to scan `src/` and summarize where request validation happens. Return only: files, patterns, and gaps.
```

```text
Do read-only exploration in a sub-agent first; after it returns, propose the smallest patch to add POST /tasks/:id/complete.
```

### Expected outcome

The sample app has concise persistent instructions, you've built a reusable custom agent, and you understand when skills, MCP tools, and sub-agents add value vs. add noise.

➡️ Next: 09 — Power-user tips

## VS Code · Module 09 — Power-User Tips 🔴

**Goal:** squeeze more value per token with filtering, collapsed tool output, and usage awareness.

> Use scripts to filter data · optimize outputs · collapse tool calls · analyze usage patterns.

### 1. Filter data *before* it enters the context

Don't make the agent read a giant file to find one thing. Pre-filter in the terminal, then paste only the result.

Examples (VS Code terminal):

```bash
# Only the lines that matter, instead of the whole file
grep -n "RegExp" sample-app/src/*.ts

# Just the dependency names, not the whole package.json
node -p "Object.keys(require('./sample-app/package.json').dependencies)"

# A test summary instead of full output
cd sample-app && npm test 2>&1 | tail -n 20
```

Paste the small result into Chat. You decide what's relevant, not the model wading through noise.

### 2. Keep tool output lean (Agent mode)

When the agent runs commands, **noisy output is tokens**. Prefer commands that emit only what's needed:

| Noisy | Lean |
| --- | --- |
| `npm test` (full log) | `npm test 2>&1 | tail -n 20` |
| `cat bigfile.ts` | `sed -n '40,80p' bigfile.ts` |
| `ls -R` | `git ls-files src` |

Ask the agent in your prompt to "run the quietest command that proves it works."

### 3. Collapse / summarize long sessions

When a session gets long (and expensive), don't keep extending it:

- Ask: `Summarize what we changed and the current state in 5 bullet points.`
- Copy that summary, **start a new Chat**, and paste it as the seed. You've compressed a huge transcript into a few lines, a manual, high-leverage context reset.

This directly fights "lost in the middle" and recency bias from long histories.

> **`/compact` works here too.** Type `/compact` in the Chat input to compress the current conversation in place. Copilot also **auto-summarizes** older turns as a conversation grows. Use `/compact` to keep working the same task cheaply, and a **New Chat** (`+`) seeded with a tight summary when you're starting something unrelated.

### 4. Analyze your own usage patterns

Reflect on the scorecards you've collected:

- Which tasks needed the most retries? What was missing: context, a stop condition, the wrong model?
- Where did you over-stuff context?
- Which guardrail caught the most agent mistakes?

Turn recurring fixes into **persistent instructions** (Module 08) so you never pay for that lesson twice.

### 5. Bundle the guardrail into the prompt

End every implementation prompt with its verification so the agent self-gates instead of handing you broken work:

```text
Implement <change> in sample-app. Done when `npm run build`, `npm test`, and `npm run lint`
all pass.
```

Then confirm in the terminal:

```bash
cd sample-app && npm run build && npm test && npm run lint
```

This is Lever 5 (deterministic controls) wired straight into your prompt loop.

### 6. Right tool, right mode

- **Ask** for thinking; **Agent** for doing. Don't burn Agent turns on a question.
- Reach for a big model only when reasoning is genuinely hard.
- Reset early and often.

### Expected outcome

You can pre-filter inputs, keep tool output and sessions lean, compress context with `/compact` or reset before it bloats, review chat history for recurring fixes, and use your scorecard history to improve your defaults.

➡️ Next: 10 — Capstone

## VS Code · Module 10 — Capstone 🔴

**Goal:** combine all five levers to ship one clean, verified feature on the sample app, and prove the difference with your scorecard.

### The brief

> Add a **`PATCH /tasks/:id`** endpoint that lets a client update a task's `title`, `priority`, or `done` status. It must validate input, reject unknown IDs with 404, follow project conventions, and keep all checks green.

This touches routing, validation, business logic, and storage, a realistic, multi-step change.

### Run it through all five levers

Treat this as a graded exercise. Hit every lever consciously:

1. **Model selection (Lever 1)**
   - Use a **capable** model for the research/plan phases; you may drop to a **smaller** model for mechanical edits.

2. **Workflow design (Lever 4)** : do it in phases, resetting between each:
   - **Research (Ask):** add `routes.ts`, `store.ts`, `tasks.ts`, `types.ts`. Ask how updates should flow and what's missing in the store to support an update-by-id. Write the analysis to `RESEARCH.md`.
   - **Plan (Plan mode):** new session, read `RESEARCH.md` and write `PLAN.md`: a small, ordered, testable checklist. Review it before any code.
   - **Implement (Agent):** new session, one step at a time.

3. **Context optimization (Lever 2)**
   - In each phase, add **only** the files that phase needs. Reset between phases.

4. **Prompt engineering (Lever 3)**
   - Every implementation prompt must include explicit constraints and a verifiable **Done when** stop condition.

5. **Deterministic controls (Lever 5)**
   - First write/extend tests in `src/routes.test.ts` describing the new behavior (valid patch → 200; unknown id → 404; invalid priority → 400).
   - End every implement step with: `Done when npm run build, npm test, and npm run lint pass.`

If you built `.github/copilot-instructions.md` in Module 08, the agent should already honor conventions without restating them.

### Acceptance checklist

- [ ] `PATCH /tasks/:id` updates `title`, `priority`, and/or `done`
- [ ] Invalid input → `400`; unknown id → `404`; success → `200`
- [ ] New tests cover all three cases and pass
- [ ] `npm run build`, `npm test`, `npm run lint` all green
- [ ] No `any`, no `new RegExp` on user input, conventions followed
- [ ] You completed it in phases with session resets

### Final scorecard + reflection

Fill in one last scorecard for the whole capstone, then answer:

1. How many retries did this take vs. the "gamble" task back in Module 01?
2. Which lever saved you the most rework?
3. What will you turn into a persistent instruction so it's free next time?

### Top 5 actions : your takeaway

1. **Choose the right model.**
2. **Write clear prompts.**
3. **Split tasks.**
4. **Add deterministic guardrails.**
5. **Maintain concise instructions.**

👉 **Make every token count.**

🎉 You've finished the VS Code track. Want the same lessons from the terminal? Try the Copilot CLI track.
