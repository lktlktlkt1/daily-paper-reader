---
title: Mixture-of-Experts for Knowledge Graph Retrieval-Augmented Generation
title_zh: 知识图谱检索增强生成的专家混合方法
authors: "Haochen Liu, Guanghui Min, Song Wang, Yada Zhu, Chen Chen, Jundong Li"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=1KkIChhCv7"
tags: ["query:agentic-rag"]
score: 7.0
evidence: MoRA使用专家混合进行知识图谱检索，提升多跳推理
tldr: 知识图谱检索增强生成（KG-RAG）能补充语言模型的知识，但现有方法或依赖大型模型成本高，或轻量模型检索质量低。本文提出MoRA，利用专家混合架构让轻量语言模型高效引导知识图谱检索，优化多跳推理。实验表明，MoRA在保持低计算开销的同时显著提升多跳问答的准确性，为可扩展KG-RAG提供新方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: KG-RAG方法要么成本高要么检索质量低，多跳推理场景下尤甚。
method: 提出MoRA，用专家混合让轻量模型有效引导知识图谱检索过程。
result: 实验显示，MoRA在多跳问答上提高准确性，同时降低计算成本。
conclusion: 为知识图谱增强的推理任务提供高效且可扩展的检索方案。
---

## Abstract
Large Language Models (LLMs) have demonstrated strong capabilities in open-domain question answering, but often struggle with factual accuracy and multi-hop reasoning due to the incompleteness of the training corpora. A promising solution is Knowledge Graph Retrieval-Augmented Generation (KG-RAG), which supplements LLMs with structured knowledge retrieved from external knowledge graphs (KGs). However, existing KG-RAG methods either rely on large-scale language models (e.g., ChatGPT) to guide the retrieval process, which leads to high computational costs, or suffer from limited retrieval quality when using lightweight language models, particularly under multi-hop scenarios. We propose MoRA (Mixture-of-Experts for Retrieval-Augmented Generation over Knowledge Graphs), a novel KG-RAG framework that enhances hop-wise KG knowledge retrieval through a Mixture-of-Experts (MoE) framework. Each expert is guided by a combination of two types of soft prompts: expert-specific soft prompt encourages specialization in different reasoning perspectives across experts, and contextual soft prompt evolves with each reasoning hop by encoding the query and previously explored KG triplets, enabling the model to preserve consistency and relevance across multi-hop retrieval. This design allows MoRA to perform accurate and robust retrieval using lightweight language models. MoRA achieves superior performance across multiple KG-based Question Answering benchmarks compared to existing retrieval systems, including those that rely on much larger language models, demonstrating its effectiveness under limited computational budgets.

---

## 论文详细总结（自动生成）

# 论文总结：Mixture-of-Experts for Knowledge Graph Retrieval-Augmented Generation (MoRA)

## 1. 论文的核心问题与整体含义
- **研究背景**：大语言模型（LLMs）在开放域问答中表现强大，但受限于训练语料的不完整性，经常在事实准确性和多跳推理上出错。
- **核心问题**：知识图谱检索增强生成（KG‑RAG）可以弥补这一缺陷，但现有方法存在两难：
  - 要么依赖大规模语言模型（如ChatGPT）引导检索，计算成本极高；
  - 要么采用轻量语言模型，但检索质量明显下降，尤其在多跳推理场景中表现不佳。
- **整体目标**：设计一个能在**有限计算预算**下，利用轻量语言模型实现**高精度、鲁棒的多跳知识图谱检索**框架。

## 2. 论文提出的方法论
- **核心思想**：提出 **MoRA (Mixture‑of‑Experts for Retrieval‑Augmented Generation over Knowledge Graphs)**，通过**混合专家（MoE）架构**，让轻量语言模型高效引导逐跳的知识图谱检索。
- **关键技术细节**：
  - **逐跳检索（Hop‑wise Retrieval）**：将多跳推理拆分为多个推理步（hop），每一步从知识图谱中检索相关三元组。
  - **专家混合（MoE）**：每个推理跳由一个专家处理，不同专家专注于不同的推理视角。
  - **双软提示机制**：
    - **专家特定软提示（Expert‑specific soft prompt）**：固定每个专家，引导其在不同推理角度上形成专长。
    - **上下文软提示（Contextual soft prompt）**：随推理跳动态演化，编码当前查询和已探索的三元组历史，保证多跳过程中的**一致性与相关性**。
- **算法流程**（文字概括）：
  1. 将用户查询与历史三元组编码为上下文软提示。
  2. 对第 \(h\) 跳，选择对应专家，结合其专家特定软提示与上下文软提示。
  3. 专家模型根据组合提示在知识图谱中检索最相关的三元组。
  4. 新检索到的三元组加入历史，上下文软提示更新，进入下一跳。
  5. 最终将完整路径的三元组与原始查询一起馈送给下游LLM进行答案生成。

## 3. 实验设计
- **数据集/场景**：多个基于知识图谱的问答（KG‑QA）基准测试。摘要未列具体名称，但提到“multiple KG‑based Question Answering benchmarks”。
- **对比方法**：
  - 依赖大规模语言模型的检索系统（如使用ChatGPT等）。
  - 其他公开的检索增强生成方法，特别是同样使用轻量语言模型的系统。
- **评估指标**：通常在KG‑QA任务中采用准确率、F1等指标（摘要未详述，但符合常规评测）。

## 4. 资源与算力
- **论文提供的算力信息**：摘要和元数据中**未明确说明** GPU 型号、数量或训练时长。
- **推断**：由于强调“轻量语言模型”和“有限计算预算”，MoRA 的计算消耗应远低于基于大语言模型的检索方法，但具体硬件配置需查阅全文。

## 5. 实验数量与充分性
- **实验数量**：摘要仅提及“在多个 KG‑QA 基准上与现有检索系统进行对比”，具体实验组数未知。
- **充分性**：
  - 对比了不同规模的基线（包括大型模型和轻量基线），比较维度合理。
  - 摘要暗示 MoRA 在轻量模型条件下取得了最优结果，但未呈现消融实验或统计显著性检验细节。
  - 客观性：由于基于公开基准评估，公平性有保障；但全文尚未可知是否控制了模型参数量、训练数据等变量。

## 6. 论文的主要结论与发现
- MoRA 以轻量语言模型为基础，通过 MoE 和双软提示机制，在多跳知识图谱问答上**显著优于现有检索系统**。
- 即使在计算预算远小于大型语言模型基线的情况下，MoRA **仍能取得更高准确性和鲁棒性**。
- 该框架为**高效、可扩展的 KG‑RAG 系统**提供了一个可行方案，尤其适合资源受限的场景。

## 7. 优点
- **架构创新**：首次在 KG‑RAG 中引入 MoE 处理逐跳推理，用双软提示兼顾专家专长与上下文连贯性。
- **高效性**：摆脱对大型语言模型的依赖，大幅降低计算开销，同时保持甚至提升检索质量。
- **多跳适应**：专门针对多跳推理设计，解决了轻量模型在长链推理中易丢失信息的问题。
- **泛化潜力**：在多个 KG‑QA 基准上验证，展示跨数据集的稳定性。

## 8. 不足与局限
- **实现细节缺失**：摘要未提供具体专家数量、软提示长度、训练策略等关键参数，复现困难。
- **实验覆盖**：仅提及“multiple benchmarks”，未说明数据集规模、领域多样性，可能仅限于常识或事实型知识图谱。
- **对比局限**：虽声称超过大型模型，但缺少与最新强基线（如改进的 KG‑RAG 变体）的全面定量对比。
- **应用限制**：MoE 引入额外的路由和专家管理开销，对轻量化设计的具体收益‑开销比未明确量化。
- **偏差风险**：双软提示的训练依赖特定任务数据，迁移到新领域可能需要重新训练提示，泛化能力有待验证。

（完）
