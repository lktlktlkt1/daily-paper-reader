---
title: Efficient and Transferable Agentic Knowledge Graph RAG via Reinforcement Learning
title_zh: 通过强化学习实现高效可迁移的智能体知识图谱RAG
authors: "Jinyeop Song, Song Wang, Julian Shun, Yada Zhu"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=vyb4S7dbSx"
tags: ["query:agentic-rag"]
score: 10.0
evidence: KG-R1利用单个智能体通过RL与知识图谱交互，逐步检索和推理
tldr: 针对现有KG-RAG系统多模块组合导致高推理成本及绑定特定KG的问题，提出KG-R1框架，通过强化学习训练单一智能体，以KG为环境进行交互。该智能体学习逐步检索决策，并将检索信息融入推理和生成过程。端到端RL优化使得行为高效且可迁移，实验表明在多个KG上性能提升且推理成本降低，为智能体RAG提供了新的训练范式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有KG-RAG模块多、成本高、迁移性差，缺乏端到端优化的智能体方法。
method: 提出KG-R1，用RL训练单个智能体逐步与知识图谱交互检索并融入推理生成。
result: 在多个知识图谱上验证，性能提升且推理成本显著降低。
conclusion: 通过RL训练，KG-R1实现了高效、可迁移的智能体KG增强生成。
---

## Abstract
Knowledge-graph retrieval-augmented generation (KG-RAG) couples large language models (LLMs) with structured, verifiable knowledge graphs (KGs) to reduce hallucinations and expose reasoning traces. However, many KG-RAG systems compose multiple LLM modules (e.g planning, reasoning, and responding), inflating inference cost and binding behavior to a specific target KG. To address this, we introduce KG-R1, an agentic KG retrieval-augmented generation (KG-RAG) framework through reinforcement learning (RL). KG-R1 utilizes a single agent that interacts with KGs as its environment, learning to retrieve at each step and incorporating the retrieved information into its reasoning and generation. The process is optimized through end-to-end RL. In controlled experiments across Knowledge-Graph Question Answering(KGQA) benchmarks, our method demonstrates both efficiency and transferability: Using Qwen-2.5-3B, KG-R1 improves answer accuracy with fewer generation tokens than prior multi-module workflow methods that use larger foundation or fine-tuned models. Furthermore, KG-R1 enables plug and play: after training, it maintains strong accuracy on new KGs without modification. These properties make KG-R1 a promising KG-RAG framework for real-world deployment. Our code is publicly available at anonymous.4open.science/r/RL_KG-4B4E.

---

## 论文详细总结（自动生成）

由于提供的资料仅包含论文元数据（摘要、标题、作者、动机、方法、结果、结论等），并未包含论文全文 PDF 的实际内容，因此以下总结完全基于元数据中的信息进行，不涉及具体公式、实验细节或定量结果。若需要更全面的分析，请提供完整论文内容。

### 1. 论文的核心问题与整体含义
- **研究背景**：知识图谱检索增强生成（KG‑RAG）通过将大语言模型（LLM）与结构化、可验证的知识图谱（KG）结合，来减少幻觉并暴露推理轨迹。
- **核心问题**：现有 KG‑RAG 系统往往由多个 LLM 模块（如规划、推理、响应）组合而成，导致推理成本飙升，且系统行为高度绑定到特定的目标 KG，缺乏迁移能力。同时，目前缺乏一种端到端优化的智能体方法来统一检索与生成。
- **整体含义**：本文旨在提出一种新的智能体框架，通过强化学习训练单一智能体，使其能在 KG 环境中逐步检索并生成答案，从而提升效率、降低推理成本，并实现跨不同 KG 的即插即用迁移。

### 2. 论文提出的方法论
- **核心思想**：将 KG‑RAG 重新定义为一个强化学习任务，用单个智能体与环境（知识图谱）交互，自主决定何时检索、检索什么，并将检索到的信息融入后续推理与生成，整个过程通过端到端 RL 直接优化最终答案质量。
- **关键技术细节**（基于元数据）：
  - **框架名称**：KG‑R1。
  - **智能体设计**：单一智能体取代了传统的多模块流水线（如分离的规划器、检索器、推理器）。
  - **交互机制**：每步智能体会根据当前状态选择检索操作，获取 KG 中的相关事实，然后更新状态继续推理，最后生成最终答案。
  - **优化范式**：采用端到端强化学习，奖励信号可能基于最终答案的正确性或其他质量指标，从而将检索决策与生成质量联合优化。
  - **算法流程**（文字描述）：给定问题 → 智能体初始化 → 循环：智能体选择动作（检索/推理/生成） → 若检索则查询 KG 并获取三元组 → 将信息追加到上下文 → 重复直至智能体决定生成答案 → 根据答案反馈计算奖励并更新策略。
- **关键特点**：无需特定于 KG 的模块，训练后可直接应用于未见过的 KG（即插即用）。

### 3. 实验设计
- **数据集/场景**：在多个知识图谱问答（KGQA）基准测试集上进行受控实验（元数据未列出具体数据集名称）。
- **基准对比方法**：对比了先前的多模块工作流方法，这些方法通常使用更大的基础模型或经过微调的模型。
- **使用的模型**：以 Qwen‑2.5‑3B 作为骨干模型进行训练和评估。
- **评估指标**：答案准确率，以及生成 token 数量（衡量推理成本）。

### 4. 资源与算力
- **说明**：提供的元数据中没有提及任何关于 GPU 型号、数量、训练时长或算力消耗的信息。无法从现有资料中获知算力需求。

### 5. 实验数量与充分性
- **实验数量**：元数据仅提及“在多个 KGQA 基准上进行控制实验”以及“迁移性验证”（即在新 KG 上测试），但未给出具体的实验组数、消融研究或统计检验。因此无法判断实验是否足够丰富。
- **充分性与公平性**：摘要声称与使用更大模型或微调模型的先前方法进行了比较，并展示了 token 效率和可迁移性，在方法上看起来是客观的对比。但由于缺少完整论文，无法评估数据划分、基线实现、随机种子等实验公平性细节。

### 6. 论文的主要结论与发现
- KG‑R1 通过端到端强化学习，成功训练出一个高效、可迁移的单一智能体，用于 KG 增强生成。
- 与多模块工作流相比，KG‑R1 使用更小的模型（Qwen‑2.5‑3B）在提升答案准确率的同时，显著减少了生成 token 数，降低了推理成本。
- 训练后的智能体展现出很强的迁移性：无需任何修改即可在新知识图谱上保持较高的准确率，实现了“即插即用”。
- 该方法为智能体 RAG 系统提供了一种新的训练范式，有望在实际部署中发挥作用。

### 7. 优点
- **端到端优化**：将检索决策与答案生成统一在 RL 框架下，避免了多模块代理损失不一致问题。
- **推理高效**：使用单一智能体，减少模块间通信开销和 token 消耗，能够以更小的模型取得竞争力的性能。
- **通用可迁移**：不绑定特定 KG，训练完成后可直接迁移到其他 KG，极大降低了适配成本。
- **范式创新**：首次将“KG 作为环境、LLM 作为智能体”的 RL 训练引入到 KG‑RAG 中，为相关研究提供新方向。

### 8. 不足与局限
- **信息缺失严重**：基于元数据无法获知具体实验细节，例如所用 KG 的规模与领域、baseline 的具体配置、消融实验的设计等，因此难以判断结论的普适性。
- **模型规模与任务局限性**：仅验证了 3B 模型在 KGQA 任务上的效果，对于更大参数量的模型、更复杂的多跳推理或对话场景，方法是否仍然有效未知。
- **训练成本未披露**：RL 训练可能引入额外的样本复杂度和训练时间，论文未提供算力或训练时间的数据。
- **潜在偏差**：基于元数据的描述偏正面，可能存在“报喜不报忧”的偏差，实际论文可能包含更多局限性（如 RL 训练稳定性、奖励设计等）未在元数据中体现。
- **应用限制**：该方法假设知识图谱是可查询的结构化环境，对于图谱不完整或无法交互的场景可能无法直接应用。

（完）
