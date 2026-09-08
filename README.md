# Counterfactual Life Exploration

**中文：假如可以重来**
**Slogan：Explore the lives that never happened.**

> An open-source AI Skill for exploring the lives that might have existed if we had chosen differently — then returning to now.

---

## What is it?

CLE is an AI Skill (not an app, not a service) that guides a structured exploration of a real past decision:

1. You tell it a moment in your life you wish you could redo — including any expectation you already have about "how it would have turned out"
2. It builds your real timeline and identifies the turning point
3. It defines a single-variable counterfactual: "what if you had chosen differently?" — your expectation is noted, not treated as fact
4. It walks the causal chain step by step — no butterfly-effect chaos, no happy-ending shortcuts
5. It shows you the parallel life, compares both lives (no scores, no hidden ranking)
6. You meet The Other Self — who only knows what the simulation established
7. You reflect on why this regret matters, and return to now

**It is not a life predictor. It is not a parallel-universe novel generator. It is not a life coach.** It is a disciplined exploration of what might have been — with clear epistemic labels separating facts from inferences from speculation.

---

## Why?

> "如果当初做出了不同的选择，我会成为怎样的人？"

Every choice makes one version of you real — and makes countless others disappear. Most AI "life simulators" generate exciting parallel-universe stories. They don't help you understand your regret. CLE is built to do the latter:

- **Epistemic discipline**: every major claim is labeled as Fact, Inference, Plausible, or Assumption (Narrative is an expression mode, not an epistemic level). Your counterfactual expectations are noted as expectations, never promoted to facts. No fake precision.
- **Single-variable counterfactuals**: only the decision you specify changes. Everything else stays put until causality moves it.
- **Two-sided comparison**: every life shows what it gains *and* what it pays.
- **The Other Self**: grounded in the simulation, not generic wisdom.
- **Return to Now**: the exploration ends by asking what you want to change *today*.

---

## How to use

CLE works in any agent that can load a Markdown-based skill (Claude Code, Codex, Cursor, and others). Two ways to get it:

### Option 1 — Clone and point to SKILL.md (works today)

```bash
git clone <your-repo-url>
```

Then tell your agent to load `SKILL.md` from the cloned directory. The skill's `references/` files sit alongside `SKILL.md` and are loaded on demand by the agent; keep them in the same directory.

### Option 2 — `npx skills` (after publishing to GitHub)

Once this repository is published to GitHub, it can be installed with the [open agent skills tool](https://github.com/vercel-labs/skills):

```bash
npx skills add <owner>/<repo>
```

The root-level `SKILL.md` is discovered automatically, and its `references/`, `examples/`, and `tests/` files install alongside it.

### Directly in any chat

Paste the contents of `SKILL.md` into your system prompt, then talk to the AI. This gives the core workflow; loading `references/` as well gives the full causal and epistemic rules.

### Start a session

Just tell it a moment in your life:

> "我大学毕业的时候有两个 offer，一个在上海，一个在老家，最后我回去了。现在有时候会想，如果当时去了上海……"

The skill will guide you from there.

---

## Example

See [`examples/career.md`](examples/career.md) for a complete end-to-end walkthrough of a career turning point — from intake to return-to-now.

---

## Philosophy

CLE is not about proving your past choice was wrong. It is about seeing the life that never happened — including what it would have cost — and then returning to the present with clearer eyes.

> 过去无法重来，但未来仍然没有被选择。

---

## Limitations

- **Not a predictor.** Outputs are exploratory scenarios, not forecasts.
- **No scoring.** CLE will not rank your lives numerically.
- **No decisions for you.** CLE presents possibilities; the choice remains yours.
- **Single session.** State lives only in your current conversation.
- **Not therapy.** If you're in crisis, please seek professional help.

---

## Structure

```
SKILL.md          # Entry point: trigger, workflow, hard constraints
references/       # Detailed rules (causality, uncertainty, reflection, safety...)
examples/         # Complete end-to-end demonstrations
tests/            # Behavioral tests for AI agents
```

---

## License

MIT


