# ARCHITECTURE.md — Counterfactual Life Exploration

> Phase 1 架构产出：整体架构、核心 Skill 设计、目录方案、MVP 实施计划。本阶段不写实现代码。

---

## 1. 定位一句话

> Counterfactual Life Exploration is an open-source AI Skill for exploring the lives that might have existed if we had chosen differently — then returning to now.

不是预测器，不是平行宇宙小说生成器，不是人生顾问。是一个有认识论纪律的**反事实探索工作流**。

---

## 2. 总体架构

```text
                    用户自然语言故事
                          │
                          ▼
        ┌───────────  SKILL.md（编排层）───────────┐
        │  触发识别 → 流程状态机 → 输出纪律          │
        └──────┬──────────┬──────────┬─────────────┘
               ▼          ▼          ▼
        references/    references/   examples/
        workflow.md    causality.md  （端到端范例，
        uncertainty.md reflection.md   few-shot 锚点）
        safety.md      philosophy.md
               │
               ▼
        11-Phase 输出（见 §4）
```

设计原则：

- **Prompt/Skill-first**：零代码、零依赖、零用户数据出域。MVP 不引入任何运行时。
- **渐进披露**：SKILL.md 只保留触发条件、流程骨架、硬性禁令；深度规则在 `references/` 按需加载。
- **跨模型**：不依赖任何厂商 API；任何遵循 Agent Skills 标准的 runtime（Claude Code / Codex / Cursor）或直接粘贴 Markdown 均可运行。
- **单次会话完成**：MVP 不持久化状态；一次会话走完全流程。用户中途提供新事实则更新 Fact 层并重新校准后续推演。

---

## 3. 核心概念模型

### 3.1 五层认识论（全流程统一标签）

| 层级 | 含义 | 标记方式 |
| --- | --- | --- |
| Fact | 用户明确提供的事实 | 无需标记（默认可信） |
| Strong inference | 由事实合理推导 | `[推断]` |
| Plausible | 合理但明显不确定 | `[可能]` |
| ASSUMPTION | 为继续模拟而做出的假设 | `[假设]` |

NARRATIVE 是表达模式（正交），不是第五层确定性等级——叙事段落内部仍可包含四层中任何一层的内容，重大变化仍需标注。

规则：重大节点（职业变化、关系变化、长期走向）必须标注；普通叙事句子不逐句打标，避免形式主义。**绝对禁止把 ASSUMPTION 写成确定语气。**

### 3.2 反事实约束（防蝴蝶效应失控）

- **单变量原则**：只改变用户指定的那一个决策，其余初始条件全部保持不变。
- **逐层推演**：每个重大变化必须能回答六问——What changed? Why? Immediate effect? Secondary effect? Long-term effect? Uncertainty?
- **因果链断裂即停**：无法建立合理解释的推演不写；宁可留白，不可编造。
- **因果现实性检查**：推演每 3–5 年检查一次——因果是否成立、是否存在现实约束冲突、是否依赖未经支持的巧合、是否需要未经支持的人格变化、是否依赖未建立的重大外部事件。**CLE 不因反事实结果"过于成功""过于失败"或偏离一般人群分布而自动回拉。**"接近普通人群分布"不是硬约束。

### 3.3 人生变量（观察维度，非评分维度）

Career / Wealth / Relationship / Family / Health / Freedom / Stability / Social Network / Location / Identity / Well-being / Risk / Opportunity / Regret

比较时只用：Higher / Lower / Increased / Decreased / More / Less / Trade-off / Uncertain。**禁止数值打分。**

---

## 4. 核心工作流：11 Phases

| Phase | 名称 | 输入 | 输出 |
| --- | --- | --- | --- |
| 1 | Life Intake | 自然语言故事 | 结构化节点提取（时间/地点/人物/选择/未选项/已知/未知/目标/限制/结果/用户反事实预期） |
| 2 | Life Timeline | 用户补充 | 真实时间线（Events / Decisions / Constraints / Unknowns / Consequences） |
| 3 | Turning Point Detection | 时间线 | 关键节点列表 + 每个节点的分叉潜力判断；无分叉潜力则不强行模拟 |
| 4 | Counterfactual Branch | 用户选定节点 | Original World 摘要 + Counterfactual World 定义（单变量改变声明） |
| 5 | Causal Propagation | 反事实定义 | 逐层因果推演（六问必答 What/Why/Immediate/Secondary/Long-term/Uncertainty + 现实性检查） |
| 6 | Parallel Life | 因果链 | 结构化年度分叉表 → 转自然语言叙事（先结构后叙事，抑制自由发挥） |
| 7 | Two Lives Comparison | 两条人生 | 变量对照表（§3.3 规则，无分数，无隐性排名） |
| 8 | The Other Self | 反事实人生 | 基于推演的第一人称对话；回答严格锚定模拟结果；未推演事实必须说"不知道" |
| 9 | Counterfactual Reflection | 全程内容 | Surface Regret → Deeper Regret → Hidden Desire（用户自命名）→ Present Relevance |
| 10 | Philosophical Insight | 本次推演 | 从本次具体人生提炼的 Life Insight（禁止固定鸡汤句式和"你以为X其实Y"模板） |
| 11 | Return to Now | — | "看完另一种人生，现在的你还想改变什么？" + 未来导向收束 |

流程纪律：

- Phase 1–3 是**收集与确认阶段**，AI 应主动追问缺失的关键信息（选项是什么、当时知道什么、限制是什么），信息不足时明确说"我还无法负责任地推演"。
- Phase 4 开始**进入模拟**，之前必须复述单变量改变声明并获用户确认。
- Phase 10 之后会话自然结束；如用户继续问"如果当初"，提醒回到 Phase 4 的下一个节点，或结束。

### 可选高级模式：Third Life（MVP 不实现）

Life C = 既非 A 也非 B 的第三种选择。架构上预留：Phase 4 允许用户声明"我想探索第三种选择"，其余流程复用。

---

## 5. 安全与伦理边界

| 风险 | 边界 |
| --- | --- |
| 虚假确定性 | 禁止"你一定会""注定""83% 概率"；重大节点强制不确定性标注 |
| 替用户做决定 | 禁止"你应该离婚/辞职/复合"；最终决定权始终属于用户 |
| 医疗/心理诊断 | 不诊断疾病；不把正常遗憾病理化 |
| 高情绪风险 | 识别丧亲、创伤、自伤、严重抑郁信号 → 停止推演，表达共情，建议专业支持（附求助资源提示） |
| 隐私 | Skill 形态，数据不出用户对话环境；README 明确声明 |
| 沉溺 | 强制 Return to Now 收束；连续多次"如果当初"时温和引导结束 |

详见 `references/safety.md`（MVP 阶段实现）。

---

## 6. 项目目录方案

```text
counterfactual-life-exploration/
├── SKILL.md                  # 入口：触发条件 + 11-Phase 流程骨架 + 硬性禁令
├── README.md                 # 面向陌生开发者：What/Why/How/Example/Philosophy/Limitations
├── LICENSE                   # MIT
├── RESEARCH.md               # 竞品与理论研究（已有）
├── ARCHITECTURE.md           # 本文件
├── references/
│   ├── workflow.md           # 11-Phase 详细操作规则与输出模板
│   ├── causality.md          # 因果链六问、单变量原则、因果现实性检查
│   ├── uncertainty.md        # 五层认识论定义、标注规则、禁用语清单
│   ├── reflection.md         # 反思四步法（Surface→Deeper→Hidden→Present）
│   ├── philosophy.md         # 哲学内核与 Insight 生成规则
│   └── safety.md             # 安全边界与高风险信号处理
├── examples/
│   ├── career.md             # 完整端到端示例
│   ├── relationship.md
│   ├── education.md
│   └── relocation.md
└── tests/
    ├── test-01-career-basic.md       # 正常职业分叉
    ├── test-02-relationship-basic.md # 正常感情分叉
    ├── test-03-missing-info.md       # 信息不足
    ├── test-04-prediction-refusal.md # 拒绝预测
    ├── test-05-no-scoring.md         # 拒绝打分
    ├── test-06-implausible.md        # 不合理反事实
    ├── test-07-multi-decision.md     # 多关键决策
    ├── test-08-butterfly-control.md  # 蝴蝶效应失控
    ├── test-09-epistemic-labels.md   # 推测当事实
    ├── test-10-return-to-now.md      # 收束验证
    ├── test-11-anti-cliche.md        # 反鸡汤测试
    └── test-12-high-risk.md          # 高情绪风险
```

### SKILL.md frontmatter（草案）

```yaml
---
name: counterfactual-life-exploration
description: >
  Explore the lives that might have existed if you had chosen differently.
  Guides a structured, epistemically disciplined counterfactual exploration
  of a real past decision: intake, timeline, turning point, single-variable
  branch, causal propagation, parallel life, comparison, the other self,
  reflection, insight, and return to now. Use when the user wants to explore
  "what if I had..." about their own past. Not a life predictor.
---
```

---

## 7. MVP 实施计划

### Phase 3 — Core Skill（SKILL.md + references/）

| 步骤 | 内容 | 依赖 |
| --- | --- | --- |
| 3.1 | 写 `SKILL.md`（frontmatter + 触发 + 11-Phase 骨架 + 禁令清单） | 本文档 |
| 3.2 | 写 `references/workflow.md`（每 Phase 的输入/操作/输出模板） | 3.1 |
| 3.3 | 写 `references/causality.md`（六问、单变量、因果现实性检查） | 3.2 |
| 3.4 | 写 `references/uncertainty.md`（五层标签 + 禁用语清单） | 3.2 |
| 3.5 | 写 `references/reflection.md`（反思四步法） | 3.2 |
| 3.6 | 写 `references/philosophy.md`（Insight 生成规则） | 3.5 |
| 3.7 | 写 `references/safety.md`（边界与高风险处理） | 独立 |

### Phase 4 — Examples

| 步骤 | 内容 |
| --- | --- |
| 4.1 | `examples/career.md`：完整 11-Phase 端到端（ longest，作 few-shot 锚点） |
| 4.2 | `examples/relationship.md`、`education.md`、`relocation.md`（完整但精简） |

### Phase 5 — Tests

每个测试文件 = 输入场景 + 预期行为 + 判定标准（AI 应做/不应做的具体表现）。对照 §30 的 10 项测试。

### Phase 6 — Quality Review

用原需求 §33 的 8 个问题逐一审查；同时检查：

- 是否有把 ASSUMPTION/PLAUSIBLE 写成 Fact 的漏洞
- 是否存在鼓励沉溺的流程设计
- 示例是否展示了"代价"而不仅是"收益"

### Phase 7 — Open Source Polish

- `README.md`（第一屏 What/Why/How/Example/Philosophy/Limitations）
- `LICENSE`（MIT）
- 初始化 git 仓库，准备 GitHub 发布

---

## 8. 已识别风险与缓解

| 风险 | 严重度 | 缓解 |
| --- | --- | --- |
| AI 在叙事阶段悄悄滑回"编故事"模式 | 高 | Phase 5 先结构后叙事；叙事段落整体声明 + 重大节点标注 |
| 用户情绪被放大（上行反事实后悔） | 高 | comparison 强制双向（得到与失去）；safety.md 高风险信号中断机制 |
| 示例变成固定模板复读 | 中 | philosophy.md 规定 Insight 必须引用本次推演的具体细节；tests 验证 |
| Skill 在弱模型上退化 | 中 | SKILL.md 硬性禁令放在最前；关键规则重复出现在 workflow 各 Phase 模板内 |
| 用户期望"预测"而非"探索" | 中 | 触发时明确声明能力边界；Test 3 验证拒绝行为 |

---

## 9. 下一步

等待指令后进入 **Phase 3（Core Skill 实现）**。建议指令格式：

> 进入 Phase 3，开始写 SKILL.md 和 references/。




