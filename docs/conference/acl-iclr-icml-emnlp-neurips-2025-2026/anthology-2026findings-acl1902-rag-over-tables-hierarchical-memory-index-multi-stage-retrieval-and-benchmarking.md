---
title: "RAG over Tables: Hierarchical Memory Index, Multi-Stage Retrieval, and Benchmarking"
title_zh: 表格上的RAG：层次记忆索引、多阶段检索与基准测试
authors: "Jiaru Zou, Dongqi Fu, Sirui Chen, Xinrui He, Zihao Li, Yada Zhu, Jiawei Han, Jingrui He"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1902.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 面向表格RAG的多阶段检索与推理组织
tldr: 现实世界中大量知识以表格形式存在，但表格RAG仍处于起步阶段，提出层次记忆索引与多阶段检索框架，有效理解表格间知识并组织上下文供LLM推理，同时构建了相应评测基准。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1902/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 838, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1902/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1657, \"height\": 667, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1902/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1393, \"height\": 701, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1902/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 675, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1902/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1638, \"height\": 1085, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1902/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1088, \"height\": 673, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1902/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1507, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1902/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1653, \"height\": 2097, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1645, \"height\": 698, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1647, \"height\": 454, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 681, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 684, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 475, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 414, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1643, \"height\": 489, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1643, \"height\": 489, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 794, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1902/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 800, \"height\": 388, \"label\": \"Table\"}]"
motivation: 表格知识分散，现有RAG难以处理跨表检索与推理。
method: 设计层次记忆索引和多阶段检索策略，组织复杂表格上下文用于LLM推理。
result: 在表格RAG任务上，方法提升了检索效率和答案准确性。
conclusion: 表格RAG的检索与推理组织方法为非结构化知识利用开辟新路。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances Large Language Models (LLMs) by integrating them with an external knowledge base to improve the answer relevance and accuracy. In real-world scenarios, beyond pure text, a substantial amount of knowledge is stored in tables, and user questions often require retrieving answers that are distributed across multiple tables. Retrieving knowledge from a table corpora (i.e., various individual tables) for a question remains nascent, for (i) how to understand intra- and inter-table knowledge effectively, (ii) how to filter unnecessary tables and retrieve the most relevant tables efficiently, (iii) how to organize complex retrieved contexts for LLMs’ reasoning, and (iv) how to evaluate the corresponding performance in a realistic setting. Facing the above challenges, in this paper, we first propose a table-corpora-aware RAG framework, named T-RAG, which consists of the hierarchical memory index, multi-stage retrieval, and graph-aware context organization for effective and efficient table knowledge retrieval and inference. Then, we develop a multi-table question answering benchmark named MultiTableQA, which spans 3 different task types, 57,193 tables, and 23,758 questions in total, and the sources are all from real-world scenarios. Based on MultiTableQA, we perform a comprehensive comparison of table retrieval methods, RAG-based approaches, and table-to-graph representation learning methods. T-RAG consistently achieves state-of-the-art accuracy, recall, and runtime performance, with improvements of up to 9.4%. Moreover, T-RAG yields an average inference gain of 11.8% across different downstream backbone LLMs. Our code and data are available at https://github.com/jiaruzouu/T-RAG.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：检索增强生成 (RAG) 被广泛用于增强大语言模型 (LLM)，但现实世界中大量知识以**表格**形式存在，且用户问题常需跨多张表格寻找答案。
- **核心问题**：如何从大规模表格语料库中有效检索并理解表内与表间知识，以支持复杂的跨表问答。现有 RAG 系统在处理表格数据时面临四大挑战：
    - 如何有效理解表内和表间的复杂知识结构。
    - 如何高效过滤无关表格并检索最相关的表格。
    - 如何组织复杂的检索上下文以供 LLM 推理。
    - 如何在一个贴近现实的场景下评估跨表检索与推理性能。

### 2. 论文提出的方法论

论文提出了一个名为 **T-RAG** 的表格语料感知 RAG 框架，核心包含三个协同组件：

- **层次记忆索引**
    - **表格线性化**：将表格的标题、列名等结构信息拼接成序列 \( s \)。
    - **多路特征提取**：为每个线性化的表格提取三种特征向量：语义特征、结构特征和启发式特征。
    - **异质超图构建**：通过 K-Means 聚类算法，分别在三种特征空间上将表格节点聚类，形成不同类型的超边，构建一个异质超图 \( G = (V, E) \)。
- **多阶段检索**
    - **粗粒度多路检索**：
        - 为每个聚类选择“典型节点”以降低计算复杂度。
        - 计算查询与各聚类典型节点的“代表性得分”（余弦相似度），选出最优聚类，并将来自不同特征空间的最优聚类合并，得到一个候选节点合集。
    - **细粒度子图检索**：
        - 基于上一步得到的候选节点，利用语义相似度构建一个稠密连接的局部子图。
        - 在此子图上运行**迭代式个性化 PageRank 算法**，以查询为个性化向量，对节点进行排序，最终筛选出最相关的表格集合。
- **图感知上下文组织**
    - **图信息注入**：在输入给 LLM 的提示词中，不仅包含检索到的表格内容，还明确了表格间的语义关系及相似度得分。
    - **层次化长思维链生成**：引导 LLM 分步推理：① 识别最相关表格；② 阐明查询与表格的联系；③ 检查具体行列信息，最终得出答案。

### 3. 实验设计

- **评测基准**：论文构建了一个名为 **MultiTableQA** 的多表问答基准，包含三种任务类型：
    - 表格事实核查 (TFV)
    - 单跳表格问答 (Single-hop TQA)
    - 多跳表格问答 (Multi-hop TQA)
    - 该基准源自真实世界的单表数据集，通过“源表格拆解”和“查询组合”技术，自动生成了包含 57,193 张表、23,758 个问题的大规模多表测试集，无需额外的人工标注。
- **对比方法**：论文将 T-RAG 与三大类基线方法进行了全面比较：
    - **表格检索方法**：DTR, Table-Contriever, Table-E5, Table-LLaMA。
    - **RAG 方法**：RALM, ColBERT。
    - **表格到图表示方法**：单一特征提取、Lattice、TAPAS、TaBERT。
- **泛化性测试**：还在 **Spider** 数据集上进行了额外的单表检索任务实验，以验证模型的鲁棒性。
- **下游 LLM 评估**：在多种前沿开源与闭源 LLM 上测试了下游推理性能，包括 Phi-3.5-mini, LLaMA-3.2-3B, Qwen-2.5-7B, LLaMA-3.1-8B, LLaMA-3.1-70B, Claude-3.5-Sonnet, GPT-4o-mini, GPT-4o。

### 4. 资源与算力

- 论文正文及附录中**未明确提及**实验所使用 GPU 的型号、数量或具体的训练/推理时长。效率分析部分仅报告了各组件在完整基准上的端到端延迟（分钟级别），但未说明所用的硬件环境。

### 5. 实验数量与充分性

- **实验数量丰富**：实验覆盖了**三类表格问答任务**，对比了**十多种基线方法**，并在**八个不同的下游 LLM** 上验证了推理性能。
- **消融实验**：设计了消融实验，验证了“图感知上下文组织”中各组件（图信息注入与长思维链）的有效性，并探讨了最终检索表数量 \( V_{\text{final}}^* \) 的影响。
- **参数研究**：对粗粒度检索的聚类数 K、典型节点数 k，以及细粒度检索的 PageRank 阻尼因子 α 和相似度阈值 τ 等关键超参数进行了敏感性分析。
- **公平性与客观性**：采用了统一的表格线性化方法和上下文提示词设置进行公平比较。对比方法覆盖了传统检索、RAG 及专用表格理解模型，体系较为完整。实验设计客观且充分。

### 6. 论文的主要结论与发现

- **检索性能顶尖**：T-RAG 在 MultiTableQA 的所有任务上均取得了最优 (SOTA) 的检索准确率和召回率，相较于最强基线，性能提升最高可达 9.4%。
- **推理性能增益显著**：采用 T-RAG 检索结果能为下游 LLM 带来平均 **11.2%** 的推理性能提升，且该增益在不同规模的多种 LLM 上表现一致。
- **检索效率高**：通过多阶段（粗到细）检索策略，T-RAG 在高效过滤大量无关表格的同时，保持了与传统方法可比甚至更优的端到端延迟。
- **泛化能力良好**：T-RAG 不仅在自建的 MultiTableQA 上表现优异，也能很好地泛化到 Spider 这类标准数据集上。
- **跨表理解能力**：传统的纯文本 RAG 方法在表格检索上表现不佳，而 T-RAG 通过图结构建模表间关系，有效解决了这一问题。

### 7. 优点

- **创新性强**：首次完整地提出并解决了面向大规模表格语料库的 RAG 框架，包括索引、检索和上下文组织的全流程。
- **方法设计巧妙**：构建异质超图来组织表格，并通过“粗到细”的多阶段检索策略，在保证高召回的同时提升了检索效率。
- **基准测试集价值高**：提出的 MultiTableQA 通过自动化、无人工成本的方式构建了大规模、真实场景驱动的多表问答测试集，为后续研究提供了有价值的评估平台。
- **实验全面扎实**：与多种范式的基线进行了广泛对比，并深入进行了消融研究和参数分析，结论令人信服。

### 8. 不足与局限

- **计算开销**：细粒度的子图检索（PageRank）在处理超大规模表格时延迟较高，可能成为瓶颈。
- **超参数依赖**：部分超参数（如相似度阈值 τ）在不同任务上的最优值有差异，需要根据任务进行调整。
- **构造数据的内在联系**：MultiTableQA 的表格由单表拆分而来，这天然保证了子表间存在联系，但可能与真实世界中完全独立、异构表格间的松散关系有所不同。
- **静态图结构**：当前的超图是静态构建的，没有讨论表格语料库动态更新时的增量索引和检索问题。
- **算力信息缺失**：论文未提供硬件和算力消耗的细节，使得结果难以精确复现。

（完）
