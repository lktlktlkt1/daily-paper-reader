---
title: "ImpRAG: Retrieval-Augmented Generation with Implicit Queries"
title_zh: ImpRAG：基于隐式查询的检索增强生成
authors: "Wenzheng Zhang, Xi Victoria Lin, Karl Stratos, Wen-tau Yih, Mingda Chen"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.472.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: ImpRAG通过整合检索与生成消除显式查询
tldr: 传统RAG将检索与生成分离并要求显式查询，限制了泛化能力。ImpRAG提出无查询RAG系统，将检索与生成统一到一个模型中，通过隐含表达信息需求，利用预训练解码器模型的分层分组和两阶段推理同时优化检索与生成任务，提升了跨任务泛化性能，为RAG范式提供了更整合的方案。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.472/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 767, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.472/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 553, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.472/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1658, \"height\": 609, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.472/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1657, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.472/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1659, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.472/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1360, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.472/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1658, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.472/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 708, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.472/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 589, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.472/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 582, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.472/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 806, \"height\": 159, \"label\": \"Table\"}]"
motivation: 传统RAG中检索与生成分离且依赖显式查询，限制了模型泛化能力。
method: 提出无查询RAG系统ImpRAG，将检索与生成集成于同一模型，利用分层分组和两阶段推理。
result: 实验表明该方法在多个任务上实现了高效的检索增强生成，且无需人工查询。
conclusion: ImpRAG通过隐式查询统一检索与生成，简化了RAG流程并提升泛化性。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems traditionally treat retrieval and generation as separate processes, requiring explicit textual queries to connect them. This separation can limit the ability of models to generalize across diverse tasks. In this work, we propose a query-free RAG system, named ImpRAG, which integrates retrieval and generation into a unified model. ImpRAG allows models to implicitly express their information needs, eliminating the need for human-specified queries. By dividing pretrained decoder-only language models into specialized layer groups, ImpRAG optimizes retrieval and generation tasks simultaneously. Our approach employs a two-stage inference process, using the same model parameters and forward pass for both retrieval and generation, thereby minimizing the disparity between retrievers and language models. Experiments on 8 knowledge-intensive tasks demonstrate that ImpRAG achieves 3.6-11.5 improvements in exact match scores on unseen tasks with diverse formats, highlighting its effectiveness in enabling models to articulate their own information needs and generalize across tasks. Our analysis underscores the importance of balancing retrieval and generation parameters and leveraging generation perplexities as retrieval training objectives for enhanced performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- 传统检索增强生成系统将检索和生成视为两个独立过程，依赖于人类指定的显式文本查询来连接。
- 这种分离限制了模型在新任务和新格式上的泛化能力，因为人类必须替模型表达信息需求，而非模型自身决定。
- 论文提出一个根本性问题：能否构建一个无查询的RAG系统，让模型隐式表达自身信息需求，从而无需人为设计查询模板，提升跨任务泛化性能。

### 2. 论文提出的方法论

- 核心思想：**ImpRAG**，一个将检索与生成统一到单个解码器语言模型中的系统，共享同一套模型参数与一次前向传播。
- 架构设计：将预训练LLM（如LLaMA）切分为三个层组：
  - **底层（LB）**：作为检索器，对最后的token做池化得到查询嵌入，利用点积计算与段落的相关性。
  - **中层（LM）**：作为阅读器，引入跨注意力（cross-attention）机制融合检索到的段落信息。
  - **顶层（LT）**：禁用跨注意力以降低计算开销，仅用于生成。
- 训练目标：联合优化生成损失和检索损失：
  - **生成损失**：标准因果语言模型损失。
  - **检索损失**：两阶段训练：
    1. **预热阶段**：使用强检索器（Contriever‑MSMARCO）生成的伪标签，采用多标签NCE损失训练初始检索能力。
    2. **自蒸馏阶段**：利用语言模型困惑度（perplexity）作为软目标，通过KL散度提升检索质量，并与生成目标联合训练。
- 推理过程：两阶段推理：
  1. 底层编码查询并检索相关段落。
  2. 对检索到的段落进行跨注意力解码生成回答；查询嵌入只在输入结束时计算一次。

### 3. 实验设计

- **数据集**：
  - 训练：知识检索任务（NaturalQuestions、HotpotQA）和不需检索的指令调优数据集（对话、阅读理解、摘要、短语去噪、句子生成等），均取子集5000条。
  - 评估：8个知识密集型任务，涵盖基础问答（NQ、SimpleQA）、多跳推理（HotpotQA、2WikiMultiHopQA）、指令跟随（T-REx、ZsRE、FEVER、AIDA）。报告精确匹配和检索召回率。
- **对比基线**：
  - **RA‑IT**：直接使用检索段落增强指令调优。
  - **RA‑DIT**：先对检索器微调，再结合LLM进行指令调优。
  - **RA‑DIT‑Llama**：将RA‑DIT的检索器替换为LLaMA前8层做检索。
- **基础模型**：LLaMA‑3.2 3B 和 LLaMA‑3.1 8B。

### 4. 资源与算力

- 使用 **NVIDIA H100 GPU**。
- 每轮训练需 **8块H100**，索引服务需额外8块GPU。
- 基线训练约 **96 GPU小时**，ImpRAG训练约 **160 GPU小时**。

### 5. 实验数量与充分性

- **主要实验**：两个模型规模 × 4种方法（含ImpRAG），共8组。
- **消融实验**：
  - 层组边界b和t的影响（Llama‑3.2 3B）。
  - 检索目标（仅自蒸馏、仅预热、两者联合）。
  - 查询模板对基线的影响。
  - 指令调优数据集组合的影响。
- 另探讨了段落编码策略、段落表示冻结、KV状态压缩等技术细节。
- 实验覆盖多个维度，对比基线公平，消融充分，能支持主要结论。

### 6. 论文的主要结论与发现

- 与传统RAG方法相比，ImpRAG在所有8个任务上性能均有提升，尤其在未见任务上提升显著（3.6‑11.5个精确匹配点，5.0‑23.2个检索召回点）。
- 统一的模型有效将生成任务中的监督信号传递给检索任务，提升了跨任务泛化能力。
- 平衡检索和生成的层参数、利用生成困惑度作为检索目标，以及合理的指令调优数据是关键。

### 7. 优点

- **消除显式查询**：模型可通过隐式表示学习信息需求，减少对人工设计的依赖，提高对新任务的适应性。
- **架构统一**：共享参数，减少检索器和生成器之间的不匹配，简化部署。
- **训练策略创新**：两阶段训练（伪标签预热 + 自蒸馏）有效结合外部监督和自监督信号。
- **实验扎实**：在多个知识密集任务和不同模型规模上验证，消融实验深入，有说服力。

### 8. 不足与局限

- **仅单步检索**：未探索迭代或多跳检索，限制了在复杂推理任务上的潜力。
- **模型规模与架构单一**：只在LLaMA‑3系列模型上验证，未扩展到其他架构或更大模型。
- **训练依赖外部检索器**：预热阶段需要Contriever‑MSMARCO生成伪标签，若无强检索引擎可能影响起步性能。
- **效率问题**：索引服务需额外GPU，训练时间高于普通指令调优基线，但仍处于可控范围。
- 由于评估任务主要是知识密集型，对于其他类型的生成任务（如创意写作）的适用性有待检验。

（完）
