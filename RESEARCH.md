# RESEARCH.md — Counterfactual Life Exploration（CLE / 假如可以重来）

> Phase 1 研究产出。目标：弄清"AI 反事实人生探索"这个方向上已经有什么、它们的问题是什么、CLE 应该站在哪里。

---

## 1. 研究方法

- 调研直接竞品与相邻项目（GitHub 公开项目为主）。
- 调研反事实思维（counterfactual thinking）的心理学研究，为"反思"阶段提供理论支撑。
- 调研 Agent Skills 开放标准，确定 Skill 的工程形态。
- 只提炼设计洞察，不复制任何项目的代码、文案或 Prompt。

---

## 2. 相关项目调研

### 2.1 赛博女娲 · 个人量子人生模拟器（nuwa-life-simulator.skill）

- 形态：结构化 Prompt / Skill，MIT，早期阶段。
- 定位："回到过去任意决策节点，改写选择，AI 推演平行人生。"
- 机制亮点：
  - 三条时间线（α 基准 / β 激进 / γ 随机）。
  - 三种推演引擎（混沌 / 统计 / 混合）。
  - "半衰期诚实"：按时间范围标注可信度（如 5 年以上 10–20%）。
  - 隐私沙盒：声称原始数据只在本地对话环境处理。
- 不足与风险：
  - "统计引擎 / 贝叶斯网络 / 先验概率"等表述带有伪科学包装的嫌疑——Prompt 无法真正维护贝叶斯网络，容易让用户误以为输出有统计学依据。
  - 百分比可信度数字（"83% 会……"）恰恰是本类产品最容易产生虚假确定性的地方。
  - 以"玩"和"存档"为主，反思（Reflection）环节薄弱，容易停留在平行宇宙小说。

### 2.2 Parallel Universe（dhruvahm666/parallel-verse）

- 形态：完整 Web App（Next.js + Supabase + Groq）。
- 定位：基于用户"What If"梦想生成 3 条平行人生时间线，可聊天"未来自己"。
- 亮点：Future Self 对话体验被验证为有吸引力；时间线 + 里程碑的交互结构清晰。
- 不足：
  - 面向"梦想/野心"（become billionaire），不是面向真实人生节点的遗憾处理。
  - 重度依赖账号、云服务和成本，MVP 不可复制。
  - 输出以爽感叙事为主，缺少代价呈现与不确定性区分。

### 2.3 Parallel Lives（Wrttnspknbrkn/parallel-lives）

- 形态：Web App，表单输入（职业/地点/假设决策）→ AI 生成替代人生。
- 不足：表单式体验与"人生探索"的情绪温度不匹配；功能清单（社交分享、徽章、3D 模型）偏离核心问题。

### 2.4 lAIfe（Donny-Guo/lAIfe）

- 形态：Flask + React + Groq 的 AI 人生模拟器。
- 亮点：README 明确提到"follows logical cause-and-effect relationships"——因果链是用户可感知的卖点。
- 不足：同样以叙事为主；没有事实/推测分层机制；没有"回到现在"的收束设计。

### 2.5 Future Self Emulator（shehanmakani/future-self-emulator）

- 形态：决策智能系统，模拟"今天做 A/B/C 选择后的未来自己"，带 API。
- 亮点：第一人称未来自我 + 权衡分析（tradeoff），与本项目的 The Other Self 相似。
- 关键差异：它面向**未来的决策**（前瞻性），CLE 面向**过去的节点**（回溯性）——这是根本不同的情绪对象：期待 vs 遗憾。

### 2.6 WhatIf.run（its-mc/whatif.run）

- 形态：AI 生成电影级叙事/图像/视频的"人生重选"平台。
- 亮点：证明"两条时间线（未选之路 / 必然之路）"的戏剧结构有市场吸引力。
- 不足：视觉奇观路线，成本高、幻觉风险高（生成内容无限定词），与"克制、诚实"的理念相反。

### 2.7 女娲蒸馏器（alchaincyf/nuwa-skill）——生态参照

- 形态：Agent Skills 开放标准下的成熟开源 Skill（SKILL.md + references/ + examples/）。
- 可借鉴的工程经验：
  - SKILL.md 用 YAML frontmatter（name / description）声明触发条件。
  - 细节规则拆到 `references/`，按需加载（progressive disclosure）。
  - `examples/` 提供完整端到端范例。
  - 跨 runtime 分发（Claude Code / Codex / Cursor / 通用 CLI `npx skills add`）。

---

## 3. 竞品共性总结

| 维度 | 现有项目的普遍做法 | 问题 |
| --- | --- | --- |
| 输入 | 表单（年龄/职业/收入）或"梦想宣言" | 问卷化、去情绪化；不尊重"讲故事"的自然入口 |
| 推演 | 一次性生成完整叙事 | 缺少逐层因果约束，AI 蝴蝶效应失控（"去上海→5年后CEO"） |
| 确定性 | 百分比、评分、统计包装 | 虚假精确是最大幻觉源 |
| 比较 | 常有"哪条路更好"的暗示 | 违背"人生无统一目标函数" |
| 反思 | 普遍缺失或止于鸡汤 | 用户获得的是爽感/伤感，不是理解 |
| 收束 | 无"回到现在"设计 | 用户沉溺于"如果当初" |
| 隐私 | Web 项目收集真实人生数据 | 敏感数据外流风险；Skill 形态天然更好 |

**共同的本质**：它们大多是"AI 平行人生小说生成器"。CLE 的差异化机会恰好藏在它们的共同盲区里。

---

## 4. 心理学研究支撑（反事实思维）

来源：Roese & Epstude 等关于 Counterfactual Thinking 的综述（Annual Review of Psychology；Functional Theory of Counterfactual Thinking）。

关键结论及设计映射：

1. **反事实思维普遍存在且有功能**——帮助人从过去提取教训、形成未来意图。
   → CLE 不是制造病态沉溺，而是把这一天然心理过程结构化。
2. **上行反事实（想象更好的可能）与下行反事实（想象更糟的可能）作用不同**——上行促进改进意图，下行提供安慰。
   → 比较阶段必须同时呈现反事实人生的"得到"与"失去"，避免只做上行比较（纯羡慕）或只做下行比较（廉价安慰）。
3. **反事实比较会放大后悔、内疚、羞耻等情绪**——尤其当用户认为结果由自己的行为造成时。
   → 安全边界：不诊断、不评判过去选择的对错；探索前有知情提示，探索后必须收束回现在。
4. **反事实思维可能功能失调**——与抑郁、焦虑、创伤后反刍相关。
   → Skill 必须识别高情绪风险信号（丧亲、自责、创伤、自伤表述）并转入安全话术/建议寻求专业支持，而不是继续推演。
5. **遗憾的功能与"未来仍有行动机会"相关**——对仍有纠正可能的领域，遗憾更持久也更有驱动力。
   → 这正是"Return to Now"（过去无法重来，但未来仍未被选择）的理论依据：把对过去的反事实能量导向对未来的一次真实选择。

---

## 5. 技术路线结论：Skill-first

- 所有被验证的核心体验（intake、时间线、分叉、因果、对照、另一个自己、洞察、回到现在）都可以由"结构化 Prompt + 渐进披露规则 + 示例"实现，无需代码。
- Agent Skills 开放标准（agentskills.io）：
  - 一个目录 + `SKILL.md`（YAML frontmatter：`name` ≤64 字符小写连字符；`description` ≤1024 字符说明做什么、何时触发）。
  - `references/` 存放深度规则，正文保持精简。
  - 兼容 Claude Code / Codex / Cursor 等 runtime，也可作为纯 Markdown 粘贴使用。
- 结论：MVP 采用 `SKILL.md + references/ + examples/ + tests/`，零代码、零依赖、零用户数据出域。

---

## 6. CLE 差异化定位

1. **只改一个变量**：严格单变量反事实，防蝴蝶效应失控（竞品普遍失控）。
2. **因果链逐层可解释**：每个重大变化必须回答 What changed / Why / Immediate / Secondary / Long-term / Uncertainty。
3. **五层认识论标签**：Fact / Strong inference / Plausible / Speculation / Narrative，禁止把推测包装成事实（竞品完全没有）。
4. **无分数比较**：只用 Higher/Lower/Trade-off/Uncertain，拒绝伪精确数字。
5. **反思是核心而非装饰**：Surface Regret → Deeper Regret → Hidden Desire → Present Relevance。
6. **The Other Self 基于已构建的推演**：对话严格锚定模拟结果，不脱离设定输出鸡汤。
7. **强制收束 Return to Now**：以"看完另一种人生，现在的你还想改变什么？"结束。
8. **隐私优先**：Skill 形态，一切发生在用户自己的对话环境，不建账号不上传。

---

## 7. 研究结论

- 方向成立：真实需求存在（多个项目验证），但现有方案全部停留在"生成叙事"，没有任何项目同时做到"单变量约束 + 因果可解释 + 认识论分层 + 反思收束"。
- CLE 的护城河不是文采，而是**认识论纪律**（什么知道、什么不知道）与**心理收束设计**（探索完回到现在）。
- 学术研究既验证了产品价值（反事实思维的准备功能），也给出了红线（功能失调风险、上行比较的后悔放大）——两者都直接进入架构约束。

> 下一步见 `ARCHITECTURE.md`。
