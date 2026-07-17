---
title: "Reasoning with Memory: Adaptive Information Management for Retrieval-Augmented Generation"
title_zh: 记忆推理：面向检索增强生成的自适应信息管理
authors: "Hieu Man, Ro-ee Tal, Abhishek Kumar, Jaejin Cho, Benjamin Hsu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1834.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 显式工作记忆作为动态认知推理空间
tldr: 针对多跳检索增强生成中链条增长时中间推理状态难以维持的问题，提出状态感知RAG，通过显式工作记忆和路径-结果双重奖励机制动态过滤与整合信息，使冻结的检索器和生成器仍能连贯推理，在复杂问答中提升推理稳定性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1834/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1608, \"height\": 613, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1834/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 724, \"height\": 702, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1834/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 256, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1834/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 247, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1834/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 1068, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1834/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 649, \"height\": 530, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1834/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 651, \"height\": 672, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1834/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1353, \"height\": 1113, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1834/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 665, \"height\": 680, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1834/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 492, \"height\": 575, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1834/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 442, \"height\": 285, \"label\": \"Table\"}]"
motivation: 多跳RAG中长链条导致中间推理状态混乱，缺乏有效信息管理。
method: 提出状态感知RAG，引入可训练提取器动态更新工作记忆，采用路径-结果双重奖励平衡局部连贯性与全局策略。
result: 在复杂多跳推理任务中，工作记忆有效维持推理状态，超越现有方法。
conclusion: 显式记忆管理为RAG系统提供了更稳定的推理支撑，实现了即插即用。
---

## Abstract
Multi-hop reasoning remains a fundamental challenge for Retrieval-Augmented Generation (RAG) systems. Recent approaches—from adaptive retrieval to agentic pipelines—struggle to maintain coherent intermediate reasoning states as chains grow longer. We introduce State-Aware RAG, a framework that addresses this limitation through an explicit working memory that serves as a dynamic cognitive workspace for reasoning. Our modular architecture features a lightweight, trainable extractor that learns to actively filter, consolidate, and update this working memory via a novel Path-Outcome Dual Reward paradigm, which balances local coherence with global strategy. The retriever and generator remain frozen, enabling plug-and-play flexibility. Experiments on eight QA benchmarks demonstrate state-of-the-art results, on average achieving +8.6% over the best memory-augmented baseline and +9.3% over the best RL-enhanced baseline. Our architecture generalizes seamlessly to stronger generators and retrievers without retraining, establishing dynamic memory management as a critical yet underexplored dimension for advancing RAG systems.

---

## 论文详细总结（自动生成）

好的，根据你提供的论文内容，以下是结构化的中文总结。

### 1. 论文的核心问题与整体含义

*   **核心问题：** 现有多跳推理检索增强生成（RAG）系统在处理长链式推理时，普遍存在中间推理状态不一致的问题。这些系统主要专注于“如何获取”信息，却忽略了“如何管理”信息。检索到的文档只是被静态地附加到上下文中，导致无关、冗余或矛盾信息在多个推理步骤中累积，最终造成上下文污染和推理漂移。
*   **研究动机：** 现有的记忆增强RAG方法（如构建静态知识图谱或进行一次性全局压缩）无法动态适应不断演变的推理轨迹，缺乏对每个步骤的记忆进行主动筛选和整合的能力。
*   **整体含义：** 论文提出动态记忆管理是多跳RAG系统中的一个关键但尚未被充分探索的维度。通过引入类似认知科学中“工作记忆”的机制，可以让模型在推理过程中主动维护一个持久、动态更新的知识工作空间，从而显著提升复杂问答的准确性和连贯性。

### 2. 论文提出的方法论

论文提出了名为“状态感知RAG”的框架，其核心思想与关键技术细节如下：

*   **核心思想：显式工作记忆**
    *   在RAG系统中引入一个全局、持久且动态更新的“工作记忆” (M_i)。这个记忆状态会贯穿整个推理轨迹，持续进行信息筛选、整合和更新，而不是简单地累积文档。
    *   系统的状态定义为 S_i = (q_i, r_i, M_i)，其中q_i是当前子问题，r_i是中间回答，M_i是更新后的记忆。

*   **模块化架构与即插即用**
    *   框架由三个核心代理（Agent）组成：
        1.  **检索器（Retriever）**：根据查询从语料库中检索候选文档。
        2.  **生成器（Generator）**：根据当前状态生成中间回答和下一个子问题。
        3.  **提取器（Extractor）**：核心训练模块，它是一个轻量级、可训练的组件，负责执行记忆管理操作，包括**信息整合**（从检索文档中筛选相关信息）和**记忆更新**（将新知识整合到工作记忆中）。
    *   **关键设计**：在训练和推理时，检索器和生成器均保持**冻结状态**，仅训练提取器，实现了高灵活性和即插即用能力。

*   **核心算法：路径-结果双重奖励**
    *   为解决多步推理中的时序信用分配问题，论文设计了一种强化学习训练范式，结合两种奖励信号联合优化提取器：
        1.  **路径奖励（Path Reward）**：评估每个推理步骤的局部连贯性，即提取的信息是否有助生成器正确回答当前子问题。
        2.  **结果奖励（Outcome Reward）**：评估最终答案相对于标准答案的整体是否正确。
    *   训练目标是最大化累积奖励：\(\frac{1}{n-1} \sum_{i=1}^{n-1} [R_p(q_i, r_i) + \lambda R_o(y, x, y^*)]\)。其中，\(R_p\)为路径奖励，\(R_o\)为结果奖励，\(\lambda\)是平衡局部连贯性与全局策略的系数。

*   **推理模式**
    *   **苏格拉底式规划**：单链式推理，计算效率高，适用于简单任务。
    *   **蒙特卡洛树搜索（MCTS）**：支持多种动作类型（分解回答、整合、精炼、重定向、结论）以进行系统性探索，适用于复杂任务。其关键特性是工作记忆在搜索树的分支间全局共享。

### 3. 实验设计

*   **数据集/场景：** 在8个问答基准上进行了评估。
    *   **多跳推理基准：** 2WikiMultihopQA、HotpotQA、MuSiQue、Bamboogle。
    *   **单跳推理基准：** SimpleQA、Natural Questions (NQ)、TriviaQA、PopQA。
*   **对比方法（七大类）：**
    1.  **直接生成**：Qwen3-8B、思维链（CoT）提示。
    2.  **标准RAG**：基础RAG和RAG+重排序。
    3.  **迭代式检索**：IR-CoT、FLARE、Search-o1。
    4.  **查询重写**：Self-RAG、RaFe。
    5.  **规划增强RAG**：MCTS-RAG、RAG-Star。
    6.  **强化学习增强RAG**：Search-R1、S3。
    7.  **记忆增强RAG**：MemorAG、HippoRAG、HippoRAG 2。
*   **评价指标：**
    *   **Sub-EM**：字符串精确匹配。
    *   **Acc. (准确率)**：使用Claude 3.7 Sonnet作为评判器的语义准确率。

### 4. 资源与算力

*   **模型配置：**
    *   **生成器**：Qwen3-8B
    *   **检索器**：Qwen3-Embedding-4B
    *   **提取器**：Qwen3-4B
*   **算力/训练时长：** **文中未明确提及**所使用的GPU型号、数量或具体的训练时长。文中仅说明使用了`verl`框架进行强化学习训练，采用张量并行（Tensor Parallel）和序列并行（Sequence Parallel），但这未直接说明硬件配置。

### 5. 实验数量与充分性

*   **主实验：** 在8个数据集上与超过15种基线方法进行了对比，验证了整体框架的优越性。实验覆盖多跳与单跳场景，较为全面。
*   **消融实验：**
    1.  **记忆管理组件消融**：验证了提取器、信息整合和记忆更新各自的贡献。
    2.  **训练策略消融**：对比了仅提示、仅SFT、结果奖励RL、路径奖励RL和双重奖励RL的效果。
*   **组件分析实验**：验证了冻结提取器对不同规模生成器（8B -> 30B、Claude 3.7 Sonnet）和不同检索器/搜索源的泛化能力。
*   **推理过程分析**：研究了推理步数和MCTS探索次数对性能的影响，并分析了Socratic与MCTS模式的成本效益。
*   **充分性与公平性评价**：实验设计逻辑清晰，从整体有效性、模块贡献、训练策略到系统可扩展性均做了详细验证，非常充分且客观。

### 6. 论文的主要结论与发现

*   **性能优势显著：** 状态感知RAG在8个基准上取得了最优结果。在多跳QA上，平均准确率比最佳记忆增强基线（HippoRAG 2）高8.6%，比最佳RL增强基线（S3）高9.3%。
*   **动态记忆管理至关重要：** 消融实验证明，移除提取器（即无动态记忆管理）会导致性能大幅下降，而主动的信息筛选和整合更是防止记忆污染的关键。
*   **双重奖励机制有效**：路径-结果双重奖励优于任何单一奖励信号，有效平衡了局部推理质量与全局任务成功。
*   **强大的可扩展性和即插即用能力**：训练好的提取器可以无需重新训练，直接与新升级的更强大生成器或检索器配合使用，并获得性能提升。

### 7. 优点

*   **创新性视角：** 区别于主流关注“信息获取”的方法，论文开创性地聚焦于“信息管理”，引入工作记忆范式解决多跳推理中的上下文污染问题。
*   **模块化与即插即用：** 只训练一个轻量级提取器而冻结核心的检索器和生成器，这一设计非常实用，大幅降低了部署和升级成本。
*   **训练策略先进：** 提出的路径-结果双重奖励巧妙地结合了过程监督和结果监督的优势，为多步推理任务的强化学习训练提供了有效思路。
*   **验证充分：** 实验不仅展示了最终结果，还通过详尽的消融、组件拓展和推理过程分析，深入剖析了方法有效性的内在原因。

### 8. 不足与局限

*   **训练成本高昂：** 使用大语言模型作为评判器（LLM-as-a-Judge）来计算奖励信号需要大量推理开销，限制了训练的可扩展性。
*   **检索质量是性能瓶颈：** 论文分析明确指出，即使有完美的记忆管理，也无法弥补由于信息未被检索到而造成的缺失。当用谷歌搜索替换静态维基百科语料库时，性能有巨大提升（+22.2%），这揭示了知识源覆盖率和排名的根本性限制。
*   **泛化能力待验证：** 论文主要在问答任务上进行了验证，其在其他领域（如科学文献、企业文档）和其他推理密集型任务（如对话）上的效果尚不明确。
*   **推理成本与效益权衡**：MCTS推理模式虽然更准确，但计算成本约为Socratic模式的7倍，而准确率提升相对有限（仅2.6个点）。Socratic模式在成本效益比上可能更具优势。
*   **提取器能力上限：** 实验显示，使用小型模型训练的提取器与使用Claude 3.7 Sonnet作为提取器的性能之间仍存在差距，表明提取器的规模是进一步提升性能的一个方向。

（完）
