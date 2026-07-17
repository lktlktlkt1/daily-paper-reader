---
title: A Comparison of Independent and Joint Fine-tuning Strategies for Retrieval-Augmented Generation
title_zh: 检索增强生成中独立与联合微调策略的比较
authors: "Neal Gregory Lawton, Alfy Samuel, Anoop Kumar, Daben Liu"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1247.pdf"
tags: ["query:agentic-rag"]
score: 6.0
evidence: 评估RAG嵌入与生成模型微调策略的比较分析
tldr: 针对RAG流水线中嵌入模型和生成模型的微调策略选择问题，系统比较了独立微调、联合微调和两阶段微调。实验表明不同策略在多数任务上性能相当，但在计算成本和实现复杂度上存在差异，为实践者按需选择提供了依据。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1247/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 728, \"height\": 319, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1247/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1509, \"height\": 917, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1247/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1295, \"height\": 801, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1247/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1461, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1247/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 465, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1247/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1667, \"height\": 1494, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1247/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1667, \"height\": 1494, \"label\": \"Table\"}]"
motivation: RAG微调存在多种策略但缺乏系统性优劣对比，实际选择困难。
method: 设计并评估独立微调、联合微调和两阶段微调三种策略对RAG性能的影响。
result: 各类策略在多个基准上性能相当，但训练效率和部署成本差异明显。
conclusion: 工作为RAG微调策略的选择提供了经验性指导，帮助在资源与效果间取得平衡。
---

## Abstract
Retrieval augmented generation (RAG) is a popular framework for question answering that is powered by two large language models (LLMs): an embedding model that retrieves context documents from a database that are relevant to a given question, and a generator model that uses the retrieved context to generate an answer to the question. Both the embedding and generator models can be fine-tuned to increase performance of a RAG pipeline on a new task, but multiple fine-tuning strategies exist with different costs and benefits. In this paper, we evaluate and compare several RAG fine-tuning strategies, including independent, joint, and two-phase fine-tuning. In our experiments, we observe that all of these strategies achieve about equal improvement in EM and F1 generation quality metrics, although they have significantly different computational costs. We conclude the optimal fine-tuning strategy to use depends on whether the training dataset includes context labels and whether a grid search over the learning rates for the embedding and generator models is required.

---

## 论文详细总结（自动生成）

好的，请查收基于您提供的论文内容生成的结构化总结。

## 论文核心问题与整体含义

本文聚焦于**检索增强生成（RAG）流水线的微调策略选择问题**。一个典型的RAG流水线包含两个可独立微调的大语言模型（LLM）组件：用于检索相关上下文的嵌入模型和用于生成答案的生成器模型。虽然微调这两个组件都能提升下游任务表现，但存在独立、联合、两阶段等多种微调策略，且各自的成本与收益不同。论文旨在通过系统性比较这些策略，为实践者提供明确的选择指导，即：在什么条件下应使用哪种微调策略，以达到性能与计算成本的最佳平衡。

## 论文提出的方法论

本文并非提出新的微调算法，而是**对现有策略进行组合、比较与分析**。具体评估的策略包括：

1.  **独立微调策略**：分别独立地对嵌入模型和生成器模型进行微调，是计算成本最低的方案。
    *   **嵌入模型微调**：使用有标注的`(问题，上下文)`对，通过最小化问题与相关文档的嵌入向量距离（最大化相似度）来优化嵌入模型。
    *   **生成器模型微调**：使用`(问题，上下文，答案)`三元组，通过最小化答案的负对数似然来优化生成器模型。

2.  **联合微调策略**：使用端到端方法同时优化嵌入和生成器模型，无需上下文标签。
    *   **技术细节**：利用 **RAG-Token** 或 **RAG-Sequence** 方法，将检索与生成过程建模为一个可对嵌入和生成器模型参数同时求导的简化概率模型。其核心思想是，奖励那些能检索到真正提升答案预测准确度的上下文的嵌入模型。
    *   **超参数**：使用两个独立的学习率分别控制嵌入和生成器模型的参数更新。

3.  **两阶段微调策略**：结合了独立和联合微调的思想。
    *   **第一阶段**：冻结嵌入模型，使用RAG-Token仅微调生成器模型。
    *   **第二阶段**：冻结生成器模型，使用RAG-Token仅微调嵌入模型（奖励其检索到有助生成器性能的文档）。

所有策略均使用**网格搜索**来寻找接近最优的学习率。为提高效率，联合微调实验直接复用了两阶段微调实验中搜索到的学习率。

## 实验设计

*   **数据集与场景**：在**HotPotQA**和**PopQA**两个问答基准数据集上评估。检索库为经过与先前工作相同方式分块处理后的维基百科（约2990万个文档块）。
*   **RAG流水线配置**：构建了4种不同的RAG流水线进行对比，以验证方法的普适性。组合方案为两种嵌入模型与两种生成器模型的笛卡尔积：
    *   **嵌入模型**：**MPNet**， **MiniLM**
    *   **生成器模型**：**LLaMA-3-8B-Instruct**，**Mistral-7B-Instruct-v0.1**
*   **对比方法（基线与策略）**：
    *   `No Ft.`：未经任何微调的基线。
    *   `Ft. Embed.`：仅微调嵌入模型。
    *   `Ft. Gen.`：仅微调生成器模型。
    *   `Indp.`：组合独立微调后的嵌入和生成器模型。
    *   `2-Phase`：两阶段微调策略。
    *   `RAG-Seq.` & `RAG-Tok.`：两种联合微调方法。

## 资源与算力

*   **硬件环境**：每个实验在一个配备**8张NVIDIA A10 GPU**的节点上进行。
*   **训练详情**：
    *   为控制计算开销，所有实验**仅微调1个epoch**。
    *   生成器模型微调采用**QLoRA**技术（秩为16，4比特量化），以进一步降低资源消耗。
    *   **训练时长**：不同策略的计算成本差异巨大。例如，平均而言，独立微调嵌入模型仅需数小时，而两阶段联合微调耗时是独立微调总和的近两倍（如在HotPotQA上，独立微调总耗时约27.4小时，两阶段为61小时）。

## 实验数量与充分性

*   **实验数量**：论文在**2个数据集 x 4种模型组合 x 7种微调方法**的配置下进行了主实验，并针对每组实验进行了学习率网格搜索。此外还包括损失收敛验证等辅助实验，实验组数比较充分。
*   **充分性与公平性**：
    *   **公平性**：所有策略使用相同的RAG流水线基础组件、数据集和评估指标（验证集上的精确匹配EM、F1分数和Recall@5），确保了对比的公平性。联合微调复用两阶段微调的学习率，虽降低了计算成本，可能对联合微调略有不公，但作者已在比较中指出了这一点。
    *   **充分性**：通过多模型、多数据集的交叉验证，增强了结论的普适性。对训练时间成本的记录也使得对比更为全面。

## 论文的主要结论与发现

1.  **性能相当，成本各异**：独立、联合和两阶段微调在最终的生成质量指标（EM和F1）上**性能近乎相同**，但所需的计算成本**差异显著**。独立微调的成本最低，其次是联合微调，两阶段微调最高。
2.  **选择策略的关键因素**：最优策略的抉择取决于两个实际条件：
    *   **是否拥有上下文标签**：若有，应首选成本最低的**独立微调**。
    *   **是否已知合适的学习率**：若无上下文标签但已知合适的学习率，应使用成本较低的**联合微调**；若两者都未知，则应使用**两阶段微调**，因为它允许对嵌入和生成器模型的学习率进行独立且高效的网格搜索。
3.  **微调效果的组分分析**：单独微调生成器模型能显著提升EM和F1；单独微调嵌入模型能显著提升召回率（Recall@5），并带来一定的下游指标增益，但其计算成本远低于微调生成器模型。

## 优点

1.  **实践指导性强**：论文清晰地给出了一个基于资源条件（有无标签）和超参数先验知识的策略选择流程图，对应用开发者极具参考价值。
2.  **实验设计扎实**：通过组合多种嵌入模型和生成器模型，在多个数据集上进行实验，证明了结论的鲁棒性，避免了依赖单一模型得出偏颇结论。
3.  **对比维度全面**：不仅关注最终性能，还详细记录和比较了不同策略的**计算时间成本**，提供了更实际的视角。
4.  **启发性发现**：观察到使用上下文标签直接微调嵌入模型的召回率表现可能不如不使用标签的端到端方法，为嵌入模型训练提供了有意思的研究线索。

## 不足与局限

1.  **实验规模有限**：为节省算力，所有实验仅微调了1个epoch，虽然论文展示了损失快速收敛的证据，但未探索更多epoch下的性能上限和过拟合风险。
2.  **RAG流水线过于基础**：实验仅使用“检索-生成”的基础单步RAG。现实中常包含重排序、多步推理等复杂模块，本文结论能否扩展到更复杂的RAG流水线尚不清楚。
3.  **超参数搜索不彻底**：仅对学习率进行了网格搜索，而批次大小、训练轮数等其他关键超参数未作优化。特别是对于嵌入模型的对比学习，批次大小对其性能影响很大，文中使用的小批次可能未发挥其最佳性能。
4.  **生成器微调方法单一**：生成器始终采用QLoRA微调，未与其他参数高效微调方法或全量微调进行对比，这可能会影响结论的通用性。
（完）
