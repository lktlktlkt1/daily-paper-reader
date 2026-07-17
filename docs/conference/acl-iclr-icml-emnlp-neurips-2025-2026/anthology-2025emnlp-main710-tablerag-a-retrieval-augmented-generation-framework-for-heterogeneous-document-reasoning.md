---
title: "TableRAG: A Retrieval Augmented Generation Framework for Heterogeneous Document Reasoning"
title_zh: "TableRAG: 面向异构文档推理的检索增强生成框架"
authors: "Xiaohan Yu, Pu Jian, Chong Chen"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.710.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 用于表格推理的迭代SQL基RAG框架
tldr: 本文针对RAG在异构文档中因扁平化表格导致信息丢失、削弱推理能力的问题，提出TableRAG框架。该框架基于SQL，通过上下文相关查询分解、文本检索和SQL生成四个步骤迭代处理表格和文本，实现复杂多跳查询。实验结果显示，TableRAG在多个表格问答基准上显著优于传统分块方法，证明了结构化推理对异构数据处理的重要性。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 794, \"height\": 635, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1657, \"height\": 1183, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 752, \"height\": 255, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 782, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 777, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 789, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 474, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 802, \"height\": 160, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 789, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 471, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.710/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 784, \"height\": 290, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.710/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1640, \"height\": 979, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.710/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1528, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.710/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1651, \"height\": 1364, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.710/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1662, \"height\": 157, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.710/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1438, \"height\": 524, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.710/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 655, \"height\": 317, \"label\": \"Table\"}]"
motivation: 异构文档中扁平化表格导致信息损失，限制RAG的复杂推理能力。
method: 基于SQL的迭代框架，通过查询分解、文本检索和SQL生成处理表格。
result: 在表格问答基准上优于传统分块方法，提升了多跳查询性能。
conclusion: 结构化SQL推理是处理异构文档和复杂表格查询的有效途径。
---

## Abstract
Retrieval-Augmented Generation (RAG) has demonstrated considerable effectiveness in open-domain question answering. However, when applied to heterogeneous documents, comprising both textual and tabular components, existing RAG approaches exhibit critical limitations. The prevailing practice of flattening tables and chunking strategies disrupts the intrinsic tabular structure, leads to information loss, and undermines the reasoning capabilities of LLMs in multi-hop, global queries. To address these challenges, we propose TableRAG, an SQL-based framework that unifies textual understanding and complex manipulations over tabular data. TableRAG iteratively operates in four steps: context-sensitive query decomposition, text retrieval, SQL programming and execution, and compositional intermediate answer generation. We also develop HeteQA, a novel benchmark designed to evaluate the multi-hop heterogeneous reasoning capabilities. Experimental results demonstrate that TableRAG consistently outperforms existing baselines on both public datasets and our HeteQA, establishing a new state-of-the-art for heterogeneous document question answering.

---

## 论文详细总结（自动生成）

好的，以下是基于您提供的论文内容，生成的结构化中文总结。

### 1. 论文的核心问题与整体含义

*   **核心问题**：现有的检索增强生成（RAG）系统在处理同时包含**非结构化文本**和**结构化表格**的异构文档时存在关键缺陷。其核心痛点在于，将表格“扁平化”为纯文本并进行分块的标准做法，会破坏表格固有的行列结构，导致信息丢失，并严重削弱大语言模型进行多跳、全局性推理的能力。
*   **研究动机**：如图1所示，当回答一个需要计算全局比例的问题时，传统RAG只能基于检索到的部分表格片段给出错误答案。因此，需要一种能够**保留表格结构完整性**、**支持跨模态全局推理**的新框架。
*   **整体含义**：论文旨在解决异构文档问答中由数据预处理引入的信息损失和推理能力受限问题，核心思想是**将表格视为不可分割的逻辑单元，并通过结构化查询语言（SQL）进行精确的符号化操作**，从而统一文本理解与表格数据分析。这项工作不仅提出了一个具体的框架（TableRAG），还构建了一个专门用于评估多跳异构推理能力的新基准（HeteQA）。

### 2. 论文提出的方法论

论文提出了名为 **TableRAG** 的框架，其核心思想是将SQL作为处理表格数据的统一接口，避免表格结构的破坏。

*   **核心思想**：通过将表格相关查询视为不可分割的推理单元，利用SQL进行**精确的符号执行**，以此来替代有损的表格扁平化和文本分块策略。
*   **总体架构**：TableRAG 包含**离线数据库构建**和**在线迭代推理**两个阶段。
    *   **离线阶段**：
        1.  **文本/表格解析**：从异构文档中提取纯文本 `T` 和一系列表格 `D`。
        2.  **双知识库构建**：
            *   **文本知识库**：将纯文本和表格的Markdown渲染文本分块、向量化索引，用于语义检索。
            *   **表格模式数据库**：提取每个表格的模式（Schema，即表名、列名、数据类型和示例），并在表格分块与其源表格模式之间建立映射函数 `f`。同时，将原始表格数据导入关系型数据库（如MySQL），为后续的SQL执行做准备。
*   **在线阶段（四步迭代推理流程）**：
    1.  **上下文感知的查询分解**：首先检索最相关的表格内容，通过映射函数 `f` 获取其模式，然后基于该模式，将复杂的原始查询分解为当前步骤需要解决的子查询 `qt`。
    2.  **文本检索**：对子查询 `qt` 进行向量召回和语义重排序，从文本知识库中获取最相关的Top-K个文本块。
    3.  **SQL编程与执行**：检查检索到的文本块中是否包含表格来源的内容。若是，则提取其模式 `St` 并生成对应的SQL语句，在数据库上执行并获得结果 `et`。此步骤是**选择性触发**的。
    4.  **组合中间答案生成**：将SQL执行结果 `et` 和文本检索结果进行交叉验证。如果两者一致，则直接作为子答案；如果SQL出错，则信任文本结果；如果两者冲突，则由LLM进行综合评估。迭代执行以上步骤，直至查询完全解决，生成最终答案 `A`。

### 3. 实验设计

*   **使用的数据集/场景**：
    *   **HybridQA**: 一个公开的多跳问答数据集，涉及表格和文本信息。实验仅保留了表格超过100个单元格的案例。
    *   **WikiTableQuestion (WikiTQ)**: 一个公开的表格问答数据集，涉及比较、聚合等操作。
    *   **HeteQA**: 本文提出的新基准，包含304个样本，跨越9个领域，由5种基本表格操作（过滤、分组、聚合、计算、排序）组合而成，专门用于评估多跳异构推理能力。
*   **对比的方法**：
    *   **Direct**：直接使用大语言模型生成答案。
    *   **NaiveRAG**: 将表格转为Markdown后进行标准RAG流程。
    *   **ReAct**: 一种基于提示语的智能体推理框架。
    *   **TableGPT2**: 使用基于Python代码执行的方法。
*   **评估指标**：
    *   **LLM-as-Judge准确率**：使用 Qwen-2.5-72B 模型对生成答案与标准答案的一致性进行0/1评分。
    *   **精确匹配**：答案与标准答案的完全匹配率。

### 4. 资源与算力

*   文中**未明确说明**实验所使用的具体GPU型号、数量或训练时长。框架本身是基于提示语的在线推理流程，不涉及模型微调，其主要资源消耗在于调用后端大语言模型的API或推理服务。
*   论文明确指出使用了多款闭源和开源的大语言模型作为后端，包括 `Claude-3.5-Sonnet`、`DeepSeek-V3`、`DeepSeek-R1` 和 `Qwen-2.5-72B`。
*   **结论**：论文没有提供训练/推理算力相关的详细信息。这是一个可以在总结中指出的点。

### 5. 实验数量与充分性

*   **实验数量**：论文进行了多组实验，评估较为全面。
    *   **主实验**：在3个数据集上，使用4种不同的后端大语言模型，对5种方法（包括TableRAG本体）进行了性能对比。
    *   **消融实验**：在2个数据集（HybridQA、HeteQA）上，对TableRAG的**4个核心模块**（上下文感知分解、SQL执行、文本检索）进行了消融研究。
    *   **效率分析**：对比了TableRAG和ReAct的**迭代步数分布**与**推理延迟**。
    *   **错误分析**：深入分析了TableRAG与基线方法的错误类型（推理错误、拒答/超步数）。
    *   **领域性能分析**：比较了不同方法在不同语义领域的表现。
    *   **超参数分析**：分析了Top-k检索参数对性能的影响。
*   **充分性与公平性**：实验设计**充分且公平**。对比了当前主流的多种方法（RAG、Agent、代码生成），使用了多种不同规模、不同架构的后端模型验证了框架的通用性，并通过消融实验证实了各个组件的有效性。实验结果使用两种评估指标报告，增强了可信度。

### 6. 论文的主要结论与发现

*   **TableRAG 性能最优**：TableRAG 在所有基准测试（HybridQA， WikiTQ， HeteQA）和所有后端大语言模型上，一致性地显著优于所有基线方法，在异构问答领域建立了新的最高水平。在HeteQA上，相较于最强的基线方法，性能提升超过10%。
*   **SQL执行是关键**：消融实验证明，保留表格结构并通过SQL进行符号化推理是性能提升的关键因素，尤其在需要复杂全局操作的HeteQA数据集上。去除SQL模块会导致性能明显下降。
*   **效率与准确性的平衡**：与ReAct相比，TableRAG不仅能实现更高的准确率，而且所需迭代步数更少、总推理延迟更低，证明了其“上下文感知分解”和SQL执行策略的高效性。
*   **架构通用性**：TableRAG框架的优越性能在使用不同后端大语言模型时均得到验证，显示出良好的架构通用性，不依赖于特定模型的能力。

### 7. 优点

*   **方法创新**：
    *   **结构化推理统一框架**：巧妙地将SQL引擎集成到RAG流程中，解决了表格扁平化导致的结构信息损失问题，这是一个直接且有效的创新。
    *   **上下文感知的分解**：查询分解并非盲目切分，而是基于检索到的表模式动态进行，使得分解出的子查询更易被SQL模块解决。
*   **资源贡献**：
    *   构建并开源了**HeteQA基准**，为评估复杂异构推理能力提供了更具挑战性的测试平台。
*   **实验严谨**：
    *   **多维度评估**：涵盖了准确率、效率、错误类型、参数敏感性等多个维度。
    *   **基线全面且强大**：对比了NaiveRAG、ReAct和TableGPT2等多种不同范式的强基线。
    *   **后端模型无关性验证**：通过在多种大语言模型上的测试，证明了框架的有效性并非偶然，增强了结论的鲁棒性。

### 8. 不足与局限

*   **对后端大语言模型的强依赖**：论文明确指出，框架的有效性依赖于底层LLM的强大能力（如Claude， DeepSeek-V3等）。如果使用较小的、未经专门指令微调的模型，性能可能会显著下降，这可能限制了在资源受限场景下的应用。
*   **基准的语言和领域限制**：HeteQA基准目前仅限于英语，其构建材料来自英文维基百科，这限制了其在多语言环境下泛化能力的验证。
*   **工程复杂性**：与简单的RAG或直接生成相比，TableRAG引入了离线数据库构建和模式映射等额外步骤，增加了系统的工程实现复杂度。
*   **错误传播风险**：尽管有交叉验证机制，但这是一个松耦合的迭代系统。任何一步（如查询分解、SQL生成、文本检索）的错误都可能导致最终答案的偏差。文中误差分析指出了SQL执行错误是推理失败的一大原因。
*   **成本问题**：频繁调用LLM进行查询分解、SQL生成和答案整合，其API调用成本可能高于单次生成方法。

（完）
