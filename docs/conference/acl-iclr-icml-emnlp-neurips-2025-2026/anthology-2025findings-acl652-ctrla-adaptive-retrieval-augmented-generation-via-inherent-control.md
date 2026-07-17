---
title: "CtrlA: Adaptive Retrieval-Augmented Generation via Inherent Control"
title_zh: CtrlA：通过内在控制的自适应检索增强生成
authors: "Liu Huanshuo, Hao Zhang, Zhijiang Guo, Jing Wang, Kuicai Dong, Xiangyang Li, Yi Quan Lee, Cong Zhang, Yong Liu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.652.pdf"
tags: ["query:agentic-rag"]
score: 7.0
evidence: 利用LLM内在的诚实与信心表示自适应控制检索时机，提升RAG效率
tldr: 传统自适应RAG主要依赖统计不确定性检测，忽略了模型内部状态所蕴含的丰富信号。CtrlA首创从表示控制视角解决自适应检索问题，通过提取大语言模型隐藏层中表征诚实与信心方向的神经特征，构建内在信号控制器。该控制器可实时判断模型是否需要外部知识支撑，并自动触发检索。实验结果表明，CtrlA在多个基准上有效减少了冗余检索次数，同时保持了与全检索相当甚至更优的答案质量，为轻量级自适应RAG提供了新方向。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1570, \"height\": 755, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 505, \"height\": 322, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1029, \"height\": 326, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 780, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 791, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 831, \"height\": 283, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1440, \"height\": 1057, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1628, \"height\": 1532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1645, \"height\": 874, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1663, \"height\": 485, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 547, \"height\": 546, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 739, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 488, \"height\": 402, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 704, \"height\": 546, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 865, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 483, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1437, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 764, \"height\": 740, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 728, \"height\": 745, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1476, \"height\": 1394, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 496, \"height\": 236, \"label\": \"Table\"}]"
motivation: 现有自适应RAG方法主要依赖统计不确定性，未利用模型内部表示。
method: 提取LLM诚实和信心方向的表示特征，用于自适应控制检索决策。
result: 在多个数据集上实现了高效检索，减少冗余同时保障回答准确。
conclusion: 利用内部表示控制检索时机是提升RAG效率的有效途径。
---

## Abstract
Retrieval-augmented generation (RAG) has emerged as a promising solution for mitigating hallucinations of large language models (LLMs) with retrieved external knowledge. Adaptive RAG enhances this approach by enabling dynamic retrieval during generation, activating retrieval only when the query exceeds LLM’s internal knowledge. Existing methods primarily focus on detecting LLM’s confidence via statistical uncertainty. Instead, we present the first attempts to solve adaptive RAG from a representation perspective and develop an inherent control-based framework, termed CtrlA. Specifically, we extract the features that represent the honesty and confidence directions of LLM and adopt them to control LLM behavior and guide retrieval timing decisions. We also design a simple yet effective query formulation strategy to support adaptive retrieval. Experiments show that CtrlA is superior to existing adaptive RAG methods on a diverse set of tasks. Honesty steering can effectively make LLMs more honest and confidence monitoring is a promising indicator of retrieval trigger.

---

## 论文详细总结（自动生成）

好的，以下是对该论文的结构化深入总结。

### 1. 论文的核心问题与整体含义

-   **研究背景与动机**：
    -   检索增强生成（RAG）通过引入外部知识来缓解大语言模型（LLM）的幻觉问题。然而，传统方法通常采用无差别的单轮检索，导致对外部知识的过度依赖或检索不完整。
    -   自适应RAG（Adaptive RAG）应运而生，其核心思想是**仅在LLM内部知识不足时才动态触发检索**，旨在平衡内部知识与外部知识的使用。
-   **核心问题与现有方法局限**：
    -   自适应RAG的关键挑战在于决定**“何时检索”（when to retrieve）**。
    -   现有方法主要依赖**统计上的不确定性**（如输出概率、熵）作为LLM自信程度的代理指标来触发检索。
    -   论文指出这种假设存在两个根本性缺陷：
        1.  **诚实性假设**：认为LLM的输出总是与其内部知识一致（即LLM是诚实的）。但实际上，LLM常在诚实与有用性之间权衡，可能生成看似合理但与自身知识不符的内容。
        2.  **不确定性等价假设**：将不确定性等同于缺乏自信。例如，模型频繁回答“我不知道”时，统计学上不确定性很低，但此时恰恰应该触发检索。
    -   因此，现有方法难以精确判断真实的检索时机。
-   **整体含义**：
    -   本文**首次从表示（representation）的视角来解决自适应RAG问题**，提出了一个基于内在控制的框架 **CtrlA**，通过直接操控LLM内部表征空间中代表“诚实”和“信心”的方向，来更精准地决定检索时机。

### 2. 论文提出的方法论

-   **核心思想**：
    基于线性表示和叠加假设，CtrlA 提取LLM表征空间中对应“诚实方向”和“信心方向”的特征向量，并分别用于**引导模型行为（诚实引导）** 和**监控模型状态（信心监测）**，以实现更精准的检索时机决策。
-   **关键技术细节与流程**：
    框架分为两大步骤：特征提取与推理应用。
    1.  **表征特征提取**：
        -   手工构建对比指令，例如：“假装你是一个 **诚实/不诚实**的人”和“假装你是一个 **自信/不自信**的人”。
        -   将对比指令与一个语句数据集 `S` 中的句子拼接，输入LLM，收集各层（共`L`层）的Token表征 `r`。
        -   计算正负指令下表征的差异向量 `v = r^+ - r^-`。对所有语句在各层上的差异向量应用主成分分析（PCA），取第一主成分作为该层的**诚实特征方向** `v_h`。信心特征方向 `v_c` 的提取方法相同。
    2.  **推理过程中的应用（CtrlA Inference）**：
        -   **诚实引导**：在逐层、逐Token生成时，将当前表征 `R_k` 向诚实方向 `v_h` 加性调整，即 `R_k + λ * v_h`。参数 `λ` 控制引导强度，旨在让LLM更诚实地承认自己的知识边界，抑制捏造信息。
        -   **信心监测**：计算当前Token表征 `R_k` 与信心方向 `v_c` 在各层上的点积，经过层间平均池化和归一化缩放后，与阈值 `τ` 比较，得到信心分数 `m̄_k`。
        -   **检索触发机制**：如果模型生成的新信息Token（排除已有内容和停用词）中，有任何Token的信心分数 `m̄_k < 0`（不自信），则立即触发检索。同时，为了应对因诚实引导而产生的“拒绝回答”式输出，额外引入了一个**拒绝处理模块**，通过模式匹配识别此类输出并触发检索或调整查询策略。
        -   **检索查询构建**：检索被触发后，设计了两种查询构建策略：
            -   **上下文增强查询**：将原始问题与当前已生成、但经过“不自信Token”掩码处理的输出片段拼接，作为查询。
            -   **目标验证查询**：通过提示LLM，基于原始问题和当前输出片段，生成一个用于验证输出正确性的搜索查询。

### 3. 实验设计

-   **数据集与场景**：
    -   **短文本问答**：PopQA（长尾实体）、TriviaQA。
    -   **长文本问答**：ASQA（歧义问题）、Biography（传记生成，Bio）。
    -   **多跳问答**：2WikiMultihopQA、HotpotQA。
    -   **时效性问答**：FreshQA。
-   **Benchmark 与评估指标**：
    -   短文本问答：准确率。
    -   ASQA：str-em、Rouge-L、MAUVE、EM、F1。
    -   Bio：FactScore。
    -   多跳问答：EM、F1。
    -   FreshQA：宽松准确率和严格准确率。
-   **对比方法**：
    -   无检索。
    -   单轮RAG。
    -   基于规则的多轮RAG（固定句子数、固定Token数、查询分解）。
    -   基于不确定性的自适应RAG（FLARE、Self-RAG、DRAGIN、SeaKR等）。
-   **公平性保障**：
    -   所有方法（包括复现的基线）均采用相同的主干模型、检索器、文档语料库和推理配置，确保对比的公平性。

### 4. 资源与算力

-   **硬件配置**：论文明确指出，所有实验均使用 **2 张拥有 32GB 显存的 NVIDIA Tesla V100 GPUs** 进行推理。
-   **训练时长**：该方法无需对LLM进行微调，因此**没有训练时间成本**。特征提取步骤（如PCA）的计算成本相对较低，文中未明确给出具体耗时。
-   **软件环境**：使用了 PyTorch-2.1.0、Transformers-4.36.2 等开源库。

### 5. 实验数量与充分性

-   **实验充分性**：
    -   实验覆盖广泛，在**4大类任务（7个数据集）** 上进行了主实验验证，并包含了对多个基线的全面比较，充分证明了方法的有效性。
    -   进行了深入的**分析性实验**，以验证核心组件的有效性：
        -   **特征有效性**：在TruthfulQA上评估诚实引导，在自制可答/不可答问题上评估信心监测。
        -   **超参数影响**：研究了诚实引导强度 `λ`、信心监测阈值 `τ` 以及引导的层范围（`LB`, `LE`, `Nstep`）对性能的影响。
        -   **数据影响**：分析了特征提取所用数据的分布和规模对最终效果的影响。
    -   进行了详细的**消融实验**，对比了不同查询构建策略、不同检索器（BM25 vs. BGE）、是否使用拒绝处理模块等对结果的影响。
    -   检验了**模型迁移性**，将CtrlA应用于不同主干模型（LLaMA2-Chat, Vicuna），证明其鲁棒性。
-   **客观性与公平性**：
    -   实验公平性高。论文对大量基线方法进行了统一环境下的复现，并与原论文报告的结果进行了区分和对比，增强了结论的可信度。

### 6. 论文的主要结论与发现

-   **整体优越性**：CtrlA 在所有测试任务和评估指标上，一致地超越了包括基于规则、基于不确定性以及需要微调的各种自适应RAG方法。
-   **有效性验证**：
    -   **诚实引导有效**：通过调整内部表征，能有效提升LLM的诚实度，使其在缺乏知识时更倾向于承认而非生成错误信息，这直接提升了RAG性能。
    -   **信心监测是可靠的触发器**：通过监测表征空间中的信心方向，能够更精确地判断模型何时缺乏知识，从而在合适的时机触发检索，优化了内外部知识使用的平衡。
-   **高效检索**：在多跳问答任务中，CtrlA不仅性能最佳，而且触发的检索次数也相对较低，表明其避免了无效检索，效率更高。
-   **鲁棒性**：该方法对不同的特征提取数据分布和大小不敏感，且可成功迁移到不同的LLM骨干网络上。

### 7. 优点

-   **视角创新**：首次从**表征控制角度**解决自适应RAG问题，开辟了新思路，绕过了传统不确定性方法的内在缺陷。
-   **方法轻量**：是一种**即插即用（Plug-and-Play）** 的框架，无需对LLM进行微调，计算开销小，易于部署和与其他方法结合。
-   **双重机制互补**：“诚实引导”与“信心监测”两个机制协同工作，一个从源头减少不实信息生成，一个从检测端精准识别知识缺口，设计巧妙。
-   **实验扎实全面**：对比基线丰富，分析维度多样（超参、层位、数据影响），且在不同模型上验证了迁移性，论证非常充分。

### 8. 不足与局限

-   **特征提取依赖对比指令**：方法和特征的提取依赖于手工设计的对比提示（Prompt 3.1），其泛化性和最优设计可能因模型而异。
-   **外部知识处理未深化**：正如作者在局限性部分所述，CtrlA主要解决“何时检索”的问题，对检索后的内容**没有进行显式的相关性和有用性验证**。这可能引入无关或矛盾信息，影响最终答案质量。
-   **超参数敏感性**：诚实引导系数 `λ` 和信心监测阈值 `τ` 对性能有显著影响，针对不同任务和模型可能需要调整，增加了实际应用的调参成本。
-   **应用场景限制**：实验主要集中于知识密集型问答，其在更开放、对话式或有更多主观判断的任务中的表现有待检验。

（完）
