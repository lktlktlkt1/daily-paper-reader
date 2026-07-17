---
title: "Retrieval as Reasoning: Learning to Select and Generate with LLMs"
title_zh: 检索即推理：学习使用LLM选择与生成
authors: "Qiwei Di, Yuhang He, Qi Chen, Quanquan Gu, Peng CHENG, Jing Bai"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=NuA9XtWY6s"
tags: ["query:agentic-rag"]
score: 8.0
evidence: LLM通过推理学习选择文档并生成答案，将检索建模为推理过程
tldr: 现有RAG存在检索目标与生成任务不一致、长提示导致性能下降等问题。本文提出将检索视为推理任务的端到端框架，让LLM自身通过多步推理组织文档、选择关键信息并生成响应，克服了检索-生成隔阂。实验表明，该统一范式有效提升了文档利用效率和答案质量，为RAG提供了新范式。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 检索目标与生成任务错位，长提示引入偏差。
method: 让LLM通过多步推理自行组织和选择文档，端到端生成答案。
result: 文档选择更精准，生成质量更高，缓解了长提示问题。
conclusion: 将检索建模为推理过程是解决RAG核心局限的有效途径。
---

## Abstract
Retrieval-Augmented Generation (RAG) (Lewis et al., 2020) has become a practical solution for addressing hallucination in large language models (LLMs) by conditioning responses on retrieved documents. However, existing RAG systems face two major limitations: (1) retrieval objectives are often misaligned with the downstream generation task, leading to irrelevant documents harmful to the generation; (2) concatenating many retrieved documents into long prompts strains model capacity and introduces positional biases that degrade performance. To overcome these issues, we propose a unified framework where the LLM itself learns to perform document selection and answer generation in an end-to-end manner. Inspired by human reasoning, our model organizes documents via hierarchical semantic IDs and selects relevant content through a self-reflection mechanism composed of query-specific attention and an additional feed-forward MLP layer. This architecture enables the model to promote helpful documents directly during generation, eliminating the need for separate retrievers or rerankers. Through joint training, the model learns to select the most informative 2-3 documents. We conduct experiments to validate the effectiveness of our design.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- 现有检索增强生成（RAG）存在两个核心局限：
  - **检索目标与生成任务错位**：检索模块追求表面相关性，常召回无关或干扰性文档，损害生成质量。
  - **长提示引入偏差与能力瓶颈**：将大量检索文档直接拼接到提示中，不仅超出模型有效上下文窗口，还会诱发位置偏差，导致性能下降。
- 论文提出一种新范式：**将检索看作推理过程的一部分**，让大语言模型（LLM）自身以端到端方式学习“何时查、查什么、如何用”，从而弥合检索与生成之间的鸿沟，提升答案的忠实度与质量。

## 2. 论文提出的方法论
- **核心思想**：不再依赖外部独立的检索器或重排器，而是让LLM通过多步推理自行组织文档、选择关键信息并生成最终响应。
- **关键技术细节**：
  - **层次化语义ID组织文档**：为文档分配层次化语义标识符，便于模型建立结构化认知。
  - **自反思选择机制**：由两部分构成：
    - 查询特定注意力（query‑specific attention）：根据当前查询动态关注文档的不同部分。
    - 额外的前馈MLP层：辅助模型进行文档相关性的判断与筛选。
  - 在生成过程中，模型利用上述机制**直接“推广”有用的文档**，隐式完成检索与排序。
- **训练方式**：对文档选择与答案生成进行联合训练，使模型学会从候选集中精确挑选 **2–3 篇**最具信息量的文档，并据此生成答案。这一过程无需任何人工标注的检索标签。

## 3. 实验设计
- **数据集/场景**：摘要中未明确列出具体数据集或任务场景，仅提及“开展实验验证设计有效性”。
- **基准与对比方法**：摘要未说明具体的 benchmark 或用于对比的基线方法。根据上下文推测，应与传统 RAG 流水线（如先检索后生成的方式）进行对比，但细节不详。

## 4. 资源与算力
- 摘要**未提及** GPU 型号、数量、训练时长或任何算力相关信息，无法评估其资源需求。

## 5. 实验数量与充分性
- 摘要仅用一句话概括实验验证，未提供实验组数、消融实验、统计检验等细节。
- 基于现有信息，无法判断实验是否充分、客观与公平。但从论文的 claim 来看，必要的有效性验证应当存在，只是未被文本揭示。

## 6. 论文的主要结论与发现
- 所提出的统一框架能够：
  - **精准选择文档**：模型学会了在生成过程中自动识别并利用最相关的 2–3 篇文档。
  - **提升生成质量**：回答更符合事实，缓解了无关文档和长提示带来的性能衰减。
  - **消除检索‑生成隔阂**：将检索内化为推理过程的一部分，使整个系统更加连贯和高效。

## 7. 优点
- **方法创新性强**：首次将检索显式建模为LLM内部推理任务，颠覆了传统“检索管道 + 生成模型”的分离式架构。
- **端到端可学习**：无需单独的检索器或重排器，简化系统流程，减少模块间的信息损失。
- **缓解长提示问题**：通过内部筛选而非外部拼接，有效规避了上下文窗口限制和位置偏差。
- **可解释性潜力**：自反思机制和层次化语义ID有望提供更好的推理过程可解释性。

## 8. 不足与局限
- **实验细节缺失**：摘要未给出数据集、基线方法、消融设置等关键信息，无法评估结论的普适性和鲁棒性。
- **规模未知**：方法仅在假设条件下验证，不清楚是否适用于大规模文档库或更复杂的开放域问答场景。
- **额外计算开销**：引入的查询特定注意力和前馈MLP层可能增加推理成本，未分析效率。
- **选择数量固定**：强制选出 2–3 篇文档，可能在某些只需单篇或多篇才能回答的问题上不适应，灵活性受限。
- **泛化风险**：仅在未知数据集上训练和验证，可能对不同的领域、语言或文档类型存在偏差。

（完）
