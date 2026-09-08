# Implementation Notes — Phase 3 Quality Review

> Phase 3 完成后的自审记录。记录架构调整、发现的问题和最终自检回答。

---

## 1. 架构调整

| 调整 | 原因 |
| --- | --- |
| 工作流从 10 Phase 调整为 11 Phase | Causal Propagation（逐层因果推演）从 Parallel Life 中拆出，因为它技术含量最高、需要独立规则，合并会导致 Phase 职责模糊。逻辑完整性优先于数字一致性（用户指令 §5 已授权此调整）。 |
| The Other Self 增加"可以提问、可以沉默、可以不确定"约束 | 防止 AI 把另一个自己写成全知人生导师，输出鸡汤。 |

---

## 2. 发现并解决的问题

| 问题 | 严重度 | 解决方式 |
| --- | --- | --- |
| The Other Self 可能变成通用 AI | 高 | SKILL.md §6 明确角色约束；workflow Phase 08 明确"脱离模拟设定变成通用 AI"为禁止事项 |
| 推演结果依赖运气/巧合 | 高 | causality.md §4：因果链需要巧合即断裂，必须停止或降级 |
| NARRATIVE 段落可能藏未标注推测 | 高 | workflow Phase 06 强制段落开头整体声明；test-09 验证 |
| 用户中途纠正事实 | 中 | uncertainty.md §3 定义停止→确认→更新 FACT→重新推演→告知修正 |
| 探索沉溺 | 中 | SKILL.md §8 和 safety.md §6 定义"三次以上温和收束" |
| 弱模型退化 | 中 | SKILL.md 硬性禁令放在最前（§1）；关键规则在每个 Phase 模板内重复出现 |

---

## 3. CLE Quality Review

### Product：是不是仍然像人生模拟器？
不是。核心流程围绕"决策→因果→分叉→反思→回到现在"设计，而非"生成平行人生故事"。Phase 09–11 是反思阶段，占流程的 27%。

### Causality：有没有因果链？
有。Phase 05 强制六问框架（What/Why/Immediate/Secondary/Long-term/Uncertainty），每个重大变化必须能解释。causality.md 定义了单变量原则、收敛检查、因果链断裂处理。

### Epistemology：有没有区分事实和推测？
有。五层标签（FACT/INFERENCE/PLAUSIBLE/ASSUMPTION/NARRATIVE），重大节点强制标注，禁用语清单（你一定会/注定/百分比/幸福度），用户纠正时更新 FACT 层。

### UX：是不是像聊天，而不是填问卷？
是。Phase 01 明确"不填表，不问年龄收入婚姻"；SKILL.md §10 定义开场方式；workflow 要求一次追问一件事。

### Reflection：有没有真正进入反思？
有。四步法（Surface → Deeper → Hidden → Present），AI 只引导不自答，reflection.md 明确"AI 的话在那里停留"而非急于接话。

### Philosophy：有没有变成廉价鸡汤？
不。philosophy.md 规定 Insight 必须引用本次推演具体内容；无法产生深度时诚实呈现常识；reflection.md 列出禁用句式。test-11 专测反鸡汤。

### Safety：有没有把模拟包装成预测？
不。Test 04 专测拒绝确定性预测；SKILL.md B1 禁令；README Limitations 明确"Not a predictor"。

### Agent compatibility：不同 Agent 是否都能够理解？
SKILL.md 使用 YAML frontmatter 符合 Agent Skills 标准；references 按需加载；examples 提供端到端 few-shot 锚点；不依赖任何厂商 API。

---

## 4. 最终自检回答（原需求 §26）

1. **CLE 和普通平行人生小说生成器有什么本质区别？**
   小说生成器的目标是"好看的故事"。CLE 的目标是"帮助你理解你的遗憾"。区别体现在：单变量约束（不失控）、因果链可解释（不跳跃）、认识论分层（不骗你）、双向比较（不诱导你羡慕）、反思与收束（不让你沉溺）。

2. **CLE 如何避免把可能性说成事实？**
   五层标签系统。重大节点（职业/关系/长期走向）强制标注 `[推断]` `[可能]` `[假设]`。禁用语清单（"你一定会""83%"等）。NARRATIVE 段落必须整体声明。

3. **CLE 如何避免蝴蝶效应失控？**
   单变量原则（只改一个决策，其余分叉瞬间冻结）+ 因果链六问（每步必须解释为什么）+ 每 3–5 年收敛检查（回归合理人群分布）+ 因果链断裂即停。

4. **CLE 为什么不使用人生总分？**
   人生没有统一目标函数。分数会制造虚假判断依据，暗示"这条更好"，违反"不替用户判断哪条路更好"的核心原则。用 Trade-off 替代。

5. **The Other Self 从哪里产生？**
   从 Phase 05–07 已构建的反事实人生。它只能知道自己走过的经历、得到和失去的东西。它不是全知 AI，不是人生导师。

6. **Reflection 与普通心理鸡汤有什么区别？**
   鸡汤给结论（"一切都是最好的安排"），短路思考。Reflection 用四步引导用户自己发现深层遗憾和隐藏渴望。AI 只提问，不分析，不诊断。

7. **为什么最后必须 Return to Now？**
   反事实思维的价值是"提取教训、形成未来意图"，不是"沉溺过去"。收束把模拟的能量导向对未来的一次真实选择，符合反事实思维的心理学功能。

8. **用户完成体验后，最理想的心理变化是什么？**
   从"如果当初……就好了"变成"我现在更清楚自己真正想要的是什么，以及这个渴望在今天的我身上还有没有出口"。不是"当初选对了"，而是"我理解了为什么我会成为今天的我"。

---

## 5. 已知遗留问题

| 问题 | 严重度 | 说明 |
| --- | --- | --- |
| tests 是行为规范，不是自动化测试 | 已接受 | MVP 纯 Skill 无代码，无法机器执行。tests 的价值在于：(1) 人工审查时逐项核对；(2) AI Agent 自评时作为判定标准。 |
| 弱模型可能不遵循 references 按需加载 | 中 | 缓解：SKILL.md 关键规则已前置硬性禁令；如果实测退化，考虑把 causality 六问模板内联到 SKILL.md |
| examples 中具体细节（公司名、人物）全部为虚构 | 已声明 | 每个 examples 文件头部已注明"反事实内容为虚构演示" |
| Insight 的"深度"因模型能力而异 | 低 | philosophy.md 已定义兜底："无法产生深度时诚实呈现常识" |

---

## 6. Phase 3 完成状态

| 交付物 | 状态 |
| --- | --- |
| SKILL.md | ✅ |
| references/（6 个文件） | ✅ |
| examples/（4 个文件） | ✅ |
| tests/（12 个文件） | ✅ |
| README.md | ✅ |
| LICENSE (MIT) | ✅ |
| IMPLEMENTATION_NOTES.md | ✅（本文件） |

**下一步**：等待指令进入 Phase 4（Examples 已在此阶段完成——原计划 Phase 4 的示例工作已提前实现）。

---

# Phase 3.5 Remediation Log（2026-09-08）

> 依据 `AUDIT.md` 的审计发现逐项修复。只修审计问题，不新增功能。

## 修复对照

| Audit ID | 状态 | 修复位置 | 修复内容 |
| --- | --- | --- | --- |
| F1 (P0) | ✅ 已修 | SKILL.md §1 B8 细则 + §2.5；uncertainty.md §2/§3；workflow Phase 01/04 | 新增"用户输入四类归属"规则和"用户反事实预期"处理规则：用户预期不是 FACT，其确定性不得提高推演确定性，推演独立于预期进行，预期与结果不一致时如实呈现 |
| F2 (P1) | ✅ 已修 | SKILL.md §2；uncertainty.md §1 | 标签体系改为"四层认识论（FACT/INFERENCE/PLAUSIBLE/ASSUMPTION）+ 一个正交的表达模式（NARRATIVE）"，消除第五层混淆 |
| F3 (P1) | ✅ 已修 | examples/career.md, relationship.md, education.md, relocation.md | 四个示例的 Insight 全部重写：去除"你以为X其实Y"模板，改为引用本次推演的具体证据（另一条路自己的遗憾/那条路特有的发现/两版的各自代价） |
| F4 (P1) | ✅ 已修 | SKILL.md §6；workflow Phase 08 | The Other Self 增加"未推演事实必须说不知道"硬规则 + 用户诱导突破信息边界的处理 + 失败示例（"结婚了不过后来离婚了"禁止）；career.md Phase 08 增加示范对话 |
| F5 (P1) | ✅ 已修 | reflection.md Step 3；workflow Phase 09 | Hidden Desire 改为"用户先命名，AI 只提供候选方向列表"，禁止 AI 先定论再找确认 |
| F6 (P1) | ✅ 已修 | causality.md §3；workflow Phase 05 | 收敛检查升级为"现实性检查"：检查因果成立性而非结果极端度，不合格必须显式修正，连续两个分段不合格必须停止推演线 |
| F7 (P1) | ✅ 已修 | causality.md §1；workflow Phase 05；examples/career.md Phase 05 | 六问改为必答，What/Why 必须显式出现在输出；career.md 因果链示范补齐 What/Why 显式行 |
| F8 (P1) | ✅ 已修 | SKILL.md §3.1 | 新增集中式"中断/退出/确认条件"表（8 种条件）+ 确认节奏总则（信息充分时主动推进） |
| F9 (P1) | ✅ 已修 | safety.md §1；SKILL.md §9 | 新增"反事实沉浸/现实逃避"信号类别（"我只想一直活在那个版本的人生里"等），定义处理方式 |
| Spec drift | ✅ 已修 | ARCHITECTURE.md, README.md | Phase 数量 10→11 全文同步；五层标签命名统一（Speculation→ASSUMPTION，NARRATIVE 改为表达模式）；tests 目录列表同步为实际 12 个文件；frontmatter 草案同步为实际版本；README 的 7 步流程更新 |
| UX 机械确认 | ✅ 已修 | workflow 总则；SKILL.md §3.1 | 各 Phase 明确"信息充分时合并呈现、主动推进"；Phase 03 用户已指认节点时跳过选择；Phase 05 检查可与下一段合并 |

## 补充说明

- single-variable 澄清：单变量原则的核心是"因果必须成立"，不是"结果必须回归平均人群"。极端结果合法（只要因果链能解释）。已写入 causality.md §3。
- 用户指令 §6 的 4 个示例场景（去上海当管理层/没分手肯定结婚/选计算机完全不一样/去北京已经成功）已通过 uncertainty.md §3 和 examples/career.md 的示范覆盖。
- 用户指令 §8 的 4 个 Other Self 测试（Test A/B/C/D）已通过 workflow Phase 08 的硬规则和失败示例覆盖。

## 遗留

无 P0 / P1 遗留。建议进行一次 Phase 3.5 Final Audit（第三方视角验证修复质量），通过后再进入 Phase 4。

---

# Phase 3.5 Final Remediation Log（Final Audit 后定点修复）

> 依据 `FINAL_AUDIT.md` 的 Remaining Findings 逐项修复。只做定点修复，未进入 Phase 4。

## 修复对照

| Finding | 状态 | 修复位置 | 内容 |
| --- | --- | --- | --- |
| R1 (P1) | ✅ 已修 | ARCHITECTURE.md §3.2/§6/§7 | "收敛检查/现实性回拉/偏离合理人群分布" 全部改为"因果现实性检查"，并明确"CLE 不因结果过于成功/失败或偏离人群分布而自动回拉" |
| R2 (P1) | ✅ 已修 | examples/career.md Phase 10 | Insight 完全去除"你以为X"句式，改为"Simulation Evidence → 两条路的'不在场代价'对照 → 换一份遗憾"结构 |
| R3 (P2) | ✅ 已修 | examples/education.md | 新增精简 The Other Self 环节，并注明"跳过是流程选择，不是缺失" |
| R4 (P2) | ✅ 已修 | SKILL.md §4 + workflow.md Phase 04 | 新增显式规则：即使用户明确要求"不要单变量了，三个一起模拟"，也必须拒绝多变量，要求选一个核心变化 |
| R5 (P2) | ✅ 已修 | SKILL.md §4、references/causality.md §3、references/workflow.md Phase 05 | 术语统一为"因果现实性检查"，并反复强调"不因偏离人群分布而拉回" |

## 术语最终统一

统一名称：**因果现实性检查**（不再使用"收敛检查"作为与"现实性检查"并列的术语）。

语义：检查因果是否成立、是否存在现实约束冲突、是否依赖未经支持的巧合、是否需要未经支持的人格变化、是否依赖未建立的重大外部事件。**不检查"结果是否偏离一般人群分布"。**

---

# v0.2 Iteration Log

> v0.2 小范围、低风险迭代。保留 v0.1 全部已验证核心，新增 8 项边界与可移植性改进。

## Files Changed

| 文件 | 变更 |
| --- | --- |
| SKILL.md | §2.4 用户报告事实与内部一致性检查；§7 Insight 新定义（非心理分析）；§8 三种结束 + Session Summary；§6 Other Self Knowledge Boundary 允许/禁止清单 + Role Induction Resistance；§4.1 Third Life / Secondary Branch 规则；§9 安全分级与不强制意义重构 |
| references/uncertainty.md | 新增 §2 Reported Fact 与内部一致性检查（轻量机制，不改变 taxonomy）；冲突确认话术；禁用语增加心理归因与"你记错了" |
| references/philosophy.md | 重写：Insight 非心理分析定义、Observation/Tension/User-owned Meaning 三段结构、心理归因禁止清单、诚实兜底（替代旧的模糊"只能给常识"说法） |
| references/safety.md | 重写：风险三档分级（正常遗憾/重大失去/急性风险，非关键词熔断）、安全模式操作、不强制意义重构、§6.2 用户主动中断 |
| references/workflow.md | Phase 04 增加 Secondary Branch 规则；Phase 08 明确 Other Self 允许/禁止使用清单；Phase 10 Insight 三段结构；Phase 11 三种结束（A/B/C）+ Session Summary；Phase 01/02 引用 Reported Fact |
| tests/test-13-decision-pressure.md | 新增：决策压力对抗测试（6 场景：直接判断/取消不确定性/强迫二选一/幸福度/强压/切换现实建议） |
| examples/family-expectations.md | 新增：东亚家庭期望分叉案例（父母期望、家庭关系、城市、职业、经济安全、自主性），非刻板概括 |
| STANDALONE_PROMPT.md | 新增：无 Skills 环境兼容 Prompt；顶部声明 canonical 为 SKILL.md，避免双 Prompt 漂移 |
| README.md | 新增 Model Capability 章节；安装体验优化（npx skills add 一键 + clone + standalone）；新示例与结构引用 |
| IMPLEMENTATION_NOTES.md | 本记录 |

## Core Regression（v0.1 已验证项）

- 11 Phase：保留（Phase 01–11 完整，见 SKILL.md §3）
- Single-variable：保留（SKILL.md §4，含"用户要求一起模拟"拒绝）
- Causal Propagation + 因果现实性检查：保留（SKILL.md §4/§3.1，references/causality.md 未改）
- Fake precision / life score / happiness score：禁止清单保留且扩充
- User counterfactual expectation ≠ FACT：保留（§2.5）
- Other Self 知识边界：保留并增强
- Reflection 用户拥有意义：保留
- Insight 禁心理归因：增强为显式三段结构
- Return to Now：保留（作为 Natural Completion 闭环；B/C 两种结束不再强制）

## 未做（遵守约束）

- 未改 11 Phase、未改因果传播核心模型、未引入 Mermaid 强制、未做 Web UI/数据库/API、未改 LICENSE、未删 audit/phase4/phase5 材料、未改历史测试结论。
