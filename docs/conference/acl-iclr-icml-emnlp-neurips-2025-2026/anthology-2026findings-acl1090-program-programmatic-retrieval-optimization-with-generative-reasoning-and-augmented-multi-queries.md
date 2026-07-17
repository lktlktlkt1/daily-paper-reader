---
title: "PROGRAM: Programmatic Retrieval Optimization with Generative Reasoning and Augmented Multi-queries"
title_zh: "PROGRAM: 通过生成式推理和增强多查询的程序化检索优化"
authors: "Gun Il Kim, Jungkyu Shin, Jong Wook Kim, Beakcheol Jang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1090.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 程序化检索与迭代剪枝用于多跳推理
tldr: 本文针对RAG中非结构化语义匹配缺乏逻辑结构、无法系统引导多跳推理的问题，提出PROGRAM框架。该框架将检索视为逻辑、时序、因果等程序类型的执行过程，通过程序类型选择、迭代剪枝和证据积累实现程序化推理。实验结果表明，PROGRAM在五个基准上均优于现有方法，证明了结构化程序检索在复杂推理任务中的优越性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1090/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 757, \"height\": 702, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1090/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1598, \"height\": 1173, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1090/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 780, \"height\": 865, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1090/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 784, \"height\": 638, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1090/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 747, \"height\": 2317, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1655, \"height\": 515, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1652, \"height\": 511, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1652, \"height\": 514, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1652, \"height\": 515, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1646, \"height\": 531, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 798, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 490, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1444, \"height\": 370, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 725, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 793, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1645, \"height\": 531, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1641, \"height\": 528, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1090/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1644, \"height\": 529, \"label\": \"Table\"}]"
motivation: RAG非结构化语义匹配缺乏逻辑结构，无法系统引导多跳推理。
method: 将检索转化为程序执行，通过类型选择、迭代剪枝和证据积累优化检索。
result: 在五个基准上均优于现有方法，证明了结构化检索的优势。
conclusion: 程序化检索优化为RAG的复杂推理提供了系统化解决方案。
---

## Abstract
Current retrieval-augmented generation (RAG) methods struggle with complex multi-hop reasoning, relying on unstructured semantic matching that lacks the logical structure needed to systematically guide retrieval. We introduce Programmatic Retrieval Optimization with Generative Reasoning and Augmented Multi-queries (PROGRAM), a novel framework that elevates retrieval to structured, program-guided reasoning. PROGRAM treats retrieval as execution of specific program types, such as logical, temporal, causal, and so forth, through three stages of ’Program-Type Selection’ with dual-metric optimization, ’Iterative Active Program Pruning’ with evidence accumulation, and ’Final Answer Generation’ with reranking. Evaluated on five benchmarks including HotPotQA, 2WikiMultihopQA, ARC-Challenge, MMLU-Pro, and MedQA with various LLMs, PROGRAM achieves state-of-the-art performance with up to 24% relative improvement on HotPotQA and 13.2% on MedQA over strong baselines including FLARE, ProbTree and Self-RAG.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

*   **核心问题**：当前的检索增强生成方法在处理复杂的多跳推理任务时，主要依赖非结构化的语义匹配。这种方法缺乏系统引导检索所需的逻辑结构，无法有效区分不同类型的问题。
*   **研究动机**：现有工作如 FLARE 和 Self-RAG，虽然引入了迭代检索或自省令牌，但本质上仍将检索视为同质的相似性搜索。它们未能识别出因果比较、时间推理、极值查询等不同问题类型需要根本不同的检索策略，这成为提升检索增强推理系统性能的关键瓶颈。
*   **整体含义**：本文旨在弥合“非结构化语义匹配”与“复杂问题所需的结构化逻辑”之间的鸿沟，通过引入一种程序化、结构化的视角来重新定义和优化检索过程，以实现更精准、更系统的推理。

### 2. 论文提出的方法论

*   **核心思想**：提出 **PROGRAM** 框架，将检索过程从通用的相似性搜索提升为**结构化、程序引导的推理**。该框架将检索视为特定程序类型的执行，而非简单的文档匹配。

*   **关键技术细节与算法流程**：
    *   **第一阶段：程序类型选择与双指标优化**
        *   **程序类型库**：定义了包含“基础”和“高级”两类别的程序类型库，如简单事实、逻辑与/或、因果、时序、医疗诊断、多跳推理等。
        *   **查询生成与评分**：针对输入问题，由大语言模型选择相关的程序类型，并为每个程序生成多个候选子查询。
        *   **双指标优化**：通过结合**信息增益（基于KL散度衡量候选查询在证据上的增量信息）** 与**语义得分（衡量候选查询与原问题的语义对齐度）** 来筛选最佳子查询：`c* = argmax (S_IG(c) + S_sem(Q, c))`。这确保了子查询既有信息增量又不偏离用户意图。

    *   **第二阶段：迭代主动程序剪枝与证据积累**
        *   **支持度得分**：为每个已选定最佳子查询的程序，检索文档并计算支持度得分 `S_sup(p_i) = Sim(q_i, D_accum_i)`，衡量程序子查询与其检索文档集之间的语义相似度。
        *   **统计性剪枝**：采用 t 检验来分析所有程序支持度得分的分布，淘汰那些检索质量在统计上不显著低于群体均值的程序。幸存者被标记为“活跃程序”。
        *   **动态检索与锁定**：每个活跃程序会迭代评估其累积文档是否足够回答问题。若不足，则继续检索；若已充分，则将该程序“锁定”，不再进行新的检索，仅保留其证据。

    *   **第三阶段：最终答案生成与重排序**
        *   **证据聚合与重排序**：收集所有活跃和被锁定程序的检索文档，形成最终证据池，并利用重排序器根据其与原问题的相关性进行重排。
        *   **答案生成**：选取重排后的前k个最相关文档，结合少样本链式思维提示，输入到大语言模型中生成最终答案。

### 3. 实验设计

*   **数据集与场景**：在五个覆盖不同推理类型的基准数据集上进行评估：
    *   **多跳推理**：HotpotQA, 2WikiMultihopQA
    *   **常识推理**：ARC-Challenge
    *   **科学推理**：MMLU-Pro
    *   **生物医学推理**：MedQA
    *   实验按数据集划分，如对多跳数据集用验证集，对常识、科学、医学数据集用测试集，各取前500个问题测试。

*   **基准与对比方法**：与一系列强大的检索基线方法进行了比较，包括：
    *   **直接生成/标准链式思维**
    *   **迭代检索**：IRCoT
    *   **主动检索**：FLARE
    *   **树状推理**：ProbTree
    *   **自省检索**：Self-RAG
    *   **自适应检索**：SeaKR

*   **骨干模型与检索配置**：
    *   **大语言模型**：使用四种指令微调的LLM作为骨干网络，包括 GPT-4o-mini、Gemma-2-9B、Qwen-2.5-7B 和 Mistral-Small-24B。
    *   **检索与重排**：检索器使用 GTE 模型；重排序器探索了 Bi-Encoder、ColBERTv2 和 Cross-Encoder 三种类型。

### 4. 资源与算力

*   **文中明确提及**：论文**未明确说明**实验所消耗的具体算力资源，如 GPU 型号、数量或训练时长。
*   **推理**：文中主要体现了在推理阶段的计算开销分析（如表征延迟的 LAT 指标），表明增加程序类型数量会导致延迟线性增加。由于该方法不涉及对基础LLM或检索器的训练，其主要算力消耗可能在于大语言模型的API调用或本地推理。

### 5. 实验数量与充分性

*   **实验组数**：论文进行了非常全面和大量的实验，可以归纳为以下几类：
    1.  **主实验**：在5个数据集 × 4种LLM骨干网络上，与7种基线方法进行了全面的性能对比，至少有`5 × 4 = 20`组主结果（详见原文表格）。
    2.  **消融实验**：对框架的三个核心模块（程序类型选择、迭代剪枝、答案生成）进行了彻底的组合消融，涉及7种配置（单模块、两两组合、全组合），在5个数据集和至少1个骨干模型上完成。
    3.  **分析实验**：针对特定设计选择进行了深入的单项分析，包括：
        *   程序类型选择的影响（基础 vs. 基础+高级 vs. 全部类型）
        *   重排序器的架构对比（Bi-Encoder, ColBERT, Cross-Encoder）
        *   最终程序选择模式（多程序 vs. 单程序）
        *   评分方法解耦（仅信息增益、仅语义、两者结合）
        *   超参数敏感性分析（迭代次数、候选子查询数量）。
*   **充分性与客观公正性**：实验设计非常充分，通过多数据集、多模型、多维度分析，全面验证了方法的有效性和鲁棒性。对比基线均为当前最先进或具有代表性的方法，比较是公平的。消融实验系统性地证明了每个组件的必要性和协同效应。分析实验深入探讨了方法各环节的设计权衡，结论具说服力。

### 6. 论文的主要结论与发现

*   **PROGRAM 在所有基准上均达到最先进性能**，尤其在复杂的多跳推理任务上取得了显著提升。例如，在HotpotQA上，相比Self-RAG的最好结果，F1分数最高相对提升24%。
*   **结构化程序引导至关重要**：PROGRAM 通过明确的逻辑子查询，有效防止了推理漂移，其性能远优于依赖非结构化置信度令牌的方法（如Self-RAG）。
*   **强大的领域适应性**：在ARC-Challenge和MedQA等专业领域数据集上的卓越表现证明，“高级”程序类型能成功地将通用LLM能力与特定领域知识结合起来。
*   **高效激发小模型潜力**：PROGRAM 在较小的开源模型（如Gemma-2-9B）上取得了接近甚至超越大型模型的效果，证明其是一种高效的“推理放大器”，有助于解决“噪声中推理”的问题。
*   **框架各组件的协同依赖性**：消融实验证明，程序类型选择、迭代剪枝和重排序是紧密结合的三位一体系统，任何单一模块或两两组合都无法有效处理复杂推理，三者协同才能激发巨大的性能飞跃。

### 7. 优点

*   **创新性视角**：首次将“程序化推理”思想系统地应用于检索增强生成的全过程，将检索从无序匹配提升到有序执行，思路新颖。
*   **方法论严谨**：框架设计精巧，三个阶段环环相扣，并通过信息增益和统计 t 检验的引入，为查询优化和路径剪枝提供了量化、客观的度量。
*   **实验验证全面且扎实**：实验覆盖了多个领域、多种模型规模和大量强基线，并通过详尽的消融和分析实验，深刻揭示了方法各组成部分的作用与价值，结果极具说服力。
*   **强适应性**：该方法不依赖于特定模型或重排器，表现出良好的通用性和稳健性。

### 8. 不足与局限

*   **程序类型空间依赖人工定义**：目前的程序类型库是通过手动设计构建的，可能无法穷尽所有有效的推理路径，尤其在金融、视觉、表格问答等未探索领域，其泛化能力有待验证。
*   **计算效率与延迟**：文中提及增加程序类型会带来显著的延迟开销。在追求极致性能时，需要权衡准确率和效率，缺少对整体计算成本的系统性分析。
*   **组件协同但复杂**：虽然三位一体的协同是优点，但也意味着框架复杂度较高，部署和调优可能需要更多工程投入。
*   **评估覆盖面**：虽已覆盖五个典型数据集，但对论文自身提到的金融、表格问答等潜在应用领域缺乏实验验证，留下了一定的不确定性。

（完）
