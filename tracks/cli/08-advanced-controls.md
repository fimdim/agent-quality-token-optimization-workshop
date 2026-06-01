# CLI · Module 08 — Advanced Controls 🔴

**Goal:** make quality **repeatable** with persistent instructions, custom agents, skills, MCP tools, and sub-agents, so you don't re-explain context every session.

> Persistent instructions · custom agents · skills (dynamic context) · MCP tools (use carefully) · sub-agents for research.

---

## 1. Persistent instructions (`AGENTS.md` / instructions file)

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

---

## 2. Custom agents / saved configurations

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

---

## 3. Skills : dynamic context loading

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

---

## 4. MCP tools : powerful, use carefully

The CLI can connect to MCP servers (databases, browsers, issue trackers, etc.). Inspect/manage them (check `/help` for an `/mcp` command or your CLI's MCP config file).

**Caution:** every enabled MCP tool adds tool definitions to the context and can take real actions. Enable only what a task needs; disable the rest. More tools = more tokens + more ways to go wrong. Treat MCP tools like context: as few as necessary.

Example prompts:

```text
/mcp list
```

Use only the GitHub MCP for this task. Disable other MCP tools, then summarize open issues labeled "bug".

Before editing code, confirm which MCP tools are enabled and explain why each one is needed.

---

## 5. Sub-agents for research

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

---

## Expected outcome

The sample app has concise persistent instructions, you've created a reusable agent/persona, and you know when skills, MCP tools, and sub-agents add value vs. noise.

➡️ Next: [09 — Power-user tips](09-power-user-tips.md)
