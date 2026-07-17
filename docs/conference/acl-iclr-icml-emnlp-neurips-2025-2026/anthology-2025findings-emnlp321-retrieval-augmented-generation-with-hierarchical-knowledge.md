---
title: Retrieval-Augmented Generation with Hierarchical Knowledge
title_zh: 基于层次知识的检索增强生成
authors: "Haoyu Huang, Yongfeng Huang, Yang Junjie, Zhenyu Pan, Yongqiang Chen, Kaili Ma, HongZhi Chen, James Cheng"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.321.pdf"
tags: ["query:agentic-rag"]
score: 7.0
evidence: 引入利用层次知识改进索引和检索的RAG方法
tldr: 针对现有图增强RAG方法未能有效利用人类认知中天然存在的层次知识的问题，本文提出HiRAG。HiRAG设计了一套层次化知识索引机制，在检索前构建概念与实体间的层级关系，并在检索时同时考虑语义相似性与结构层级，从而提升检索结果的相关性与深度。在多个公开数据集上进行评估，结果显示HiRAG相较于最新基线模型取得了显著一致的性能提升，证明了层次知识在检索增强生成中的巨大潜力。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.321/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 514, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.321/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1653, \"height\": 855, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.321/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1332, \"height\": 615, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.321/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 588, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.321/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 662, \"height\": 352, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.321/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 731, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.321/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1566, \"height\": 1870, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.321/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1647, \"height\": 1567, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.321/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 780, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.321/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1403, \"height\": 773, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.321/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 790, \"height\": 155, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.321/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 800, \"height\": 407, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.321/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1647, \"height\": 1450, \"label\": \"Table\"}]"
motivation: 现有RAG方法未充分挖掘认知中的层次结构知识。
method: 提出HiRAG，在索引和检索中利用层次知识增强语义与结构理解。
result: 实验证明HiRAG相对于基线方法取得显著性能提升。
conclusion: 层次知识能有效提升RAG的检索和生成效果。
---

## Abstract
Graph-based Retrieval-Augmented Generation (RAG) methods have significantly enhanced the performance of large language models (LLMs) in domain-specific tasks. However, existing RAG methods do not adequately utilize the naturally inherent hierarchical knowledge in human cognition, which limits the capabilities of RAG systems. In this paper, we introduce a new RAG approach, called HiRAG, which utilizes hierarchical knowledge to enhance the semantic understanding and structure capturing capabilities of RAG systems in the indexing and retrieval processes. Our extensive experiments demonstrate that HiRAG achieves significant performance improvements over the state-of-the-art baseline methods.

---

## 论文详细总结（自动生成）

好的，以下是对该论文的结构化、深入、客观的中文总结。

### 1. 论文的核心问题与整体含义

*   **研究背景**：基于图的检索增强生成方法旨在通过构建知识图谱来显式建模文本块中实体间的关系，从而增强大语言模型在特定领域或知识密集型任务中的表现，缓解“幻觉”问题。
*   **核心问题**：现有基于图的RAG系统未能充分利用人类认知中天然存在的**层次化知识**，这导致了两个关键挑战：
    1.  **语义相近但结构疏远**：知识图谱中语义高度相关的实体（如“大数据”和“推荐系统”）可能因语料驱动的构建方式而在图结构中相距甚远，导致检索时无法有效关联。
    2.  **局部与全局知识鸿沟**：现有方法分别从局部（特定实体描述）和全局（社区摘要）层面检索知识，但未能弥合这两层知识之间的内在差异。将不协调的局部与全局信息直接提供给LLM，可能导致推理脱节、答案不完整甚至相互矛盾。
*   **整体含义**：本文旨在开发一种能够整合层次知识的新RAG框架，以增强索引和检索过程中的语义理解和结构捕获能力。

### 2. 论文提出的方法论

该论文提出了一个名为 **HiRAG** 的框架，其核心思想是通过构建和利用层次化知识图谱来解决上述挑战。HiRAG包含两个关键模块：

*   **HiIndex：层次化知识索引**
    *   **核心思想**：不局限于扁平的原始知识图谱，而是自底向上逐层构建一个层次化知识图谱。高层节点是其下层节点集群的摘要，能够增强语义相似实体间的连通性。
    *   **技术流程**：
        1.  **构建基础知识图谱**：从文档中提取实体和关系，构成第`0`层图。
        2.  **递归构建高层**：对于第`i`层（`i >= 1`），首先使用**高斯混合模型**对第`i-1`层的实体根据其语义嵌入进行聚类。
        3.  **生成摘要实体**：将每个聚类中的实体描述输入LLM，并利用一组预定义的元摘要实体（如“组织”、“技术”）进行引导，生成该聚类的摘要实体，作为第`i`层的新节点。
        4.  **建立层间关系**：在聚类内的下层实体和新生成的上层摘要实体之间创建关系边。
        5.  **终止条件**：通过计算“集群稀疏度”及其变化率来自动决定构建的层数`k`。当稀疏度变化低于阈值（如5%）时停止，表示聚类质量不再提升。
        6.  **社区检测**：在最终的层次化知识图谱上应用Leiden算法进行社区发现，高层节点作为语义桥梁，使得语义相似但结构疏远的低层实体能被划入同一社区。

*   **HiRetrieval：层次化知识检索**
    *   **核心思想**：检索三层知识（局部、全局、桥梁）作为LLM的上下文，以有效弥合知识鸿沟。
    *   **技术流程**：
        1.  **局部知识**：从层次化知识图谱中检索与查询语义最相关的前`n`个实体描述。
        2.  **全局知识**：找到包含这些局部实体的社区，并检索其社区报告。
        3.  **桥梁知识**：为解决局部与全局知识的鸿沟，该方法从每个检索到的社区中选择与查询最相关的前`m`个关键实体，然后在知识图谱中找到连接这些关键实体的**最短路径**。这些路径上的三元组（头实体、关系、尾实体）构成了桥接层知识。
        4.  **生成**：将这三层知识作为上下文提供给LLM，生成最终答案。

### 3. 实验设计

*   **数据集**：实验使用了来自 **UltraDomain** 基准的四个领域特定长文本数据集：**Mix**、**CS**、**Legal**和**Agriculture**。此外，为了客观评估QA性能，还使用了两个多跳问答数据集：**HotpotQA** 和 **2WikiMultiHopQA**。
*   **对比方法**：与多种最先进和流行的RAG基线方法进行了比较：
    *   **NaiveRAG**：基于向量搜索的文本块检索。
    *   **GraphRAG**：利用社区检索全局知识（使用本地搜索模式）。
    *   **LightRAG**：结合全局和局部知识的双层级检索。
    *   **FastGraphRAG**：整合KG和个性化PageRank的方法。
    *   **KAG**：利用人工标注模式进行结构化推理的专业领域框架。
    *   **消融变体**：`w/o HiIndex`（用扁平KG替换层次KG）和 `w/o Bridge`（不使用桥梁知识）。
*   **评估模型与指标**：
    *   **LLM评判**：使用 **GPT-4o** 等多个强力LLM作为评估模型，从**全面性、赋能性、多样性、总体**四个维度比较不同方法生成答案的**胜率**。
    *   **客观指标**：在QA任务上使用**精确匹配**和**F1分数**。

### 4. 资源与算力

*   **LLM使用**：论文明确指出使用了 **DeepSeek-V3** 作为大语言模型进行信息抽取、实体摘要和答案生成，使用 **GLM-4-Plus** 作为嵌入模型进行向量搜索和语义聚类。
*   **算力细节**：**文中未提及**具体的GPU型号、数量或训练时长。论文主要报告的是API调用的令牌成本、调用次数和端到端的时间成本。

### 5. 实验数量与充分性

*   **实验数量充足**：实验覆盖了**4个不同领域的数据集**，并在一组**5个强大的基线方法**上进行了广泛的对比，同时还进行了**两个关键的内部消融实验**（验证层次化索引和桥接知识的有效性）。
*   **评估客观公正**：
    *   采用LLM评判时，不仅使用了主要评估模型GPT-4o，还交叉验证了**Qwen-turbo和Claude-3.5-sonnet**作为评委，结论保持一致，消除了单一评估模型的偏差。
    *   除了LLM评判的胜率，还使用字符匹配层面的EM和F1分数进行了客观评估，验证了HiRAG在答案正确性上的提升。
    *   通过计算和比较图谱的聚类系数，从结构上定量证明了层次化索引增强了实体的语义聚合。
*   **分析深入**：对层次化索引的层数`k`的确定、令牌/时间/API调用成本效率、桥梁知识的覆盖率都进行了定量分析和讨论。

### 6. 论文的主要结论与发现

*   **HiRAG全面优于基线**：HiRAG在所有四个数据集和多数评估维度上，以显著优势击败了所有基线RAG方法。
*   **层次化索引是关键**：消融实验证明，使用层次化知识图谱（HiIndex）比扁平知识图谱能显著提升答案质量，因为它强化了语义相似实体间的连接。
*   **桥接知识至关重要**：消融实验证明，通过最短路径构建的桥接知识（HiRetrieval的一部分）能有效弥合局部与全局知识间的鸿沟，对生成连贯、准确的答案不可或缺。
*   **良好的效率权衡**：虽然HiRAG的离线索引阶段消耗了更多令牌和时间成本（如Mix数据集约7.55美元），但其在线检索阶段无需额外令牌成本，且在时间与API调用上更为高效，适合线上部署。

### 7. 优点

*   **问题定义清晰，动机充分**：精准地指出并形式化了现有图RAG方法中“语义疏远”和“知识鸿沟”两个核心痛点。
*   **方法设计优雅且有据可依**：HiIndex通过无监督的GMM聚类和LLM摘要自动化构建层次结构，HiRetrieval通过“最短路径”创建桥接知识的想法直观且有效，两者均紧密围绕所定义的挑战。
*   **实验设计扎实**：
    *   多领域数据集、多强基线的对比，以及多维度的评估指标，使得结论非常可靠。
    *   消融实验设计和跨模型评委的交叉验证增强了内部效度和结果的鲁棒性。
    *   对层数选择、成本效率等工程实践细节进行了分析，提高了方法的实用性。

### 8. 不足与局限

*   **索引成本较高**：构建高质量的层次化知识图谱需要大量LLM调用，导致索引阶段的令牌消耗和时间开销较大。
*   **检索排序机制有待完善**：HiRetrieval 模块在关系排序上较为简单，更复杂的查询感知排序机制可能会进一步提升检索质量。
*   **社区检测方法的可替换性讨论不足**：层次化图谱构建后直接应用Leiden算法，未讨论更复杂的层次社区发现方法是否可能带来增益。
*   **评估的局限性**：虽然评估设计已很严谨，但胜率指标受LLM评判主观性影响，且用于评估的GPT-4o可能与系统本身使用的LLM（DeepSeek-V3）存在亲缘偏差风险，尽管进行了交叉验证。

（完）
