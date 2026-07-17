---
title: Improving Retrieval-Augmented Generation through Multi-Agent Reinforcement Learning
title_zh: 通过多智能体强化学习改进检索增强生成
authors: "Yiqun Chen, Lingyong Yan, Weiwei Sun, Xinyu Ma, Yi Zhang, Shuaiqiang Wang, Dawei Yin, Yiming Yang, Jiaxin Mao"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=9Ia0KiVAut"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 采用多智能体RL联合优化RAG各组件（查询改写、检索、过滤、生成），作为协作智能体
tldr: 标准RAG流水线中各组件通常独立有监督训练，导致局部最优与整体目标不一致。本文提出多智能体强化学习框架，将查询改写、文档检索、过滤及答案生成分别建模为协作智能体，通过全局奖励信号联合优化所有组件。这种端到端的学习方式有效解决了组件间目标错位问题。在开放域问答上的实验表明，联合优化后的RAG系统在答案准确性和事实一致性方面均显著优于独立训练的方法。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: RAG组件独立优化导致组件目标与最终答案准确率不一致。
method: 将RAG各组件建模为多智能体，利用强化学习进行端到端联合优化。
result: 联合优化的RAG流水线在问答任务上取得更好的一致性和准确率。
conclusion: 多智能体RL能有效协调RAG各组件，提升整体生成质量。
---

## Abstract
Retrieval-augmented generation (RAG) is widely utilized to incorporate external knowledge into large language models, thereby enhancing factuality and reducing hallucinations in question-answering (QA) tasks. A standard RAG pipeline consists of several components, such as query rewriting, document retrieval, document filtering, and answer generation. However, these components are typically optimized separately through supervised fine-tuning, which can lead to misalignments between the objectives of individual components and the overarching aim of generating accurate answers. Although recent efforts have explored using reinforcement learning (RL) to optimize specific RAG components, these approaches often focus on simple pipelines with only two components or do not adequately address the complex interdependencies and collaborative interactions among the modules. To overcome these limitations, we propose treating the complex RAG pipeline with multiple components as a multi-agent cooperative task, in which each component can be regarded as an RL agent. Specifically, we present MMOA-RAG\footnote{The code of MMOA-RAG is on \url{https://github.com/chenyiqun/MMOA-RAG}.}, \textbf{M}ulti-\textbf{M}odule joint \textbf{O}ptimization \textbf{A}lgorithm for \textbf{RAG}, which employs multi-agent reinforcement learning to harmonize all agents' goals toward a unified reward, such as the F1 score of the final answer. Experiments conducted on various QA benchmarks demonstrate that MMOA-RAG effectively boost the overall performance of the pipeline and outperforms existing baselines. Furthermore, comprehensive ablation studies validate the contributions of individual components and demonstrate MMOA-RAG can be adapted to different RAG pipelines and benchmarks.

---

## 论文详细总结（自动生成）

# 论文总结：通过多智能体强化学习改进检索增强生成

## 1. 核心问题与整体含义
- **问题背景**：检索增强生成（RAG）在问答任务中广泛用于注入外部知识、提升事实性并减少幻觉。标准 RAG 流水线通常包含查询改写、文档检索、文档过滤和答案生成等多个组件。
- **核心痛点**：这些组件普遍采用独立的有监督微调，导致各自优化的局部目标与最终生成准确答案的整体目标之间出现错位。
- **已有局限**：现有使用强化学习（RL）的工作多聚焦于只含两个组件的简单流水线，未能充分处理多模块间的复杂依赖与协同。
- **本文动机**：将多组件 RAG 流水线建模为多智能体协作任务，通过多智能体强化学习联合优化所有模块，使全局奖励（如最终答案的 F1 分数）统一协调各智能体的目标。

## 2. 方法论
- **核心框架**：MMOA‑RAG（Multi‑Module joint Optimization Algorithm for RAG）。
- **关键思想**：把 RAG 流程中的每个组件（查询改写、检索、过滤、生成）分别看作一个强化学习智能体，所有智能体围绕统一的奖励信号进行端到端的联合优化。
- **技术细节**：
  - 采用多智能体强化学习框架，协调多个模块的交互。
  - 奖励函数直接与最终输出质量挂钩（如答案的 F1 分数），从而迫使每个模块的行为服务于整体性能。
  - 通过联合训练，自动学习各模块间的协同策略，替代原本独立、局部最优的微调范式。
- **算法流程**（基于摘要推断）：
  1. 初始化各模块的策略网络；
  2. 在每一轮对话或问答中，依次执行查询改写→检索→过滤→生成，收集所有中间动作；
  3. 计算最终答案相对于真实答案的统一奖励；
  4. 利用多智能体强化学习算法（如某种策略梯度方法）更新所有模块的参数，使奖励最大化。
- 具体公式和伪代码未在摘要中展开，需参阅原文。

## 3. 实验设计
- **数据集/场景**：在多个问答基准上进行实验（摘要未列出具体名称，推测为开放域问答常用数据集）。
- **对比方法**：与现有基线进行比较（摘要未指明具体基线方法，可能包括独立监督训练的 RAG 流水线以及已有 RL‑优化特定模块的工作）。
- **评估指标**：以最终答案的准确率、一致性等为主要指标，统一奖励即为 F1 分数。
- **消融实验**：验证各组件（查询改写、检索、过滤、生成）对整体性能的贡献，并展示了 MMOA‑RAG 可适配不同 RAG 流水线和基准。

## 4. 资源与算力
- 提供的摘要中未提及 GPU 型号、数量、训练时长等算力资源信息。原文可能包含相关说明，需在完整论文中查找。

## 5. 实验数量与充分性
- 摘要显示实验覆盖**多个 QA 基准**，包含与现有基线的对比以及**消融研究**，且证明了方法的可迁移性。这暗示实验组数较为丰富。
- 但具体数据集数量、每个数据集的实验设置、重复次数等未在摘要中给出。从方法论角度看，多基准验证和消融分析能够提供一定的客观性和公平性，但缺乏细节难以评估是否会引入选择性偏差或超参数过度拟合。

## 6. 主要结论与发现
- MMOA‑RAG 通过多智能体强化学习全局优化整个 RAG 流水线，**有效提升了最终答案的准确性和一致性**，性能优于独立训练的基线方法。
- 联合优化比孤立训练更能让各个模块的行为协调一致，从而解决目标错位问题。
- 消融实验证实每个组件都对整体增益有贡献；方法在不同 RAG 流水线和基准上表现出良好的适应能力。

## 7. 优点
- **视角新颖**：首次将完整 RAG 流水线形式化为多智能体协作问题，并引入多智能体 RL 解决端到端目标对齐。
- **系统性联合优化**：不再局限于单个或两个模块的优化，而是覆盖查询改写、检索、过滤、生成全链条，更贴近实际应用。
- **实验设计较全面**：多基准验证、消融研究以及跨流水线迁移实验，体现了方法的鲁棒性和通用性。
- **代码开源**：有利于复现和后续研究。

## 8. 不足与局限
- **细节缺失**：摘要未说明实验所用具体数据集、基线方法、模型规模以及算力消耗，难以评估方法在资源受限场景下的可行性和实际增益幅度。
- **潜在开销**：多智能体 RL 训练通常需要大量环境交互，可能带来较高的训练成本和在线推理延迟，这一点摘要未提及。
- **泛化边界模糊**：实验虽然在“多种”基准上进行，但未指明领域覆盖范围（如仅限英文开放域问答），无法判断其是否适用于对话、多轮交互或特定领域任务。
- **比较公平性存疑**：未说明与哪些 RL 优化方案对比，以及是否对超参数进行了公平调优，摘要无法提供足够的证据排除偏向性。
- **可复现性风险**：缺少算法超参数、网络结构等关键信息，仅凭摘要难以独立复现结果。

（完）
