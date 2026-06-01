# C3 : Context Engineering 🟢

> **Provide as little as possible, but as much as necessary.**

The model is a **stateless, probabilistic text engine**. It has no memory between calls, the _entire_ context is re-sent on every step. What you put in that context window (and what you leave out) determines quality.

---

## The two failure modes

| Too little context                     | Too much context                        |
| -------------------------------------- | --------------------------------------- |
| Model **hallucinates** missing details | Relevant signal is **buried in noise**  |
| Invents APIs, file names, behavior     | "Lost in the middle" — key info ignored |
| Confident but wrong                    | Slower, pricier, _and_ often wrong      |

The goal is the **narrow band in the middle**: exactly the files and facts needed, nothing more.

---

## Two context-window pitfalls

- **Lost in the middle** : models attend most to the **start** and **end** of a long context; information in the middle is frequently ignored.
- **Recency bias** : the model favors the **latest** inputs, so stale or contradictory earlier turns get over-weighted or forgotten.

**Best practice:** _reset sessions often_ and _split tasks_ so each context stays short and relevant.

---

## Exercise A : Trim the context

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

---

## Exercise B : Order matters

You have a long session. The crucial constraint is _"never log request bodies, they contain PII."_ Where should it live to survive **lost-in-the-middle** and **recency bias**?

- (a) Buried in turn 3 of a 20-turn chat
- (b) In a persistent instructions file **and** restated in your latest prompt
- (c) Said once at the very start and never repeated

<details>
<summary>Answer</summary>

**(b).** Persistent instructions keep it always-present (it rides at a stable position every call), and restating it in the latest prompt exploits recency bias _in your favor_. Option (c) gets lost as the session grows; (a) sits in the ignored middle.

</details>

---

## Expected takeaway

You are an **editor of context**, not a hoarder. Curate the minimal relevant set, put critical constraints where the model actually looks (start/end + persistent instructions), and reset often so the window stays clean.
