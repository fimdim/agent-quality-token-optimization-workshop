# C2 : The Compounding Error Problem 🟢

> Multi-step agent workflows **amplify** errors. Per-step accuracy that looks "good enough"
> collapses over many steps.

This is the single most important reason quality matters _more_ for agents than for one-shot chat.

---

## The math

If each step succeeds independently with probability `p`, then completing `n` steps in a row succeeds with probability:

$$P_{\text{success}} = p^{\,n}$$

That exponent is brutal. Examples:

| Per-step accuracy | After 50 steps ($p^{50}$) |
| ----------------- | ------------------------- |
| 99%               | ~**61%**                  |
| 95%               | ~**8%**                   |

A 4-point drop in per-step accuracy (99% → 95%) turns a _probably fine_ workflow into a _almost certainly broken_ one.

---

## Exercise

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

---

## Why this changes how you work

Two ways to keep $p^n$ high:

- **Raise `p`** — better model choice, cleaner context, precise prompts, guardrails. (Levers 1–3 and 5.)
- **Lower `n`** — split a giant task into short, independently-verified phases so errors can't silently compound. (Lever 4: Research → Plan → Implement, plus frequent session resets.)

Deterministic guardrails (tests, linters, type-checks) effectively **reset `p` back toward 1.0** after each step by catching errors before they propagate, which is exactly why Module 07 exists.

## Expected takeaway

Quality compounds **exponentially**. Small per-step improvements and shorter chains produce huge swings in whether the whole task succeeds. "Good enough per step" is a trap.
