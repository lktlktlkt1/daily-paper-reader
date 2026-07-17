---
title: "RAG over Tables: Hierarchical Memory Index, Multi-Stage Retrieval, and Benchmarking"
title_zh: 表格上的检索增强生成：分层记忆索引、多阶段检索与基准评测
authors: "Jiaru Zou, Dongqi Fu, Sirui Chen, Xinrui He, Zihao Li, Yada Zhu, Jiawei Han, Jingrui He"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=PifVwyqe5L"
tags: ["query:agentic-rag"]
score: 7.0
evidence: 面向表格的多阶段检索，用于复杂问答
tldr: 表格数据中的知识检索与推理是RAG的难点，问题常需跨越多个表格。本文针对表格RAG，提出分层记忆索引来刻画表内和表间知识关联，设计多阶段检索流程过滤冗余表格并精准定位相关信息。同时构建了相应评测基准。实验验证了该方法在表格复杂问答上的有效性，为结构化数据RAG奠定基础。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 表格问答需跨表检索，现有RAG方法难以有效处理表格知识关联。
method: 提出分层记忆索引与多阶段检索流程，优化表内与表间知识检索。
result: 在表格问答基准上，多阶段检索显著提升了答案准确度。
conclusion: 为结构化数据RAG提供了高效检索框架与评测基准。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances Large Language Models (LLMs) by integrating them with an external knowledge base to improve the answer relevance and accuracy. In real-world scenarios, beyond pure text, a substantial amount of knowledge is stored in tables, and user questions often require retrieving answers that are distributed across multiple tables. Retrieving knowledge from a table corpora (i.e., various individual tables) for a question remains nascent, at least, for (1) how to understand intra- and inter-table knowledge effectively, (2) how to filter unnecessary tables and how to retrieve the most relevant tables efficiently, (3) how to prompt LLMs to infer over the retrieval, (4) how to evaluate the corresponding performance in a realistic setting. Facing the above challenges, in this paper, we first propose a table-corpora-aware RAG framework, named T-RAG, which consists of the hierarchical memory index, multi-stage retrieval, and graph-aware prompting for effective and efficient table knowledge retrieval and inference. Further, we first develop a multi-table question answering benchmark named MultiTableQA, which spans 3 different task types, 57,193 tables, and 23,758 questions in total, and the sources are all from real-world scenarios. Based on MultiTableQA, we did the holistic comparison over table retrieval methods, RAG methods, and table-to-graph representation learning methods, where T-RAG shows the leading accuracy, recall, and running time performance. Also, under T-RAG, we evaluate the inference ability upgrade of different LLMs.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义
- **研究动机**：检索增强生成（RAG）依赖外部知识库提升大模型答案质量，但现实世界中大量知识储存在**表格**中，而非纯文本。用户问题常需**跨表检索**整合多张表中的信息才能回答。
- **现存难点**：
  - 如何有效理解**表内**与**表间**的知识关联。
  - 如何高效过滤冗余表格并精准检索最相关的表格。
  - 如何引导大模型在检索到的多表格上进行推理。
  - 缺乏贴近真实场景的多表问答评测基准。
- **整体含义**：本文旨在为**表格语料上的RAG**提供一个系统性的解决方案，涵盖索引构建、检索策略、生成提示和评测基准，从而提升结构化数据上复杂问答的性能。

### 2. 方法论
- **框架名称**：T‑RAG（Table‑Corpora‑Aware RAG）
- **核心组件**：
  - **分层记忆索引**：同时刻画**表内**与**表间**的知识结构，构造层级化索引以保存表格间的关联。
  - **多阶段检索流程**：逐步过滤冗余表格，精确定位与问题最相关的表格和表格片段，提高检索效率。
  - **图感知提示**：将检索到的表格形式化的图结构信息注入LLM提示，引导模型在表间关系上进行推理。
- **技术流程**：整体流程为“表格语料 → 分层记忆索引构建 → 多阶段检索 → 图感知提示引导LLM回答”。

### 3. 实验设计
- **评测基准**：首次构建多表问答基准 **MultiTableQA**，包含：
  - 3种不同任务类型
  - 57,193 张表格
  - 23,758 个问题
  - 数据均来源于真实场景。
- **对比方法**：
  - 表格检索方法
  - 不同RAG方法
  - 表格‑图表示学习方法
- **评估维度**：答案准确度、召回率、运行时间等，并进行不同LLM在T‑RAG下的推理能力升级评估。

### 4. 资源与算力
- 论文摘要和元数据中**未明确提及**使用的GPU型号、数量或训练时长。由于T‑RAG主要涉及索引构建与多阶段检索，通常推理阶段的资源需求较低，但具体算力细节需查阅全文方可知晓。

### 5. 实验数量与充分性
- **实验组数**：在摘要中体现多组对比：
  - 多类表格检索方法对比
  - 多种RAG方法对比
  - 多种图表示学习方法对比
  - 不同LLM在T‑RAG下的性能评估
- **充分性与公平性**：
  - 构建了大规模、多类型的真实场景评测集，覆盖多种任务，具备较高的现实模拟度。
  - 进行整体对比，同时控制T‑RAG框架，对下游LLM进行独立评估，设计相对系统。
  - 摘要未详细说明消融实验的具体数量，但整体实验覆盖面较广，能够支撑主要结论。

### 6. 主要结论与发现
- T‑RAG在**准确度、召回率和运行时间**上均表现领先。
- 分层记忆索引与多阶段检索能有效处理表格知识间的复杂关联，过滤冗余信息。
- MultiTableQA为结构化数据RAG提供了标准评测平台，揭示了不同方法之间的性能差异。
- 在T‑RAG框架下，多种LLM均能获得推理能力的提升，表明框架具有良好的模型适应性。

### 7. 优点（亮点）
- **问题新颖性**：首次系统研究面向表格语料的多阶段RAG，填补了文本RAG到结构化数据RAG的空白。
- **方法系统性**：从索引、检索到提示全流程设计，组件之间协同良好，兼顾效果与效率。
- **评测贡献**：MultiTableQA是首个大规模、多任务、真实来源的多表问答基准，对领域后续研究有重要推动作用。
- **实验全面**：比较了检索、RAG和图表征三大类方法，并单独评估LLM提升。

### 8. 不足与局限
- **实验细节透明性**：摘要未提供算力细节、超参数设置及消融实验的具体数量，难以独立判断资源开销和模块贡献度。
- **领域覆盖风险**：虽然基准源于真实场景，但可能仍偏向某些领域（如科学、金融等），在其他垂直领域表格结构下的表现待验证。
- **应用限制**：分层索引和多阶段检索对表格结构的依赖性较强，对于非结构化表格或复杂嵌套表头的适应性未在摘要中说明。
- **生成部分依赖**：框架高度依赖LLM的推理能力，在较弱LLM上的下限性能未提及。

（完）
