---
title: Multi-agent System with Individual Optimized Expertise for Retrieval Augmented Generation
title_zh: 面向检索增强生成的个体优化多智能体系统
authors: "Yingtao Ren, Xiao Luo, Jinzhao Zhou, Yu-Cheng Chang, Chin-teng Lin"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=VVJeDnuo4c"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 通过个体优化赋予多智能体系统不同专长以改进RAG
tldr: 当前RAG方法因检索不充分和幻觉问题仍不理想。本文提出MAPS，通过三个具有专用技能的智能体协作完成RAG：查询扩展、检索和生成代理，并利用反馈奖励分别优化。实验表明，个体优化的多智能体系统在检索质量和生成准确性上优于单一模型，为多智能体RAG开辟了新方向。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 检索不充分与幻觉问题限制RAG性能。
method: 设计三个专用智能体进行查询扩展、检索和生成，并分别优化。
result: 多智能体协作提升了检索准确率与生成质量。
conclusion: 个体优化与多智能体协同是改进RAG的有效策略。
---

## Abstract
This paper studies the problem of retrieval-augmented generation (RAG), which leverages external knowledge to increase the performance of language models. Despite the remarkable progress, current RAG approaches are still far from satisfactory due to inadequate retrieval and potential hallucination. Towards this end, we propose a novel approach named Multi-agent System with Individual Optimized Expertise (MAPS) for RAG. The core idea of our MAPS is to equip three well-designed agents with different specializations using individual optimization corpus. In particular, we first expand ambiguous queries with a query extension agent, and quantify the reward based on the accuracy, which can be utilized to refine our agent for higher expansion efficiency. To enhance the retrieval quality, we include a unanimity voting method to annotate the current query as insufficient or sufficient, and their generative outcomes are utilized as ground truth to supervised fine-tune the judge agent. To further mitigate potential hallucination, an answer agent is optimized with dynamic matching-based rewards with curriculum learning for final outputs. Extensive experiments across multiple benchmark datasets validate the effectiveness of the proposed MAPS in comparison with state-of-the-art approaches.

---

## 论文详细总结（自动生成）

# 论文深度解析：面向检索增强生成的个体优化多智能体系统（MAPS）

## 1. 论文的核心问题与整体含义
- **研究动机**：检索增强生成（RAG）通过引入外部知识来提升语言模型性能，但现有方法存在两大瓶颈：
  - **检索不充分**：初始查询可能模糊或不够精确，导致检索到的文档相关性不足。
  - **幻觉风险**：生成模型可能产出与检索事实不一致的内容。
- **整体含义**：该工作主张通过**构建多智能体系统**来分解 RAG 流水线，并对每个智能体进行**个体化专门优化**，从而系统性地缓解上述问题，旨在获得更准确、更可靠的 RAG 效果。

## 2. 方法论：MAPS 核心思想与技术细节
- **核心思想**：设计三个分别承担查询扩展、检索质量裁决和最终答案生成的智能体，每个智能体通过独立的优化语料和奖励信号进行微调，协同完成 RAG 任务。
- **关键技术细节**：
  - **查询扩展代理（Query Extension Agent）**
    - 对模糊查询进行扩展，生成更精确的检索关键信息。
    - 优化方式：基于扩展后检索准确率计算奖励，利用该奖励对代理进行精炼，以提升扩展效率。
  - **裁决代理（Judge Agent）**
    - 使用**一致性投票法**（Unanimity Voting）对当前查询是否检索充分进行标注（充分 / 不充分）。
    - 将生成的裁决结果作为真实标签，对裁决代理进行有监督微调。
  - **答案代理（Answer Agent）**
    - 负责最终答案生成。
    - 采用**动态匹配奖励**与**课程学习**相结合的优化策略，以抑制幻觉。
- **算法流程**（文字说明）：
  1. 输入用户查询 → 查询扩展代理对查询进行改写或扩充。
  2. 利用扩展后的查询进行检索，获取外部文档。
  3. 裁决代理评估检索结果是否充分；若不充分，可能触发进一步的查询调整或反馈。
  4. 答案代理基于最终检索结果生成最终答案。
  5. 各代理根据各自的奖励信号或监督目标独立更新参数。

## 3. 实验设计
- **数据集 / 场景**：论文提到在**多个基准数据集**上进行验证，摘要未列出具名称，但从动机推断可能涉及开放域问答或事实验证类 RAG 评测任务。
- **对比方法**：与当前最先进的 RAG 方法（State-of-the-art approaches）进行全面比较，具体方法名称需参考正文。
- **评估指标**：可能包括检索质量指标（如召回率、精确率）和生成质量指标（如准确性、事实一致性、幻觉率）。

## 4. 资源与算力
- 论文摘要及元数据中**未明确说明**使用的 GPU 型号、数量或训练时长。
- 基于多智能体微调的常见需求，可推测实验需数块高性能 GPU（如 A100）完成监督微调或强化学习优化，但具体数字未知。

## 5. 实验数量与充分性
- **实验组数**：摘要指明“多基准数据集”上的大量实验，通常包含：
  - 主实验（与多个基线在多个数据集上的性能对比）；
  - 消融实验（移除某个代理或优化成分以验证其贡献）；
  - 组件分析（如不同奖励函数对代理的影响）。
- **充分性与公平性**：
  - 宣称使用多个基准、与最先进方法对比，实验设计较为全面。
  - 每个代理均独立优化，使用各自的优化信号，这在一定程度上保证了对比公平（避免共享偏见）。
  - 但因摘要未披露具体数据集和基线细节，无法最终判断所有维度的均衡性。

## 6. 主要结论与发现
- 个体优化的多智能体系统在检索质量和生成准确性上均**优于单一模型 RAG 方案**。
- 通过分工与专用化，MAPS 能够更有效地处理查询歧义、筛选高质量知识、并减少回答幻觉。
- 该工作为多智能体 RAG 提供了新范式，表明**分散式专业化协作**是提升 RAG 系统鲁棒性的可行方向。

## 7. 优点
- **架构创新**：首次将 RAG 流水线显式分解为三个可独立优化的专用智能体，思路清晰、模块性强。
- **个体优化机制**：针对不同子任务设计了针对性奖励（准确率驱动、一致性投票标注、动态匹配奖励等），避免了统一信号无法适配各阶段特点的问题。
- **幻觉缓解**：通过裁决代理把控检索质量，再结合课程学习的答案优化，形成了双重保障。
- **实验广度**：多数据集验证增强了结论的普适性。

## 8. 不足与局限
- **细节缺失**：目前仅依靠摘要，无法评估方法的具体实现复杂度、超参数敏感性以及代理间通信开销。
- **实验覆盖风险**：未在摘要中看到低资源场景、跨领域迁移或对检索器类型的鲁棒性分析，这些可能是潜在不足。
- **偏差风险**：使用一致性投票生成裁决代理的训练标签，若基础生成模型本身存在系统性偏差，该标签可能带有噪音。
- **应用限制**：多代理协作在推理时可能带来额外延迟和计算成本，实际部署的可行性需要进一步探讨。

（完）
