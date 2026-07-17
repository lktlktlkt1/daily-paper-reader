---
title: Query Routing over Multimodal Knowledge Bases for Retrieval-Augmented Reasoning
title_zh: 面向检索增强推理的多模态知识库查询路由
authors: "Chunyi Peng, Zhipeng Xu, Zhenghao Liu, Yishan Li, Yukun Yan, Shuo Wang, Zhiyuan Liu, Yu Gu, Minghe Yu, Ge Yu, Maosong Sun"
date: 2025-09-01
pdf: "https://openreview.net/pdf?id=yU1zAy8N75"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 根据推理状态动态决定何时何地检索，结合LLM规划和动态检索
tldr: 现有多模态检索增强生成方法通常采用静态检索流程，忽视了模型在推理过程中动态规划与决策的能力。R1-Router框架通过引入基于推理状态的路由机制，让多模态大语言模型能够主动决定何时以及从哪个知识库检索信息。该方法将检索行为与推理链深度耦合，大幅提升了复杂推理任务的准确性与效率。实验表明，R1-Router在多个多模态问答基准上显著优于传统固定流水线方法。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 静态检索流程未利用MLLM的推理和规划能力进行动态知识交互。
method: 提出R1-Router，学习基于推理状态动态路由查询到多模态知识库。
result: 在检索增强推理任务上取得显著性能改进。
conclusion: 动态查询路由能有效提升多模态RAG的推理能力。
---

## Abstract
Multimodal Retrieval-Augmented Generation (MRAG) has shown promise in mitigating hallucinations in Multimodal Large Language Models (MLLMs) by incorporating external knowledge during generation. Existing MRAG methods typically adopt a static retrieval pipeline that fetches relevant information from multiple Knowledge Bases (KBs), followed by a refinement step. However, these approaches overlook the reasoning and planning capabilities of MLLMs to dynamically determine how to interact with different KBs during the reasoning process.
To address this limitation, we propose R1-Router, a novel MRAG framework that learns to decide ***when*** and ***where*** to retrieve knowledge based on the evolving reasoning state. Specifically, R1-Router can generate follow-up queries according to the current reasoning step, routing these intermediate queries to the most suitable KB, and integrating external knowledge into a coherent reasoning trajectory to answer the original query. Furthermore, we introduce Step-wise Group Relative Policy Optimization (Step-GRPO), a tailored reinforcement learning algorithm that assigns step-specific rewards to optimize the reasoning behavior of MLLMs.
Experimental results on various open-domain QA benchmarks across multiple modalities demonstrate that R1-Router outperforms baseline models by over 7\%. Further analysis shows that R1-Router can adaptively and effectively leverage diverse KBs, reducing unnecessary retrievals and improving efficiency and accuracy.

---

## 论文详细总结（自动生成）

基于您提供的论文摘要和元数据，以下是对论文《Query Routing over Multimodal Knowledge Bases for Retrieval-Augmented Reasoning》的详细中文总结。

### 1. 论文的核心问题与整体含义
*   **研究动机**：现有多模态检索增强生成（MRAG）方法通常采用静态检索流水线：先固定地从多个知识库检索信息，再进行一次后期融合。这种模式忽略了多模态大语言模型（MLLM）内在的推理和规划能力。
*   **核心问题**：如何让 MLLM 在推理过程中**动态地、主动地**决定“何时检索”以及“从哪个知识库检索”，而不是被动接受预先拉取的外部信息。
*   **整体含义**：将检索行为与模型的逐步推理链深度耦合，从“先检索后推理”转变为“边推理边路由式检索”，以提升复杂多模态推理任务的准确性和知识利用效率。

### 2. 论文提出的方法论
*   **核心框架：R1-Router**
    *   **动态查询路由**：模型不再是单次检索，而是根据当前的**推理状态**生成后续查询，并将这些中间查询路由到最合适的一个或多个多模态知识库（KB）。
    *   **推理轨迹整合**：将从不同 KB 检索到的外部知识有机地嵌入到一个连贯的推理链中，最终生成原始问题的答案。
    *   **“何时”与“何地”的决策**：框架的核心是学习一种路由策略，该策略在推理的每一“步”判断是否需要检索；如果需要，再判断将查询发往哪个模态/哪个领域的 KB。
*   **关键算法：Step-wise Group Relative Policy Optimization (Step-GRPO)**
    *   这是一种专门定制的强化学习算法，用于优化 MLLM 的推理行为。
    *   **步骤级奖励**：与传统 RL 仅对整个生成序列给出最终奖励不同，Step-GRPO 为推理链中的每一个步骤分配特定的奖励信号，从而精细地引导模型学习何时检索、检索什么以及如何利用检索结果进行下一步推理。

### 3. 实验设计
*   **数据集/场景**：在多个跨模态的开放域问答基准测试集上进行了验证（具体数据集名称未在摘要中列出，但涵盖不同模态的组合）。
*   **基准对比方法**：对比了现有的 MRAG 方法，即采用静态检索流水线（先检索多知识库再统一融合优化）的基线模型。
*   **核心评估指标**：性能提升幅度（综合准确率等），摘要中指出 R1-Router 比基线模型性能提升超过 7%。

### 4. 资源与算力
*   **说明**：所提供的摘要和元数据中**未提及**任何关于算力资源的信息，包括 GPU 型号、数量、训练时长、模型参数规模等。因此，无法从现有材料中获知该部分的细节。

### 5. 实验数量与充分性
*   **实验规模**：摘要显示实验覆盖了多个跨模态的开放域 QA 基准，属于多数据集验证。此外，还包含进一步的分析实验，以证明模型能够自适应地利用多样化 KB 并减少不必要检索。
*   **充分性与客观性评估**：从摘要披露的信息看，实验设计具备基本充分性，包含多基准横向对比和深入的效率/行为分析。与静态流水线方法的对比也符合该问题的常规研究范式，具备公平性。但更多的细节（如消融实验、统计显著性检验等）需要查看全文才能准确判断。

### 6. 论文的主要结论与发现
*   R1-Router 在多个跨模态开放域问答任务上实现了显著的性能突破，准确率相较基线模型提升超过 7%。
*   通过动态路由决策，模型能够自适应地、高效地利用不同知识库中的信息。
*   该方法在提升推理准确率的同时，能够有效减少不必要或冗余的检索操作，改善了检索增强生成的效率。

### 7. 优点
*   **理念创新**：首次将基于推理状态的动态路由引入多模态 RAG，变被动为主动，更贴近人类的复杂推理习惯。
*   **精细优化**：提出的 Step-GRPO 算法实现了步骤级别的奖励，能够更精准地训练模型在长推理链中的检索和整合行为。
*   **效率与效果双赢**：在显著提升推理准确率的同时，降低了无效检索的次数，实用价值较高。

### 8. 不足与局限
*   **信息不全的限制**：由于仅基于摘要和元数据进行分析，论文在具体实现细节（如路由器的具体网络结构、多模态知识库的具体构成）、更广泛的基线对比（如是否与不检索的 MLLM 或其它 Agent 框架对比）、计算开销的量化等方面可能存在的不足无法被完整评估。
*   **潜在局限推测**：方法依赖于一个预定义的多模态知识库集合，对于开放世界中动态变化的知识源可能适应性有限。同时，步骤级的强化学习训练通常会带来更高的训练复杂度和不稳定性，这或许是一个应用限制，但需待全文验证。
*   **实验覆盖**：摘要未提及在封闭域、对话型或需要深层次多跳推理的任务上的表现，实验覆盖的全面性暂无法判断。

（完）
