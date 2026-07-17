---
title: Reinforced Internal-External Knowledge Synergistic Reasoning for Efficient Adaptive Search Agent
title_zh: 强化内外知识协同推理的高效自适应搜索智能体
authors: "Ziyang Huang, Xiaowei Yuan, Yiming Ju, Haoran Cai, Jun Zhao, Kang Liu"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=IEDYctsolA"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 提出IKEA智能体，协同使用内部参数知识和检索外部知识，通过RL优化检索时机
tldr: 现有基于RL的搜索智能体经常忽视自身参数化知识，导致冗余检索与潜在知识冲突。IKEA提出一种内外知识协同推理机制，让智能体在强化学习中学会自主判断是否需要检索以及如何融合内外信息。通过自适应检索时机决策与知识整合策略，IKEA在保持高准确率的同时显著降低了检索次数与推理延迟。实验验证了该框架在多源知识场景下的高效性与鲁棒性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有搜索智能体未能充分利用内部知识，导致冗余检索和知识冲突。
method: 设计IKEA智能体，利用强化学习实现自适应检索和内外知识协同推理。
result: 有效减少冗余检索，降低推理延迟，提升回答质量。
conclusion: 内外知识协同能显著增强搜索智能体的效率与可靠性。
---

## Abstract
Retrieval-augmented generation (RAG) is a common strategy to reduce hallucinations in Large Language Models (LLMs). While reinforcement learning (RL) can enable LLMs to act as search agents by activating retrieval capabilities, existing ones often underutilize their internal knowledge. This can lead to redundant retrievals, potential harmful knowledge conflicts, and increased inference latency. To address these limitations, an efficient and adaptive search agent capable of discerning optimal retrieval timing and synergistically integrating parametric (internal) and retrieved (external) knowledge is in urgent need. This paper introduces the Reinforced Internal-External Knowledge Synergistic Reasoning Agent (IKEA), which could indentify its own knowledge boundary and prioritize the utilization of internal knowledge, resorting to external search only when internal knowledge is deemed insufficient. This is achieved using a novel knowledge-boundary aware reward function and a knowledge-boundary aware training dataset. These are designed for internal-external knowledge synergy oriented RL, incentivizing the model to deliver accurate answers, minimize unnecessary retrievals, and encourage appropriate external searches when its own knowledge is lacking. Evaluations across multiple knowledge reasoning tasks demonstrate that IKEA significantly outperforms baseline methods, reduces retrieval frequency significantly, and exhibits robust generalization capabilities.

---

## 论文详细总结（自动生成）

# 论文总结：Reinforced Internal-External Knowledge Synergistic Reasoning for Efficient Adaptive Search Agent

## 1. 核心问题与整体含义
- **研究动机**：现有基于强化学习（RL）的检索增强生成（Retrieval-Augmented Generation, RAG）智能体在充当“搜索智能体”时，普遍**未能充分利用自身参数化（内部）知识**。
- **核心问题**：这种对内、外知识的非协同使用导致了三个弊端：
  - **冗余检索**：在模型已具备相关知识时仍触发外部搜索，浪费计算与时间。
  - **知识冲突**：检索到的外部信息可能与内部已有知识矛盾，损害回答质量。
  - **推理延迟升高**：不必要的搜索显著增加响应时间。
- **整体含义**：论文提出需要一种能够**自主判断检索时机、优先使用内部知识、仅在内部知识不足时进行外部搜索**的高效自适应搜索智能体。

## 2. 方法论
- **智能体名称**：IKEA（Reinforced **I**nternal-External **K**nowledge Synergistic Reasoning Agent）
- **核心思想**：
  - 让智能体通过强化学习学会**辨识自身知识边界**，优先利用参数化知识。
  - 只有当内部知识被认为不足时，才调用外部检索。
  - 检索发生后，能**协同整合**内部（参数化）与外部（检索）知识。
- **关键技术组件**：
  1.  **知识边界感知奖励函数**：奖励模型给出正确答案，同时**惩罚不必要的检索**；在自身知识确实匮乏时，又鼓励适当的搜索。
  2.  **知识边界感知训练数据集**：专为内部-外部知识协同的强化学习设计，训练模型辨别何时需要检索。
  3.  **强化学习优化目标**：通过上述奖励和数据集，用 RL 优化智能体的自适应检索与协同推理策略。
- **流程**：输入问题 → 模型根据内部知识初步判断是否足够 → 若足够，直接生成答案；若不足，触发检索 → 整合外部信息与内部知识，生成最终答案。整个过程由 RL 策略驱动。

## 3. 实验设计
- **数据集与场景**：摘要仅提到“多种知识推理任务”（multiple knowledge reasoning tasks），未列出具体名称（如开放域问答、多跳推理等）。需要查看全文才可获知。
- **基准方法**：对比了基线方法（baseline methods），包括现有基于 RL 的搜索智能体及其他 RAG 方案，但摘要未列出具体对比对象。
- **评测指标**：准确率、检索频率、推理延迟、泛化能力等（摘要提及）。

## 4. 资源与算力
- **摘要中未提供任何算力信息**（如 GPU 型号、数量、训练时长等）。需依赖原文补充。

## 5. 实验数量与充分性
- **实验组数**：摘要未给出具体数量。从表述“evaluations across multiple knowledge reasoning tasks”推断，应涵盖多个任务、多种对比方法和消融实验，但详尽程度不明。
- **充分性与公平性**：摘要声称 IKEA“显著优于基线方法”，并展示了检索频率的显著降低与强泛化能力，初步表明实验具有说服力。但由于未披露数据集细节、对比方法细节、消融设计，暂时无法判断充分性。需完整论文评估。

## 6. 主要结论与发现
- IKEA 能显著**减少冗余检索**，从而降低推理延迟。
- 在保持高准确率（甚至提升准确性）的同时，有效避免有害的知识冲突。
- 泛化能力（robust generalization capabilities）强，表明该框架适用于多种知识推理场景。

## 7. 优点
- **新颖的协同机制**：将内部知识与外部检索在强化学习框架下动态协同，不再把检索视为独立步骤。
- **高效的检索策略**：通过知识边界感知，实现“按需搜索”，避免资源浪费。
- **奖励函数与数据集设计**：针对内外知识协同这一目标，专门设计了知识边界感知的奖励和训练数据，思路简洁、目标明确。
- **实用价值**：直接缓解了 RAG 智能体的高延迟、高冗余问题，离实际部署更近一步。

## 8. 不足与局限
- **信息缺失严重**：仅从摘要评判，大量关键细节未知：
  - 未列出具体数据集与对比方法，无法评估实验的广度和代表性。
  - 未报告算力开销，难以判断训练成本。
  - 未提及 IKEA 的外部检索器类型（如稠密检索、稀疏检索）、检索库规模等，限制了复现可能。
- **泛化性仍待验证**：摘要提到“多任务”评估，但究竟是哪些任务、是否跨领域、是否覆盖低资源场景，这些都会影响结论的普适性。
- **内部知识静态性假设**：实际应用中，模型知识会过时，论文未说明如何处理内部知识陈旧导致误判“不需要检索”的风险。
- **奖励设计可能隐含偏差**：知识边界感知奖励函数若设计不当，可能导致过度保守（很少搜索）或检索抑制影响未知答案的获取，摘要未给出分析。

（完）
