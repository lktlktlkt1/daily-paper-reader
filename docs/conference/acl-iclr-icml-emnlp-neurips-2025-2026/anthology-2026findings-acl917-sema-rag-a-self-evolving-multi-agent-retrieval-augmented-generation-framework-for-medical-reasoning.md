---
title: "SEMA-RAG: A Self-Evolving Multi-Agent Retrieval-Augmented Generation Framework for Medical Reasoning"
title_zh: SEMA-RAG：面向医疗推理的自进化多智能体检索增强生成框架
authors: "Yongfeng Huang, Ruiying Chen, James Cheng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.917.pdf"
tags: ["query:agentic-rag"]
score: 10.0
evidence: 自进化多智能体RAG框架，匹配多阶段临床推理，支持迭代检索与反馈
tldr: 医学问答中，传统单轮静态检索范式与多阶段临床推理严重脱节。SEMA-RAG提出自进化多智能体框架，将解释、探索与裁决任务分配给不同智能体协同完成，并引入迭代检索与充分性反馈机制。多个智能体通过角色分工与通信构建可靠证据链，克服了单一推理链过载的问题。实验证明，该框架在复杂医学推理任务上显著超越现有方法，为垂直领域智能RAG系统提供了新范式。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.917/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 672, \"height\": 633, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.917/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1631, \"height\": 917, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.917/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 682, \"height\": 533, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.917/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1567, \"height\": 1112, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.917/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1660, \"height\": 1237, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.917/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 813, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.917/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.917/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 661, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.917/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.917/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 801, \"height\": 832, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.917/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 605, \"height\": 255, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.917/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 495, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.917/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 678, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.917/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 675, \"height\": 179, \"label\": \"Table\"}]"
motivation: 单轮静态检索与多阶段临床推理脱节，导致查询翻译缺乏语义深度和检索无迭代反馈。
method: 构建自进化多智能体RAG框架，分解异质任务至多个智能体协同完成推理与检索。
result: 在医学问答上形成可靠证据链，性能超越现有方法。
conclusion: 多智能体RAG能有效模拟多阶段临床推理过程。
---

## Abstract
Retrieval-Augmented Generation (RAG) is widely employed to mitigate risks such as hallucinations and knowledge obsolescence in medical question answering, yet its predominantly single-round, static retrieval paradigm misaligns with the multi-stage process of clinical reasoning. This compressed workflow induces two structural deficiencies: question-to-query translation often lacks clinically grounded semantic interpretation, and retrieval lacks iterative sufficiency feedback, making it difficult to form reliable evidence chains. We argue that both issues stem from a deeper cause—overloading a single reasoning chain with heterogeneous tasks of interpretation, exploration, and adjudication—and that the remedy is to reconstruct the workflow via task decoupling and dynamic multi-round exploration. To this end, we propose the Self-Evolving Multi-Agent framework **SEMA-RAG**, which assigns these roles to three specialist agents: **Interpreter Agent** for clinical schema interpretation, **Explorer Agent** for sufficiency-driven self-evolving retrieval, and **Arbiter Agent** for evidence adjudication and answer selection. Across five benchmarks and five LLM backbones, SEMA-RAG improves the strongest baseline by **+6.46** accuracy points on average, measured per backbone.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将基于您提供的论文内容，以中文、Markdown格式生成一份结构化、深入、客观的总结。

### 1. 论文的核心问题与整体含义

*   **核心问题**：当前的检索增强生成（RAG）技术在医疗问答中虽被广泛用于缓解幻觉和知识过时问题，但其主流的**单轮静态检索范式**与临床医生的**多阶段动态推理过程**严重脱节。
*   **具体表现**：这种脱节工作流导致两个结构性缺陷：
    1.  **查询翻译缺乏临床语义**：从问题到检索查询的转化缺乏临床依据，导致隐式约束难以明确表达。
    2.  **检索缺乏迭代充分性反馈**：检索过程无法评估已有证据是否足够，也无法在证据不足时进行自我调整和补充检索，导致难以形成可靠的证据链。
*   **根本原因与解决方向**：论文认为，问题的根源在于**将“解释、探索、裁决”这些异构任务过度加载在单一推理链上**。因此，根本的解决之道是**通过任务解耦和动态多轮探索来重构工作流**，使其更贴合分阶段的临床工作模式。

### 2. 论文提出的方法论

SEMA-RAG 是一个**自进化多智能体 RAG 框架**，它通过角色分工和协作，将复杂的临床推理任务分解给三个专门化的智能体。

*   **核心思想**：模拟临床医生的诊断流程，将单一轮次的 RAG 过程扩展为一个“解释-探索-裁决”的闭环协作系统。
*   **关键技术细节与算法流程**：
    *   **1. 解释器智能体 **：
        *   **功能**：负责将非结构化的医学问题 $Q$ 映射为一个结构化的**临床纲要元组 $Q'$**。
        *   **组成**：包括 `临床意图`, `医学实体`, `临床约束`, 以及一个摘要性的 `初始检索查询`。
        *   **目标**：将隐式的临床意图和关键约束显式化，为后续检索和推理提供稳定的锚点。随后，该元组被线性化为一个可直接用于稠密检索的查询字符串 $\hat{q}_{init}$。
    *   **2. 探索者智能体 **：
        *   **功能**：执行**充分性驱动的自进化迭代检索**。
        *   **流程**：从解释器智能体生成的初始查询开始，进行多轮检索。在每一轮 $t$ 中：
            1.  根据本轮查询集 $Q_t$ 检索新文档，更新累积证据集 $C_t$。
            2.  评估当前证据集 $C_t$ 是否“**充分**” ($s_t \in \{0, 1\}$) 以回答问题。
            3.  若证据不充分 ($s_t=0$)，则识别具体的证据缺口 $g_t$，并生成最多 $m$ 个目标明确的**跟进查询** $Q_{t+1}$ 以填补缺口。
            4.  若证据充分 ($s_t=1$)，或达到最大迭代轮次 $T_{max}$，则终止循环，输出最终的封闭证据集 $C^*$ 和探索轨迹 $\tau$。
        *   **自进化特性**：系统在任务执行过程中，能根据每轮检索结果的评估，自适应地更新查询和检索轨迹，实现动态收敛。
    *   **3. 裁决者智能体 **：
        *   **功能**：对探索者智能体收集的最终证据集 $C^*$ 进行**综合裁决**。
        *   **流程**：
            1.  **证据裁决**：处理冗余和潜在冲突的证据，去粗取精，识别一致性与矛盾点，将支持性与反驳性线索整合成一份**可追溯的结构化证据报告 $R$**。
            2.  **证据锚定作答**：基于生成的证据报告 $R$，从候选答案集 $Y$ 中选择最终答案 $\tilde{y}$。

### 3. 实验设计

*   **数据集与场景**：在**五个医学问答基准数据集**上进行了评估，覆盖了从临床考试到生物医学文献推理的广泛场景：
    *   **临床考试类**：MMLU-Med, MedQA-US, MedMCQA
    *   **生物医学研究类**：PubMedQA*, BioASQ-Y/N
*   **基线方法**：对比了三种代表性的方法，以刻画从无检索到迭代检索的性能差异：
    *   **无检索**：CoT（思维链提示，仅依赖模型内部知识）。
    *   **单轮检索**：MedCPT（作为医学领域检索器）和 MedRAG（检索融合框架）。
    *   **迭代检索**：i-MedRAG（通过跟进问题驱动多轮检索）。
*   **基础模型**：为了评估框架的鲁棒性，在**五个主流、不同来源的大语言模型**上进行了测试：deepseek-v3.1, kimi-k2, qwen3-coder-plus, gemini-2.0-flash, glm-4.0-flash。

### 4. 资源与算力

*   **论文未明确提及**具体的硬件配置（如 GPU 型号、数量）或模型训练的算力开销。
*   **推断**：实验采用 **API 调用的推理模式**，所有大语言模型调用均由模型提供商服务。这意味着主要的算力成本在于本地构建和查询稠密向量检索索引，但论文未披露此部分的硬件细节。

### 5. 实验数量与充分性

*   **实验数量**：大概进行了 25 组以上的主要实验（5个基准 x 5个模型），并辅以消融实验、参数分析、案例分析、泛化实验和成本分析等，总计实验量可观。
*   **充分性与公平性**：
    *   **公平性**：所有方法均在**零样本设定**下评估，且除 SEMA-RAG 外，基线方法均遵循其官方设定，对比基础清晰。SEMA-RAG 本身未使用额外的训练或微调，确保了公平性。
    *   **充分性**：
        *   **多维度验证**：通过跨数据集、跨模型的实验，充分论证了方法的有效性和泛化能力。
        *   **消融实验**：通过逐一移除三个核心智能体，量化了每个模块的贡献。
        *   **参数分析**：分析了最大迭代轮次 $T_{max}$ 和查询广度 $m$ 的影响，为参数选择提供了依据。
        *   **转移性测试**：在更小的模型、不同的检索器、开放式生成及多轮对话场景下进行了额外测试，证明了方法的鲁棒性和可迁移性。

### 6. 论文的主要结论与发现

1.  **性能优越且稳健**：SEMA-RAG 在所有五个基准、五种大语言模型上均一致地优于最强基线方法，平均准确率提升了 **+6.46 个百分点**。
2.  **任务解耦是关键**：通过将“解释-探索-裁决”任务解耦并由专门智能体协作，有效解决了单一推理链的认知过载问题，是性能提升的根本原因。
3.  **自进化探索机制有效**：探索者智能体引入的充分性驱动的自进化检索循环，相比固定轮次的迭代检索，能更有效地完成证据，构建可靠的证据链。
4.  **过早决策代价高**：在那些因证据不完整而可能导致错误决策的难题上，SEMA-RAG 的增益尤为显著，证明了其避免过早下结论的价值。

### 7. 优点

*   **创新性的框架设计**：提出了“自进化多智能体 RAG”范式，通过任务解耦和角色专业化，系统性地重塑了 RAG 工作流以匹配复杂的临床推理过程，这是本文最核心的亮点。
*   **引入“自进化”机制**：探索者智能体的“证据充分性评估-针对性补全”循环，超越了一般的迭代 RAG，实现了更具目的性和动态收敛能力的证据探索。
*   **验证充分且多维**：实验设计非常扎实，不仅覆盖了多个基准和模型，还深入进行了消融、参数、案例和成本效率分析，并超出了离散选择的范畴，验证了在开放式问答和对话场景的泛化能力，结论极具说服力。
*   **良好的可解释性与可溯源性**：通过要求产出结构化纲要、明确证据缺口、建立可追溯的证据报告，整个推理过程的“黑箱”感降低，更符合医疗领域对安全性和可靠性的要求。

### 8. 不足与局限

*   **环境限制**：实验仍局限于**基准数据集**，未在真实的临床工作流（如纵向电子健康记录推理）中验证。
*   **检索依赖**：系统性能高度依赖于外部知识库的**质量和覆盖率**。若关键证据缺失或过时，自进化循环也可能收敛于不完整或不正确的证据上。
*   **终止标准不足**：当前的证据充分性判定，主要基于类级别的合理性，而非直接针对**选项层面的可分离性**，可能导致在初步锁定正确类别后过早停止，而无法精确区分剩余选项（如错误案例分析所示）。
*   **推理成本**：多智能体、多轮次的协作模式带来了更高的推理延迟和 token 消耗，虽然性价比优于固定步骤的迭代基线，但仍显著高于单轮方法。
*   **缺乏过滤与超参数敏感性**：在证据累积过程中缺乏显式的相关性过滤，且性能对停止标准、探索深度等超参数较为敏感。

（完）
