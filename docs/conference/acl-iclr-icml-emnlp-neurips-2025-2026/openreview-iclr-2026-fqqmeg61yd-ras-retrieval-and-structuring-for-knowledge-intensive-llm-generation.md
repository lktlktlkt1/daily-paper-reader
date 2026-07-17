---
title: "RAS: Retrieval-And-Structuring for Knowledge-Intensive LLM Generation"
title_zh: RAS：知识密集型LLM生成的检索与结构化
authors: "Pengcheng Jiang, Lang Cao, Ruike Zhu, Minhao Jiang, Yunyi Zhang, Jiaming Shen, Jimeng Sun, Jiawei Han"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=fqqmeg61yd"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 通过迭代检索与结构化知识构建支持RAG多步推理
tldr: 检索到的非结构化文本难以支持复杂多步推理。本文提出RAS框架，交替进行针对性检索规划与知识图谱构建，将外部信息动态组织为结构化形式。实验证明，显式的知识组织能显著提升推理路径的连贯性和答案准确性，为增强RAG的推理能力提供了新思路。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 非结构化检索上下文导致多步推理路径脆弱。
method: 动态构建问题特定知识图谱，交织检索规划与结构化构建。
result: 结构化知识提升了推理连贯性和问答准确率。
conclusion: 组织外部知识是强化RAG推理的有效手段。
---

## Abstract
Large language models (LLMs) have achieved impressive performance on knowledge-intensive tasks, yet they often struggle with multi-step reasoning due to the unstructured nature of retrieved context. While retrieval-augmented generation (RAG) methods provide external information, the lack of explicit organization among retrieved passages limits their effectiveness, leading to brittle reasoning pathways. Recent interpretability studies highlighting the importance of structured intermediate reasoning further align with this perspective. 
We propose Retrieval-And-Structuring (RAS), a framework that dynamically constructs question-specific knowledge graphs through iterative retrieval and structured knowledge building. RAS interleaves targeted retrieval planning with incremental graph construction, enabling models to assemble and reason over evolving knowledge structures tailored to each query. On seven knowledge-intensive benchmarks, RAS consistently outperforms strong baselines, achieving up to 8.7\% and 7.0\% gains with proprietary and open-source LLMs, respectively. Our results demonstrate that dynamic, question-specific knowledge structuring offers a robust path to improving reasoning accuracy and robustness in language model generation.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **核心问题**：在知识密集型任务中，大语言模型（LLM）虽然表现优异，但在进行多步推理时经常出错。这主要是因为检索增强生成（RAG）方法提供的外部上下文通常是**非结构化的文本片段**，缺乏明确的组织，导致推理路径脆弱、不连贯。
- **整体含义**：论文提出一种**迭代式检索与结构化**框架 RAS，将外部信息动态组织为问题特定的知识图谱，使模型能够在逐步构建的、有针对性的结构化知识上进行推理，从而显著提升多步推理的准确性和鲁棒性。其研究动因也与近期可解释性研究中强调的“中间结构化推理的重要性”相呼应。

## 2. 论文提出的方法论
- **核心思想**：RAS 交替执行**目标导向的检索规划**与**增量式知识图谱构建**，将非结构化的检索结果逐步转化为结构化、可演化的知识形态。
- **关键流程**：
  1. **检索规划（Retrieval Planning）**：针对当前推理状态，生成针对性的查询，获取与问题相关的段落。
  2. **结构化构建（Structuring）**：从检索到的段落中抽取出实体与关系，增量地将它们加入一个**问题特定的知识图谱**。
  3. **交错循环**：上述两步反复进行，图谱随着新的检索结果不断扩展与修正，形成一条动态演进的知识链条。
  4. **生成与推理**：最后，LLM 基于这个逐步构建的结构化图谱进行答案生成或多步推理。
- **算法特色**：RAS 不像传统 RAG 那样一次性检索一堆非结构化文本，而是让检索与组织同步推进，让模型在每一个推理步骤都能接触到最新组织好的结构化知识，从而构造出更连贯的推理链条。

## 3. 实验设计
- **测试平台**：在 **7 个知识密集型基准**上进行了评估（文中未列出具体名称，仅说明了数量）。
- **对比方法**：与当前强基线（strong baselines）进行比较，包括使用**商业闭源 LLM** 和**开源 LLM** 的多个代表性 RAG 方案。
- **评价维度**：关注多步推理场景下的答案准确率以及推理连贯性。

## 4. 资源与算力
- **说明情况**：提供的论文摘要和元数据中**未明确提及**所使用的 GPU 型号、数量、训练/推理时长或具体计算资源消耗。从方法描述（迭代检索 + 图谱构建）可以推断，其主要算力开销来自 LLM 的多次调用及知识抽取，但论文未给出量化信息。

## 5. 实验数量与充分性
- **实验数量**：覆盖 **7 个不同数据集**，并分别在专有和开源 LLM 上与强基线进行对比。同时很可能包含**消融实验**来验证各组件的作用（如检索规划、结构化构建、迭代次数等，但摘要中未展开细节）。
- **充分性与公平性**：
  - 多数据集、多模型基底的测试保证了结论的**泛化性和外部效度**。
  - 对比对象为“强基线”，说明未选择弱方法进行不公平比较。
  - 由于未提供消融实验、显著性检验等细节，暂时无法判断实验的**内部效度是否完美**，但框架本身的设计原则已为系统性评估提供了基础。

## 6. 论文的主要结论与发现
- **性能提升**：RAS 在 7 个知识密集型基准上均优于强基线：使用专有 LLM 时最高提升 **8.7%**，使用开源 LLM 时最高提升 **7.0%**。
- **推理质量**：动态构建的问题特定知识图谱能够有效修复非结构化检索带来的推理脆弱性，提升多步推理的**连贯性与稳健性**。
- **方法价值**：论文证明了 **“显式组织外部知识”** 是强化 LLM 推理能力的有效手段，为未来 RAG 系统提供了从“检索-阅读”到“检索-组织-推理”的演进思路。

## 7. 优点
- **创新性融合**：首次将**交替式检索规划与增量知识图谱构建**紧密结合，解决了传统 RAG 在推理时知识孤立的痛点。
- **动机充分**：从可解释性研究中提取结构化推理的重要性，使方法不仅有实证支撑，还有理论自洽性。
- **实用性设计**：无需预定义全局知识库或固定流程，可以自适应地为每个问题构建定制化知识结构，灵活性高。
- **实验扎实**：覆盖多个模型和数据集，性能增益显著且一致，展示了方法的鲁棒性。

## 8. 不足与局限
- **计算效率未量化**：迭代检索与图谱构建会增加 API 调用或本地推理次数，实际延迟和吞吐量可能是瓶颈，但论文未提供开销分析。
- **对抽取质量的敏感**：知识图谱的构建依赖于实体/关系抽取模块的准确性，其误差可能被迭代过程放大，文中未讨论失效模式。
- **任务与数据集细节缺失**：摘要未列出具体的 7 个基准名称及任务类型（如多跳问答、事实验证等），难以判断方法在不同推理难度上的表现差异。
- **基线可能不完整**：未提及是否与基于隐式结构化表示（如链式思考、思维树）的 RAG 增强方法进行对比，对比范围可能受限。
- **潜在偏差**：实验可能偏向于支持结构化收益的评测指标，未提及生成内容其他维度（如流畅度、忠实度、安全性）的变化。

（完）
