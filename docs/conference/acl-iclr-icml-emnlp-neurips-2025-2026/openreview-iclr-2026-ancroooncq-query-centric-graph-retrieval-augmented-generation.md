---
title: Query-Centric Graph Retrieval Augmented Generation
title_zh: 以查询为中心的图检索增强生成
authors: "Yaxiong Wu, Jianyuan Bo, Yongyue Zhang, Sheng Liang, Yong Liu"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=anCrOOoncq"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 通过以查询为中心的图进行多跳块检索，支持复杂问答的多步检索
tldr: 为解决图RAG中实体级与文档级粒度困境，提出以查询为中心的图RAG框架QCG-RAG。利用Doc2Query技术构建可控粒度的查询中心图，通过生成查询实现多跳块检索。在多个多跳问答数据集上验证了其在长上下文理解和推理上的高效性与可解释性，优于现有文档级和实体级方法。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 图RAG面临细粒度实体图高token成本和粗粒度文档图关系模糊的粒度两难问题。
method: 通过Doc2Query生成查询构建可控粒度的查询中心图，并设计多跳检索机制选取相关文本块。
result: 在多跳问答任务上达到了性能与可解释性的最优平衡，且降低了token开销。
conclusion: QCG-RAG为图增强RAG提供了一种灵活且高效的范式，适合复杂推理场景的实际应用。
---

## Abstract
Graph-based retrieval-augmented generation (RAG) enriches large language models (LLMs) with external knowledge for long-context understanding and multi-hop reasoning, but existing methods face a granularity dilemma: fine-grained entity-level graphs incur high token costs and lose context, while coarse document-level graphs fail to capture nuanced relations. We introduce QCG-RAG, a query-centric graph RAG framework that enables query-granular indexing and multi-hop chunk retrieval. Our query-centric approach leverages Doc2Query and Doc2Query{-}{-} to construct query-centric graphs with controllable granularity, improving graph quality and interpretability. A tailored multi-hop retrieval mechanism then selects relevant chunks via the generated queries. Experiments on LiHuaWorld and MultiHop-RAG show that QCG-RAG consistently outperforms prior chunk-based and graph-based RAG methods in question answering accuracy, establishing a new paradigm for multi-hop reasoning.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：基于图的检索增强生成（Graph-based RAG）在增强大语言模型（LLM）的长上下文理解和多跳推理时，面临“粒度困境”——细粒度实体级图虽能捕获细致关系，但会引入极高 token 开销并丢失上下文；粗粒度文档级图虽开销低，却无法捕获细粒度、多跳的语义关联。现有方法难以在成本与效果间取得平衡。
- **整体含义**：提出以查询为中心（query-centric）的图 RAG 框架，通过生成查询来构建可控粒度的图索引并进行多跳块检索，试图打破上述粒度困境，为复杂问答场景提供更高效、可解释的范式。

### 2. 论文提出的方法论
- **核心思想**：从“文档”或“实体”为中心转向以“查询”为中心，利用 Doc2Query 及其变体自动生成大量可能查询，用这些查询构造图节点，从而获得一种可控粒度的图结构（查询粒度），并基于该图进行多跳文本块检索。
- **关键技术细节**：
  - **查询中心图构建**：应用 Doc2Query（及 Doc2Query--）为每个文档或文本块生成潜在查询，查询作为图的节点；根据查询-文档、查询-查询的共现或语义相似性建立边，形成可控粒度的查询中心图。相比直接使用原始文本或实体，该图在保留多跳关系信号的同时，大幅压缩了拓扑规模。
  - **多跳块检索机制**：在查询中心图上执行专门设计的多跳检索策略，沿边游走并聚合相关查询，最终将关联的原文本块作为上下文提供给 LLM。该机制利用生成查询的桥梁作用，实现跨文档、跨段落的关联发现。
- **算法流程概览**（文字说明）：
  1. 对文档集运行 Doc2Query（或强化版本）生成候选查询集合。
  2. 构造查询中心图：将查询作为节点，基于共现等关系构建边。
  3. 输入用户问题后，在查询中心图进行多跳遍历，筛选出与问题相关的多跳查询路径。
  4. 根据筛选出的查询，回溯到其所关联的原始文本块，拼装成检索增强上下文。
  5. 将上下文与问题一起输入 LLM 生成最终回答。

### 3. 实验设计
- **数据集/场景**：
  - LiHuaWorld（可能为多跳、长上下文问答数据集）
  - MultiHop-RAG（专门用于评估多跳检索增强生成的数据集）
- **基准对比方法**：文中提到对比了先前的 chunk-based（基于文本块）和 graph-based（基于图）的 RAG 方法（具体方法名未在元数据中列出，但涵盖了文档级和实体级代表方法）。
- **任务类型**：多跳问答，重点考察准确率、可解释性及 token 开销。

### 4. 资源与算力
- 提供的文本（元数据）中**未提及** GPU 型号、数量、训练时长或推理硬件等算力细节，因此无法从现有信息中总结这部分内容。

### 5. 实验数量与充分性
- **实验组数**：至少包括两个数据集（LiHuaWorld 和 MultiHop-RAG）上的主实验，以及可能存在的消融实验（如探究查询中心图构建的不同策略、多跳检索深度的影响），但详细分组数量未在摘要中透露。
- **充分性与客观性**：在多个多跳问答基准上与基于块和基于图的方法进行全面对比，显示出性能优越性；同时关注 token 开销和可解释性，考虑了实际部署成本。从摘要判断，实验设计覆盖了主挑战（粒度困境）的多个维度，具备一定公平性，但缺少更具体的数据支撑无法评估全面性。

### 6. 论文的主要结论与发现
- QCG-RAG 在多跳问答任务上一致优于先前的基于块和基于图的 RAG 方法，取得了性能与可解释性的最优平衡。
- 查询中心图能以更低 token 成本实现与细粒度图相近甚至更优的检索质量，有效缓解粒度困境。
- 这种以查询为中心的图构建与多跳检索机制，为复杂推理场景的 RAG 提供了灵活且高效的新范式。

### 7. 优点（方法或实验设计的亮点）
- **创新粒度概念**：提出查询粒度的图索引，跳出实体/文档的两极框架，实现成本与效果的自由控制。
- **图质量与可解释性**：查询作为节点天然具有语义可读性，增强了图的可解释性，便于调试和分析。
- **多跳检索专门设计**：针对多跳问答定制的图游走和块回溯机制，更贴合任务需求。
- **实验对比全面**：与主流块级、图级方法对比，覆盖关键评估指标（准确率、token 成本），验证贴近实际应用。

### 8. 不足与局限
- **细节透明性有限**：目前仅基于元数据，无法判断 Doc2Query 的具体实现、图构建的边定义、多跳遍历深度限制等关键技术细节，以及实验中是否包含统计显著性检验。
- **数据集范围**：仅在 LiHuaWorld 和 MultiHop-RAG 两个数据集上报告结果，未展示其他领域（如对话、事实验证）或更大规模基准的泛化能力。
- **成本与实时性**：虽宣称 token 开销低，但查询生成及图构建的离线成本、增量更新能力未说明，可能影响动态知识库场景下的适用性。
- **对比方法覆盖**：未说明是否对比了最新的混合粒度或自适应图方法，可能遗漏部分强基线。
- **偏差风险**：若 Doc2Query 生成查询的质量依赖训练数据的分布，可能在特定领域产生系统性偏差，元数据未提及相关分析。

（完）
