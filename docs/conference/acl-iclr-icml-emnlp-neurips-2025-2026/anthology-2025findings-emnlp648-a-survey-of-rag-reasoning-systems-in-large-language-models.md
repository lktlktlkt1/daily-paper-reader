---
title: A Survey of RAG-Reasoning Systems in Large Language Models
title_zh: LLM中检索增强生成推理系统综述
authors: "Yangning Li, Weizhi Zhang, Yuyao Yang, Wei-Chieh Huang, Yaozu Wu, Junyu Luo, Yuanchen Bei, Henry Peng Zou, Xiao Luo, Yusheng Zhao, Chunkit Chan, Yankai Chen, Zhongfen Deng, Yinghui Li, Hai-Tao Zheng, Dongyuan Li, Renhe Jiang, Ming Zhang, Yangqiu Song, Philip S. Yu"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.648.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 综述融合RAG与推理的系统，包括智能体迭代搜索-思考框架
tldr: RAG提升事实性但难以处理多步推理，纯推理方法则易产生幻觉。本文从统一视角梳理推理如何增强RAG各阶段、外部知识如何辅助推理，并重点介绍了智能体LLM交替搜索与思考的协同框架。该综述为理解RAG与推理的深度融合、达成高性能知识密集型任务提供了全景视图。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.648/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1586, \"height\": 664, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.648/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 807, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.648/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1581, \"height\": 755, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.648/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1528, \"height\": 1257, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.648/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1529, \"height\": 1454, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.648/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1676, \"height\": 948, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.648/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1667, \"height\": 1263, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.648/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1576, \"height\": 1185, \"label\": \"Table\"}]"
motivation: RAG和推理单独使用各有不足，需融合应对复杂任务。
method: 从推理-搜索统一视角综述三大类方法：推理增强RAG、RAG增强推理及协同框架。
result: 厘清了融合机制与智能体搜索-思考迭代的高性能路径。
conclusion: RAG与推理协同是迈向可靠多步推理的重要方向。
---

## Abstract
Retrieval-Augmented Generation (RAG) lifts the factuality of Large Language Models (LLMs) by injecting external knowledge, yet it falls short on problems that demand multi-step inference; conversely, purely reasoning-oriented approaches often hallucinate or mis-ground facts. This survey synthesizes both strands under a unified reasoning-search perspective. We first map how advanced reasoning optimizes each stage of RAG (Reasoning-Enhanced RAG). Then, we show how retrieved knowledge of different type supply missing premises and expand context for complex inference (RAG-Enhanced Reasoning). Finally, we spotlight emerging Synergized RAG-Reasoning frameworks, where (agentic) LLMs iteratively interleave search and thought to achieve state-of-the-art performance across knowledge-intensive benchmarks. We categorize methods, datasets, and open challenges, and outline research avenues toward deeper RAG-Reasoning systems that are more effective, multimodally-adaptive, trustworthy, and human-centric.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义
- **研究动机**：大语言模型（LLM）面临两大核心局限——由静态、参数化知识存储导致的知识幻觉，以及处理真实世界复杂推理时的困难。
- **现有方法不足**：检索增强生成（RAG）虽然能注入外部知识提升事实性，但在需要多步推理的任务上表现乏力；纯推理方法（如链式思考）则容易产生事实错误与谬误。
- **核心观察**：知识缺失会阻碍推理，推理缺陷又会妨碍知识利用，二者天然耦合。早期工作多停留在单向增强：用推理优化RAG流水线（推理增强RAG），或用检索补充推理过程（RAG增强推理），但这些方法仍受限于“先检索后推理”的静态框架，存在检索准确性不稳定、推理深度受限、系统适应性不足等根本缺陷。
- **整体含义**：该综述从统一的推理-检索视角出发，系统梳理这两条路线的融合，特别着重于近年来兴起的“协同RAG-推理”框架——让LLM以智能体（agentic）方式交替进行搜索与思考，实现检索与推理的互促共进，进一步迈向兼具事实性和深度推理能力的系统。

### 方法论
论文是一篇综述，未提出新的方法，而是构建了一个三层分类体系，将现有工作统一在“推理-检索”视角下：

- **推理增强RAG（Reasoning → RAG）**：将推理能力注入RAG流水线的三个阶段。
  - **检索优化**：通过推理感知查询重写（分解、再造、扩展）、检索策略与规划（提前规划、自适应决策）、检索模型增强（利用结构知识或显式推理）提升检索质量。
  - **集成增强**：利用推理评估文档相关性、过滤噪音（如SEER、M-RAG-R），并融合多源证据（BeamAggR、DualRAG、CRP-RAG）。
  - **生成增强**：上下文感知合成（选择性利用上下文、构建推理路径）与扎根生成控制（事实核查、引用生成、忠实推理）以抑制幻觉。

- **RAG增强推理（RAG → Reasoning）**：利用外部或上下文内知识补全推理缺失前提。
  - **外部知识检索**：从知识库、网页、工具（计算器、API）获取事实或计算支持。
  - **上下文内检索**：利用先验经验（历史交互、成功策略）或示例/训练数据引导推理模式。

- **协同RAG-推理（RAG ⇔ Reasoning）**：智能体式迭代交替检索与推理。
  - **推理工作流**：链式（如IRCoT、CoV-RAG）、树式（思维树或蒙特卡洛树搜索如AirRAG、MCTS-RAG）、图式（图上漫游如LightRAG，或“图上思考”如ToG）等结构化多步推理范式。
  - **智能体编排**：单智能体（提示型如ReAct、Search-O1，微调型如INTERS，强化学习型如Search-R1、R1-Searcher）与多智能体（去中心化协作、中心化分层控制）。

综述梳理了各类方法的代表性工作，并整合了基准数据集与未来挑战。

### 实验设计
作为综述，本论文不包含原创实验，但系统整理了用于评估RAG-推理能力的**基准与数据集**：
- **代表性基准**（表1与表2）：涵盖Web浏览（BrowseComp、GAIA）、单跳问答（TriviaQA、NQ）、多跳问答（HotpotQA、MuSiQue、2WikiMultiHopQA）、多项选择问答（MMLU-Pro、QuALITY）、数学（MATH、AQuA）、代码（LiveCodeBench）以及事实核查、长文本QA、多模态QA、文本摘要、对话等任务。
- **对比方法**：论文通过分类体系对超过200篇相关工作进行定性比较，主要对比不同工作所属的增强路径（单向 vs 协同）、推理工作流（链/树/图）、智能体架构（单/多代理）等设计差异，而非定量实验对比。
- **评估维度**：基准覆盖了从简单事实检索到深层多步推理、多模态、动态环境（如网页浏览）等多维度能力要求，并特别关注同时依赖外部知识与内部推理的复杂场景。

### 资源与算力
- **论文未报告任何训练算力**，原因在于这是一篇文献综述，未进行新的模型训练或大规模实验。文中提到的所有方法（如Search-R1、INTERS等）的算力细节可追溯到原始论文，但本综述未汇总这些信息。

### 实验数量与充分性
- 综述自身并无实验，但从其覆盖范围看，它引用了超过200篇论文，涵盖了方法分类、基准与数据集。
- **充分性评价**：作为领域综述，其对现有工作的覆盖是广泛的，分类体系清晰，对方法的优劣与适用场景进行了较为全面的定性讨论。由于未进行定量实验，无法评价统计意义上的充分性或公平性；但其分类与对照为后续公平的系统性基准测试提供了基础框架。

### 主要结论与发现
1.  **三阶段进化路径**：RAG与推理的融合经历了“推理增强RAG → RAG增强推理 → 协同RAG-推理”的演进，从单向改进走向知识与推理的深度互锁。
2.  **协同框架是前沿**：以“Deep Research”产品为代表的协同RAG-推理系统，通过智能体迭代搜索与思考，在多跳推理、开放域问答、科学发现等知识密集型任务上取得领先表现。
3.  **工作流与编排的对比**：链式推理简洁但易错误传播，树式/图式方法能探索更多假设但开销更大；单智能体简单灵活，多智能体协同可增强鲁棒性与可扩展性，但带来协调成本。
4.  **现有基准的差距**：多数基准仍聚焦于文本、简单推理与通用领域，对多模态、真实工业场景、深层因果/反事实推理、检索-推理全过程的细粒度评估仍不足。
5.  **未来方向**：需提升推理效率（如潜在推理、深度压缩）、检索效率（预算感知、记忆缓存）、人机协同、多模态检索与推理、检索可信度与鲁棒性。

### 优点
- **统一框架**：将零散的RAG与推理融合研究整合为一个清晰的三级分类（推理增强RAG、RAG增强推理、协同系统），便于理解全局。
- **凸显协同趋势**：重点突出了智能体式“交替搜索-思考”的协同范式，把握了领域前沿（如Deep Research）。
- **丰富的基准梳理**：提供了跨13类任务、46个基准的详细列表，并总结了各基准的核心检索与推理挑战。
- **全面的结构对比**：对推理工作流（链/树/图）和智能体编排（单/多代理）的优势、局限和适用场景做了系统性比较（表6），具有较强的指导意义。

### 不足与局限
- **广度胜过深度**：为构建综合分类，对单项工作的技术细节、具体实现与细致的假设分析着墨较少，尤其是RAG和推理各自内部的细分领域（如稀疏/稠密检索、符号推理）。
- **缺乏定量基准测试**：未提供各类方法的统一实验对比，无法直观判断不同方法论在相同基准下的相对强弱。
- **未来方向较宽泛**：提出的研究机会（如效率、多模态、人本化）尚属方向性描述，未给出具体的评估标准或先行方案建议。
- **覆盖的时效性与偏见风险**：以2025年初的视角收录工作，部分最新进展（如基于RL的深度研究智能体）的深入分析有限；分类框架虽简明，但可能掩盖某些交叉方法的本质权衡。

（完）
