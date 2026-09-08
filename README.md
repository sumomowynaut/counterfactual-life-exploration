# Counterfactual Life Exploration

**中文名：假如可以重来** · **反事实人生探索**
**Slogan：Explore the lives that never happened. / 探索那些从未发生的人生。**

> An open-source AI Skill for exploring the lives that might have existed if we had chosen differently — then returning to now.
> 一个开源的 AI Skill：帮你回到人生中真实的关键决策节点，探索"如果当初做出不同选择"可能存在的另一条人生，然后回到现在。

**[English](#what-is-it) · [中文说明](#中文说明)**

---

## What is it?

CLE is an AI Skill (not an app, not a service) that guides a structured, epistemically disciplined exploration of a real past decision:

1. You tell it a moment in your life you wish you could redo — including any expectation you already have about how it would have turned out.
2. It builds your real timeline and identifies the turning point.
3. It defines a **single-variable counterfactual**: what if you had chosen differently? Your own expectation is noted — never treated as fact.
4. It walks the causal chain step by step — no butterfly-effect leaps, no happy-ending shortcuts.
5. It shows the parallel life and compares both lives (no scores, no hidden ranking).
6. You meet **The Other Self** — who only knows what the simulation actually established.
7. You reflect on why this regret matters, and **return to now**.

**It is not a life predictor. It is not a parallel-universe novel generator. It is not a life coach.** It is a disciplined exploration of what might have been — with clear epistemic labels separating facts from inferences, possibilities, and assumptions.

---

## Why?

> "如果当初做出了不同的选择，我会成为怎样的人？"

Every choice makes one version of you real — and makes countless others disappear. Most AI "life simulators" generate exciting parallel-universe stories; they don't help you understand your regret. CLE is built to do the latter:

- **Epistemic discipline** — every major claim is labeled as Fact / Inference / Plausible / Assumption (Narrative is an expression mode, not an epistemic level). Your counterfactual expectations are noted as expectations, never promoted to facts. No fake precision.
- **Single-variable counterfactuals** — only the decision you specify changes. Everything else stays put until causality moves it.
- **Two-sided comparison** — every life shows what it gains *and* what it pays.
- **The Other Self** — grounded in the simulation, not generic wisdom.
- **Return to Now** — the exploration ends by asking what you want to change *today*.

---

## How to use

CLE works in any agent that can load a Markdown-based skill (Claude Code, Codex, Cursor, and other AI agents). Two ways to get it:

### Option 1 — Clone and point to SKILL.md (works today)

```bash
git clone <this-repo-url>
```

Then tell your agent to load `SKILL.md` from the cloned directory. Its `references/` files sit alongside `SKILL.md` and are loaded on demand by the agent; keep them in the same directory.

### Option 2 — `npx skills` (after publishing)

Once published, install via the [open agent skills tool](https://github.com/vercel-labs/skills):

```bash
npx skills add <owner>/<repo>
```

The root-level `SKILL.md` is discovered automatically, and `references/`, `examples/`, and `tests/` install alongside it.

### Directly in any chat

Paste the contents of `SKILL.md` into your system prompt, then talk to the AI. This gives the core workflow; loading `references/` as well gives the full causal and epistemic rules.

### Start a session

Just tell it a moment in your life — for example:

> "我大学毕业的时候有两个 offer，一个在上海，一个在老家，最后我回去了。现在有时候会想，如果当时去了上海……"

The skill will guide you from there.

---

## Example

See [`examples/career.md`](examples/career.md) for a complete end-to-end walkthrough — from intake to return-to-now. More examples: [relationship](examples/relationship.md), [education](examples/education.md), [relocation](examples/relocation.md).

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
- **Not therapy.** If you are in crisis, please seek professional help.

---

## Structure

```
SKILL.md          # Entry point: trigger, workflow, hard constraints
references/       # Detailed rules (causality, uncertainty, reflection, safety, ...)
examples/         # Complete end-to-end demonstrations
tests/            # Behavioral tests for AI agents
phase4/           # Real-world validation cases and report
phase5/           # Publication readiness audit
```

---

## License

MIT

---

# 中文说明

## 这是什么

**Counterfactual Life Exploration（CLE，中文名：假如可以重来）** 是一个开源 AI Skill。它不是一个 App、一个网站、一次算命，也不是普通的人生模拟器。

它的核心是：围绕你人生中一个**真实发生过**的决策节点，构建一条"如果当初做了不同选择"的路径，然后**受约束地、逐层因果地**推演这条人生，让你看见另一个自己，比较两条人生各自得到和失去的东西，最后**回到现在**。

## 它和普通 AI 人生模拟器有什么不同

- **认识论纪律**：重大结论都会标注为「事实 / 推断 / 可能 / 假设」（叙事只是一种表达方式，不是认识等级）。你自己的反事实预期会被标注为「你的预期」，绝不会被当成事实，也不会提高推演的确定性。
- **单变量反事实**：只改变你指定的那一个决策。其他初始条件保持不变，直到因果链合理地改变它们。
- **拒绝伪精确**：不打分、不算"成功概率"、不排"哪条人生更好"。只呈现每条人生得到了什么、付出了什么、哪些仍然无法知道。
- **另一个自己（The Other Self）**：只知道自己这条人生里被推演建立过的信息。没推演过的事，它会老实说"我不知道"，不会编造。
- **回到现在（Return to Now）**：探索结束时会问：看完另一种人生之后，现在的你还想改变什么？过去的无法重来，但未来仍然没有被选择。

## 怎么使用

CLE 可以运行在任何能加载 Markdown-based Skill 的 AI Agent 中（Claude Code、Codex、Cursor 等）。

1. **获取**：克隆本仓库，让 Agent 加载根目录的 `SKILL.md`；或把 `SKILL.md` 内容粘贴进对话。
2. **开始**：用你自己的话讲一个你想重来的人生节点即可，例如：
   > "我大学毕业的时候有两个 offer，一个在上海，一个在老家，最后我回去了。现在有时候会想，如果当时去了上海……"
3. **过程**：Agent 会先听你讲、确认关键事实，再锁定你想重走的那一个节点，逐层推演，最后带你回到现在。它不是问卷，不会一次问你十个问题。

详细规则见 `references/`（workflow / causality / uncertainty / reflection / philosophy / safety）。完整示例见 `examples/`。

## 适用场景

- 职业选择："如果我当初没有辞职……"
- 感情："如果当初没有分手……"
- 教育："如果当初选了另一个专业……"
- 城市："如果当初没有离开家乡 / 去了另一座城市……"

## 边界与限制

- 不是预测工具：输出是探索性情景，不是预言。
- 不做人生评判：不会给两条人生打分或告诉你哪条更"正确"。
- 不替你决定：最终选择权永远在你手里。
- 不是心理治疗：如果你正处于危机中，请寻求专业帮助（本项目不提供诊断）。

## 仓库结构

```
SKILL.md          # 入口：触发条件、11 阶段流程、硬性约束
references/       # 详细规则（因果、认识论、反思、安全等）
examples/         # 四个完整端到端示例
tests/            # 行为测试清单
phase4/           # 真实世界验证案例与报告
phase5/           # 发布就绪审计
```

## License

MIT
