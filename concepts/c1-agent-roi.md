# C1 : Agent ROI 🟢

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

---

## The "agent gambling" anti-pattern

A common failure loop:

1. Write a **weak prompt** with **minimal context**.
2. Get a mediocre result.
3. **Retry** until something works.

Each retry re-sends the prompt, the files, and the growing conversation, so the cheap-looking first prompt quietly becomes the _most expensive_ path to the answer.

---

## Exercise

Imagine two developers solving the same task with the **same model**.

### Developer A : "just retry"

| Attempt | Tokens sent | Outcome                 |
| ------- | ----------- | ----------------------- |
| 1       | 3,000       | Wrong — too vague       |
| 2       | 5,000       | Wrong — missing context |
| 3       | 7,000       | Wrong — agent guessed   |
| 4       | 9,000       | ✅ Finally correct      |

### Developer B : "invest up front"

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

---

## Reflect

- Where in your own work do you "gamble", retrying instead of improving the prompt?
- **"Don't minimize tokens, maximize their value."** A 6,000-token prompt
  that works once beats a 3,000-token prompt you run four times.

## Expected takeaway

Cost is dominated by **retries**, not by the size of a single good prompt. Optimize for
_getting it right the first time_, and total token spend usually **falls**.
