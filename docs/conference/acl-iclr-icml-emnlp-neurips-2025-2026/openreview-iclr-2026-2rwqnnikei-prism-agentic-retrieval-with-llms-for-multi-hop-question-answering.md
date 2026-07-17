---
title: "PRISM: Agentic Retrieval with LLMs for Multi-Hop Question Answering"
title_zh: PRISM：面向多跳问答的智能体驱动检索
authors: "Md Mahadi Hasan Nahid, Davood Rafiei"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=2rwqNNIKeI"
tags: ["query:agentic-rag"]
score: 10.0
evidence: 三专用LLM智能体的迭代循环式检索系统
tldr: 面向多跳问答中需收集多条证据的挑战，提出智能体驱动检索系统PRISM，由问题分析、选择和补充三个智能体迭代协作，生成紧凑且全面的证据集合，在精确率和召回率上取得优异表现。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 多跳问答需要高精确率和高召回率的检索，现有方法难以兼顾。
method: 设计PRISM框架，包含问题分析器、选择器和补充器三个专用LLM智能体，迭代交互以实现精准全面的证据检索。
result: 在多跳QA基准上，PRISM以紧凑证据集达到领先性能。
conclusion: 智能体驱动的迭代检索为复杂问答提供了高效可解释的解决方案。
---

## Abstract
Retrieval plays a central role in multi-hop question answering (QA), where answering complex questions requires gathering multiple pieces of evidence. We introduce an Agentic Retrieval System that leverages large language models (LLMs) in a structured loop to retrieve relevant evidence with high precision and recall. Our framework consists of three specialized agents: a Question Analyzer that decomposes a multi-hop question into sub-questions, a Selector that identifies the most relevant context for each sub-question (focusing on precision), and an Adder that brings in any missing evidence (focusing on recall). The iterative interaction between Selector and Adder yields a compact yet comprehensive set of supporting passages. In particular, it achieves higher retrieval accuracy while filtering out distracting content, enabling downstream QA models to surpass full-context answer accuracy while relying on significantly less irrelevant information. Experiments on four multi-hop QA benchmarks---HotpotQA, 2WikiMultiHopQA, MuSiQue, and MultiHopRAG---demonstrates that our approach consistently outperforms strong baselines.

---

## 论文详细总结（自动生成）

# PRISM: 面向多跳问答的智能体驱动检索

## 1. 论文的核心问题与整体含义

- **核心问题**：在多跳问答中，回答复杂问题需要从大量文档中收集多段证据。现有检索方法难以同时实现高精确率和高召回率，要么漏掉关键证据，要么引入大量噪声。
- **研究动机**：检索环节的性能直接决定下游问答模型的上限。需要一种能够精准定位相关证据、同时不遗漏必要信息的检索系统。
- **整体含义**：论文提出一种智能体驱动的迭代检索框架PRISM，利用大语言模型（LLM）的结构化交互，生成紧凑且全面的证据集，从而在降低无关内容的同时提升答案准确率。

## 2. 论文提出的方法论

- **核心思想**：将检索任务分解为三个专用智能体的协作循环，分别负责问题分解、精确选择和召回补充，通过迭代优化证据集合。
- **三个智能体及其角色**：
  - **问题分析器**：将多跳问题拆分为若干子问题。
  - **选择器**：针对每个子问题识别最相关的上下文，注重精确率。
  - **补充器**：引入可能遗漏的证据，注重召回率。
- **流程**：问题分析器生成子问题 → 选择器为每个子问题检索高精确率上下文 → 补充器检查并补充缺失证据 → 选择器与补充器迭代交互，最终输出紧凑而全面的支持段落集合。
- **关键特点**：利用LLM的语义理解与推理能力，实现智能体间的反馈循环，在有限迭代中平衡精确率与召回率。

## 3. 实验设计

- **数据集**：四个多跳问答基准——HotpotQA、2WikiMultiHopQA、MuSiQue 和 MultiHopRAG。
- **对比方法**：与强基线进行对比（摘要未列出具体基线名称，可能包括传统稀疏/稠密检索、多步检索及基于LLM的检索方法）。
- **评估指标**：检索准确率、答案准确率，同时关注证据集的紧凑性（减少无关内容）。

## 4. 资源与算力

- **说明**：提供的摘要和元数据中**未明确说明**使用的GPU型号、数量、训练时长或推理算力。推测该方法主要依赖LLM的推理调用（可能通过API或本地部署），但具体资源消耗无从得知。

## 5. 实验数量与充分性

- **实验组数**：摘要未给出具体实验数量，但提及在四个数据集上评估，且声称“持续优于强基线”，暗示至少包含各数据集的主实验。
- **充分性**：从摘要看，覆盖了多个不同类型的多跳QA基准，对比了强基线，且验证了证据紧凑性带来的下游回答提升，实验设计较为全面。但摘要未提及消融实验、超参数分析或统计显著性检验，无法判断消融研究是否充分。
- **公平性**：声称与强基线对比，且强调使用紧凑证据集仍能超越全上下文答案准确率，表面对比公平。

## 6. 论文的主要结论与发现

- PRISM的智能体迭代检索框架在多跳QA基准上，以**更紧凑的证据集**达到领先的检索准确率和答案准确率。
- 通过选择器与补充器的分工协作，系统能够**过滤干扰内容**，使下游QA模型在依赖显著更少无关信息的情况下，仍然超越使用全量上下文的答案准确率。
- 智能体驱动的结构化检索为复杂问答提供了高效且可解释的解决方案。

## 7. 优点

- **创新性架构**：将检索过程建模为三个专用智能体的协作，分解清晰，可解释性强。
- **兼顾精确与召回**：通过选择器和补充器的迭代，在紧凑性和全面性之间取得平衡，优于传统单一评分排序方法。
- **通用性**：在四个不同类型的多跳QA基准上均表现优异，验证了方法的泛化能力。
- **下游友好**：减少无关信息输入，直接提升下游问答模型的效能与效率。

## 8. 不足与局限

- **细节缺失**：由于仅提供摘要，许多关键技术细节（如智能体实现方式、LLM种类、迭代停止条件、训练/微调情况）不明，无法深入评估其可复现性。
- **计算开销**：多智能体迭代调用LLM可能带来较高推理延迟和成本，摘要未讨论效率问题。
- **消融实验未知**：未说明各智能体、迭代次数等组件的贡献，削弱了对设计有效性的理解。
- **偏差风险**：依赖单一LLM进行分解、选择和补充，可能继承模型的内部偏差或幻觉，影响检索正确性。
- **应用限制**：仅在公开多跳QA数据集上验证，真实场景下的噪声文档、动态知识库或低资源领域适用性未知。

（完）
