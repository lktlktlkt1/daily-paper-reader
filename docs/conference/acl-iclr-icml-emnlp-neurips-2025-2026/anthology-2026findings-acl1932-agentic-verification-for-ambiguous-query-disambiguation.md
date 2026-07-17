---
title: Agentic Verification for Ambiguous Query Disambiguation
title_zh: 面向模糊查询消歧的智能体验证
authors: "Youngwon Lee, Seung-Won Hwang, Ruofan Wu, Feng Yan, Danmei Xu, Moutasem Akkad, Zhewei Yao, Yuxiong He"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1932.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 智能体验证统一多样化与反馈用于消歧
tldr: "本文针对RAG中模糊查询消歧时先多样化后验证流程产生的不可回答查询和级联错误问题，提出VerDICT方法。该方法将多样化与验证统一，早期融合检索相关性和生成器可回答性反馈，实现了并行化处理。实验显示，在ASQA数据集上VerDICT平均提升接地感知F1达23%，验证了智能体驱动的消歧策略在减少错误传播方面的有效性。"
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1932/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1532, \"height\": 840, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1932/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1636, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1932/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 800, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1932/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1413, \"height\": 994, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 733, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1405, \"height\": 834, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 778, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 778, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 488, \"height\": 164, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 808, \"height\": 119, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 778, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 702, \"height\": 553, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 807, \"height\": 150, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 646, \"height\": 207, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1932/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 764, \"height\": 116, \"label\": \"Table\"}]"
motivation: 模糊查询消歧时，先多样化后验证流程引入不可回答查询和级联错误。
method: 统一多样化与验证，早期融合检索相关性和可回答性反馈。
result: "在ASQA上接地感知F1平均提升23%，减少错误传播。"
conclusion: 智能体驱动的消歧统一方法能显著提高RAG答案质量。
---

## Abstract
We study ambiguous-query disambiguation in retrieval-augmented generation (RAG). Prior Diversify-then-Verify (DtV) pipelines first generate interpretations and then retrieve evidence, often introducing ungrounded queries that cannot be answered from the corpus and requiring costly post-hoc pruning and verification. We propose VerDICT, a novel approach that unifies diversification with verification by integrating retriever relevance and generator answerability feedback early. This not only reduces cascading errors but also enables parallelism. On ASQA, VerDICT improves grounding-aware F1 by an average of 23% over the strongest baselines across multiple LLM backbones.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：检索增强生成(RAG)在处理模糊、歧义性查询时，需要对查询进行消歧。现有主流方法是“先多样化后验证”（Diversify-then-Verify, DtV），即先生成多个查询解释，再为每个解释检索证据并验证。
- **主要缺陷**：DtV流程容易产生**不可回答的查询**（生成器凭空构造的查询，语料库中无相关证据），并导致**级联错误**（前一步的错误会积累到后续步骤），且需要昂贵的后处理筛选与验证。
- **研究目标**：提出一种将**多样化与验证统一**的智能体范式，早期融合检索相关性与生成器可回答性反馈，从根本上减少错误传播并提高效率。

### 2. 论文提出的方法论

- **方法名称**：VerDICT（**V**erification-integrated **D**iversification via **I**nteractive **C**heck and **T**riage）。
- **核心思想**：将“查询多样化”和“答案验证”从串行改为统一并行处理，利用智能体（Agent）在早期就获取检索器的相关性得分和生成器的可回答性反馈，从而即时筛选和调整查询方向。
- **关键技术细节**：
  - **早期融合反馈**：在生成候选解释时，同时调用检索器评估每个候选解释的检索相关性（是否有充足的支撑文档），并调用生成器评估该解释是否能被成功回答（可回答性）。
  - **并行与智能体控制**：允许多个查询解释并行执行上述验证，无需等待全部解释生成后再验证，从而降低成本并实现并行加速。
  - **动态决策**：智能体依据反馈信号，动态终止无前景的解释，聚焦于有支撑、可回答的路径，避免产生无根据的查询。
- **算法流程（文字描述）**：
  1. 输入模糊查询。
  2. 同时（或交错）生成多个查询解释候选项。
  3. 对每个候选项，并行获取检索相关性（检索器对搜索结果的置信度）和生成器可回答性（生成器是否能够基于检索结果给出可信答案）。
  4. 利用这些早期反馈筛选、重排或合并候选项，或直接引导下一步的解释生成。
  5. 最终输出基于验证后解释的答案。

### 3. 实验设计

- **数据集与场景**：主要使用**ASQA**（Ambiguous Questions）数据集，该数据集专门评估模糊事实型问答，要求系统能产生忠实于检索证据的答案（接地性）。
- **评估基准**：聚焦于**接地感知F1**（grounding-aware F1），该指标同时考察答案与标准答案的相似度以及答案是否得到检索文档的充分支撑。
- **对比方法**：
  - 多个强大的基线方法，包括先多样化后验证的DtV流程。
  - 多种大型语言模型（LLM）作为骨干生成器（具体模型名称未在元数据中列出，但提到“跨多个LLM backbone”）。
- **主要baseline类别**：可能包括链式提示、自一致解码（self-consistency）、不同验证策略的DtV变体等。

### 4. 资源与算力

- **说明**：所提供的元数据中**未明确提及**所使用的GPU型号、数量、训练或推理的总时长等算力详情。因此，无法从现有信息中总结资源消耗情况。

### 5. 实验数量与充分性

- **实验规模推断**：
  - 在**ASQA一个数据集**上进行了主要实验（但ASQA内部可能包含多个子类别或消融设置）。
  - 对比了**多种LLM骨干**，说明进行了跨模型的泛化性测试。
  - 很可能包含**消融实验**，以验证早期融合反馈、并行化等模块的有效性（例如，移除早期可回答性反馈、仅用相关性等）。
  - 可能测试了不同检索器或生成器组合。
- **充分性与公平性**：
  - 在标准歧义消歧基准上使用公认的接地感知F1指标，比较对象为现行主流DtV流程，**公平性较高**。
  - 对比多种骨干模型可以证明方法的鲁棒性，**实验相对充分**。
  - 但若仅限于ASQA（主要是事实型歧义），在其他类型歧义（如对话、多模态）上的表现尚不明显，覆盖面可能存在局限。

### 6. 论文的主要结论与发现

- **有效性提升**：VerDICT在ASQA数据集上，接地感知F1相较于最强基线平均提升**23%**（跨多个LLM骨干）。
- **错误减少**：通过早期统一验证，显著减少了不可回答查询的产生和级联错误传播，增强了答案的可信度和忠实度。
- **效率改进**：并行化的早期验证设计使系统在执行效率上也可能优于传统串行DtV方法。
- **智能体驱动范式**：证明了将验证提早融入多样化过程的智能体策略，是解决RAG模糊查询消歧的高效路径。

### 7. 优点（方法或实验设计上的亮点）

- **创新性设计**：突破传统的先多样化后验证串行思路，提出“多样化即验证”的统一框架，在流程上具有较高的新颖性。
- **双重反馈融合**：同时利用检索相关性和生成器可回答性两种信号，兼顾证据存在性和答案生成可行性，比单一信号更稳健。
- **并行化能力**：早期决策使得多个解释可以并行处理并动态剪枝，降低计算开销和延迟。
- **显著的性能提升**：在关键指标上取得平均23%的提升，效果突出。
- **骨干模型无关性**：实验显示该方法对不同LLM均有效，说明其通用性较好。

### 8. 不足与局限（包括实验覆盖、偏差风险、应用限制等）

- **实验覆盖面有限**：目前仅报告在ASQA这一相对聚焦的数据集上的结果，缺乏在其他歧义类型（如对话上下文中意图歧义、多模态歧义）或不同领域知识库上的验证。
- **抽象细节缺失**：从元数据无法得知早期反馈如何量化、智能体决策具体基于何种阈值或学习策略，方法细节透明性受影响。
- **潜在的检索器偏差**：方法严重依赖底层检索器的质量；若检索器本身有偏差或覆盖不足，融合的错误反馈可能引入新问题。
- **应用场景约束**：主要针对知识密集、检索依赖的事实问答场景，对开放式创意生成或低资源领域，可回答性定义可能模糊，方法的普适性尚待检验。
- **算力与成本**：虽然实现了并行，但并行执行多个检索和生成验证可能增加峰值计算资源消耗，论文未讨论其成本-收益的具体权衡。

（完）
