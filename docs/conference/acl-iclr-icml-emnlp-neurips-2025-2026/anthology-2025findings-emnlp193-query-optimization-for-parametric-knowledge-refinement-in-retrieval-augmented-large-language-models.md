---
title: Query Optimization for Parametric Knowledge Refinement in Retrieval-Augmented Large Language Models
title_zh: 基于参数知识精炼的检索增强大语言模型查询优化
authors: "Youan Cong, Pritom Saha Akash, Cheng Wang, Kevin Chen-Chuan Chang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.193.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: ERRR通过提取LLM参数知识精炼查询以确保检索相关信息
tldr: 为解决RAG系统中查询与LLM知识需求之间的信息鸿沟，提出提取-精炼-检索-阅读（ERRR）框架。首先提取LLM的参数知识，再由专用查询优化器精炼查询，确保只检索最相关信息以生成准确回答。该方法支持可训练管线和降低计算成本，为RAG的查询优化提供了新思路，实验表明能有效提升检索精准度和生成质量。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.193/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1502, \"height\": 1142, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.193/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 843, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.193/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1236, \"height\": 531, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.193/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1194, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.193/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1116, \"height\": 219, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.193/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1666, \"height\": 1080, \"label\": \"Table\"}]"
motivation: RAG系统存在预检索信息鸿沟，传统查询优化未充分利用LLM自身知识。
method: 提出ERRR框架，先提取LLM参数知识，再用查询优化器精炼查询以检索精准信息。
result: 实验表明该方法显著提升了检索相关性，降低了噪声，并改善了生成准确性。
conclusion: ERRR通过知识驱动查询优化，有效提升了RAG系统的整体性能。
---

## Abstract
We introduce the Extract-Refine-Retrieve-Read (ERRR) framework, a novel approach designed to bridge the pre-retrieval information gap in Retrieval-Augmented Generation (RAG) systems through query optimization tailored to meet the specific knowledge requirements of Large Language Models (LLMs). Unlike conventional query optimization techniques used in RAG, the ERRR framework begins by extracting parametric knowledge from LLMs, followed by using a specialized query optimizer for refining these queries. This process ensures the retrieval of only the most pertinent information essential for generating accurate responses. Moreover, to enhance flexibility and reduce computational costs, we propose a trainable scheme for our pipeline that utilizes a smaller, tunable model as the query optimizer, which is refined through knowledge distillation from a larger teacher model. Our evaluations on various question-answering (QA) datasets and with different retrieval systems show that ERRR consistently outperforms existing baselines, proving to be a versatile and cost-effective module for improving the utility and accuracy of RAG systems.

---

## 论文详细总结（自动生成）

好的，以下是对该论文的结构化总结。

### 1. 论文的核心问题与整体含义

*   **核心问题：** 论文聚焦于检索增强生成（RAG）系统中的“预检索信息鸿沟”（Pre-Retrieval Gap）。该鸿沟指的是，根据用户原始查询检索到的信息，与大型语言模型（LLM）生成最佳回答所需的特定知识之间存在不匹配。
*   **研究动机：** 现有的查询优化方法（如RRR框架）主要通过重写或泛化查询来扩大检索范围，但忽略了LLM自身的知识需求。这导致检索到的文档可能包含与查询相关但对于LLM是冗余的、或者缺失LLM真正需要验证和补充的信息，限制了回答的准确性。
*   **整体含义：** 论文旨在通过精准定位LLM的知识缺口来优化查询，使检索过程从“寻找与查询相关的信息”转变为“寻找LLM生成准确答案所需的信息”，从而更有效地利用外部知识库。

### 2. 论文提出的方法论

论文提出了**提取-精炼-检索-阅读（Extract-Refine-Retrieve-Read, ERRR）**框架，通过利用LLM的参数知识来指导查询优化。

*   **核心思想：** ERRR的核心是先“探查”LLM“已知”什么，再根据其“未知”或“不确定”的部分去优化查询，确保检索回的外部知识能精确地验证、补充或修正LLM的内部知识，从而弥合预检索信息鸿沟。
*   **关键技术细节与流程：**
    1.  **参数知识提取：** 直接提示LLM，令其为给定问题`q`生成一个伪上下文文档`C = E(q|θ)`。该文档被视为LLM参数知识`θ`的具象化表示，尽管可能包含不准确信息。
    2.  **查询优化：** 使用一个专门的查询优化器（也是一个LLM），基于提取出的参数知识`C`和原始问题`q`，生成一组优化后的查询`f'(C, q)`。这些查询旨在从外部知识库中获取能够验证、质疑或补充参数知识`C`的信息，特别是时间敏感的信息。
    3.  **检索与生成：** 使用优化后的查询`f'(C, q)`在外部知识库（如搜索引擎、维基百科）中进行检索，得到更相关的文档集`R(f'(C, q))`。最后，将原始问题`q`和检索到的文档一同交给LLM阅读器生成最终答案。
*   **可训练方案：** 为降低成本和增加灵活性，论文提出用一个小型可调模型（如T5-Large）作为查询优化器，通过知识蒸馏从大型教师模型（如GPT-3.5-Turbo）学习查询优化的能力。

### 3. 实验设计

*   **数据集与场景：** 实验在三个开放域问答数据集上进行，覆盖了不同难度的场景：
    *   **AmbigQA:** 测试处理模糊问题的能力。
    *   **PopQA:** 测试关于小众/长尾知识的问题。
    *   **HotpotQA:** 测试需要多跳推理的复杂问题。
*   **基准方法与对比对象：**
    *   **Direct:** 直接使用LLM（GPT-3.5-Turbo）回答。
    *   **RAG:** 经典的检索增强生成。
    *   **ReAct:** 交织推理与行动的迭代式RAG框架。
    *   **Frozen/Trainable RRR:** 重写-检索-阅读框架，是最直接的对比基准。
    *   **Frozen/Trainable ERRR:** 论文提出的框架。
*   **检索系统：** 为验证适应性，实验使用了两种检索后端：
    *   **Web搜索:** Brave Search API。
    *   **本地稠密检索:** 基于WikiDPR的稠密段落检索。

### 4. 资源与算力

论文**未明确说明**所使用的具体GPU型号、数量或总训练时长。
*   文中提到的模型包括：GPT-3.5-Turbo（作为主要的LLM和知识蒸馏的教师模型）、T5-Large（770M参数，作为可训练的查询优化器）。
*   对于**Trainable RRR**，提到使用2e-5的学习率，训练3个epoch，batch size为8。
*   对于**Trainable ERRR**，提到对每个数据集训练3个epoch，学习率为1e-4，batch size为4。

### 5. 实验数量与充分性

*   **实验组数：** 论文进行了较全面的实验。在3个数据集（AmbigQA, PopQA, HotpotQA）× 2种检索系统（Web搜索，本地检索）的设置下，对比了7种方法（Direct, RAG, ReAct, Frozen RRR, Trainable RRR, Frozen ERRR, Trainable ERRR）。
*   **实验充分性与公平性：**
    *   **充分性:** 实验覆盖了不同的任务难度和知识流行度，并在不同类型检索系统上验证了方法的鲁棒性。同时还分析了成本和延迟。这是一个比较全面的评估。
    *   **客观与公平性:** 对比方法包括当前主流和直接相关的基准。所有方法的LLM骨干模型（GPT-3.5-Turbo）保持一致，提示词、检索文档数量等细节均有说明，确保了对比的公平性。
    *   **不足:** 实验缺少全面的消融研究，例如，未探究单独移除“参数知识提取”步骤，直接让LLM优化查询的效果；也未分析不同提取/优化提示词的影响。由于资源限制，部分基线（如ReAct）未在所有数据集上完成评估。

### 6. 论文的主要结论与发现

*   **性能优越性：** ERRR框架在所有数据集和检索系统中，一致地优于直接生成、经典RAG和RRR等基线方法，证明了通过参数知识指导查询优化的有效性。
*   **可训练方案的优势：** Trainable ERRR使用更小的模型，性能甚至超越了其教师模型Frozen ERRR（基于GPT-3.5-Turbo），同时成本更低。
*   **鲁棒性强：** ERRR在检索质量较差的本地密集检索场景下表现尤为突出，其精准的优化查询能减少无关信息的检索，从而减轻噪声对LLM生成过程的干扰。
*   **成本效益高：** 相比ReAct等迭代式框架，作为单轮交互的ERRR在保持高性能的同时，显著降低了成本和延迟。

### 7. 优点

*   **创新的问题视角：** 将查询优化的目标从“匹配查询”转向“匹配LLM的知识需求”，这是一个新颖且深刻的洞察。
*   **简洁有效的框架设计：** 四步流水线（提取-精炼-检索-阅读）清晰直观，易于实现，并可作为一个模块集成到更复杂的系统中。
*   **实用性导向：** 提出的可训练方案兼顾了成本和灵活性，为在资源受限或对数据隐私有要求的场景下部署提供了可行路径。
*   **详实的评估：** 在多个维度的数据集和检索系统上进行了评估，充分证明了方法的有效性和适应性。

### 8. 不足与局限

*   **模型依赖性：** 框架的性能严重依赖底层LLM的能力。如果LLM提取的参数知识质量很差（例如，对于极其冷门的知识完全“幻觉”），那么优化后的查询可能也会偏离方向。
*   **缺乏关键消融实验：** 未展示“参数知识提取”这一核心步骤的必要性。例如，是否可以将“请根据你的知识盲区优化查询”这样的指令直接纳入优化器提示中，而不显式生成伪文档。
*   **单轮交互的限制：** 论文将ERRR限定在单轮场景，虽然成本低，但相比ReAct等能够进行多步推理和验证的系统，可能无法处理极端复杂的、需要多步交互查询的任务。
*   **训练方案细节缺失：** 对Trainable ERRR的描述相对简略，如知识蒸馏数据的构建规模、质量，以及为何没有引入强化学习等细节未充分展开。

（完）
