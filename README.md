# Agent Quality & Token Optimization : Hands-On Workshop

> **Core principle:** Don't minimize tokens - **maximize their value.**
> Better quality → fewer retries → lower total cost.

This workshop turns the _Agent Quality & Token Optimization_ workshop into a set of **hands-on labs**. You will not just read about the techniques, you will _practice_ them and **measure** the difference they make.

---

## Run in GitHub Codespaces (zero local setup)

The fastest way to start is a Codespace, Node.js, the sample app dependencies, and the Copilot extensions are all pre-configured by [.devcontainer/devcontainer.json](.devcontainer/devcontainer.json).

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/fimdim/agent-quality-token-optimization-workshop)

1. Click the badge (or **Code ▸ Codespaces ▸ Create codespace**).
2. Wait for the container to build, `npm install` runs automatically in `sample-app/`.
3. Open a terminal and verify: `cd sample-app && npm run build && npm test`
   (the build passes; **one** test fails on purpose, that's your first exercise).

> Prefer local? Any machine with **Node.js 20+** works too, see the track setup module.

---

## Who this is for

A mixed audience, from developers new to AI agents through to experienced Copilot users.
Modules are ordered by increasing difficulty. Each module clearly marks its level:

| Badge | Level        | Meaning                                   |
| ----- | ------------ | ----------------------------------------- |
| 🟢    | Beginner     | Safe to do with no prior agent experience |
| 🟡    | Intermediate | Assumes you've done the beginner modules  |
| 🔴    | Advanced     | Power-user techniques, deeper config      |

---

## Two tracks — pick one (or do both)

The workshop ships as **two fully separate tracks** covering the same concepts with
tool-native instructions:

| Track                  | Tool                                        | Start here                                           |
| ---------------------- | ------------------------------------------- | ---------------------------------------------------- |
| **VS Code**            | GitHub Copilot Chat / Agent mode in VS Code | [`tracks/vscode/README.md`](tracks/vscode/README.md) |
| **GitHub Copilot CLI** | `copilot` command-line agent in a terminal  | [`tracks/cli/README.md`](tracks/cli/README.md)       |

Both tracks share:

- [`concepts`](concepts/README.md) : short, **tool-agnostic** thinking exercises (no tool required).
- [`sample-app`](sample-app/README.md) : a small, deliberately imperfect TypeScript API you will
  improve throughout the labs.

> You can complete the **concepts** with pen and paper. The **track modules** use the
> sample app so your prompts have something real to work on.

---

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

---

## Prerequisites

**Common**

- [Node.js 20+](https://nodejs.org/) and npm (for the sample app)
- [Git](https://git-scm.com/)
- A GitHub account with **GitHub Copilot** enabled

**VS Code track**

- [Visual Studio Code](https://code.visualstudio.com/)

**CLI track**

- [GitHub Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/about-copilot-cli) installed
  (`npm install -g @github/copilot` or the official installer) and authenticated
  (`copilot` then `/login`).

> Verify your setup in **Module 00** of your chosen track before continuing.

---

## How to measure "quality" without raw token counts

Throughout the labs you'll use these **proxy metrics** to make the abstract idea of "token value" concrete:

- **Retries to success** : how many times you had to re-prompt before the result was correct.
- **Turns / tool calls** : how many round-trips the agent took.
- **Correction edits** : how many manual fixes you made afterward.
- **Guardrail signal** : did tests / lint / type-check pass on the first agent attempt?

Lower numbers = higher token value. You'll record these in a simple scorecard in each module.

---

## The 5 levers at a glance

```text
1. Model selection       → large = plan/debug · medium = implement · small = trivial · Auto by default
2. Context optimization  → only relevant files · reset sessions often
3. Prompt engineering    → be precise · add stop conditions · supply context explicitly
4. Workflow design       → Research → Plan → Implement (separate, clean contexts)
5. Deterministic control → tests · linters · security checks to stop compounding errors
```

---

## Top 5 actions (the takeaway you should leave with)

1. Choose the right model.
2. Write clear prompts.
3. Split tasks.
4. Add deterministic guardrails.
5. Maintain concise instructions.

> **→ Make every token count.**
