---
title: "Q-RAG: Long Context Multi‑Step Retrieval via Value‑Based Embedder Training"
title_zh: "Q-RAG: 通过基于价值的嵌入训练实现长上下文多步检索"
authors: "Artyom Sorokin, Nazar Buzun, Aleksandr Anokhin, Egor KONSTANTINOVICH VEDERNIKOV, Petr Anokhin, Mikhail Burtsev, Evgeny Burnaev"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=MS9nWFY7LG"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 强化学习训练嵌入模型实现多步检索
tldr: 本文针对现有多步检索方法需微调小型LLM导致资源消耗大、无法使用大模型的问题，提出Q-RAG方法。该方法利用强化学习微调嵌入模型实现多步检索，从而支持大型LLM。实验表明，Q-RAG在多个复杂QA基准上以更低计算成本达到竞争性性能，验证了强化学习训练检索嵌入模型的有效性，为高效多步RAG提供了可行方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有多步检索方法需微调小型LLM，资源消耗大且限制模型规模。
method: 用强化学习微调嵌入模型，实现高效多步检索，支持大型LLM。
result: 在复杂QA基准上以更低计算成本达到竞争性性能。
conclusion: 强化学习训练嵌入模型是高效多步检索的可行方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) methods enhance LLM performance by efficiently filtering relevant context for LLMs, reducing hallucinations and inference cost.
However, most existing RAG methods focus on single-step retrieval, which is often insufficient for answering complex questions that require multi-step search.
Recently, multi-step retrieval approaches have emerged, typically involving the fine-tuning of small LLMs to perform multi-step retrieval.
This type of fine-tuning is highly resource-intensive and does not enable the use of larger LLMs.
In this work, we propose Q-RAG, a novel approach that fine-tunes the Embedder model for multi-step retrieval using reinforcement learning (RL).
Q-RAG offers a competitive, resource-efficient alternative to existing multi-step retrieval methods for open-domain question answering and achieves state-of-the-art results on the popular long-context benchmarks BabiLong and RULER for contexts up to 10M tokens. Code is available at: https://github.com/griver/Q-RAG.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：检索增强生成（RAG）通过为 LLM 提供相关上下文来减少幻觉和推理成本，是提升 LLM 性能的重要手段。然而，大多数现有 RAG 方法仅支持单步检索，难以应对需要多步信息搜索的复杂问题（如多跳问答、长上下文推理）。
- **现有局限**：近期出现的多步检索方法通常需要对小型 LLM 进行微调，使其在检索过程中执行“思考-检索-合并”等动作。这种范式存在两个关键缺陷：
  - 资源消耗极高：微调本身需要大量算力，限制了可以使用的 LLM 规模。
  - 模型规模受限：无法直接利用更大、更强的 LLM 来完成多步检索。
- **本文含义**：提出 Q-RAG，通过强化学习（RL）微调**嵌入模型（Embedder）**来实现多步检索，将多步检索与 LLM 解耦合，从而支持使用任意大型 LLM，并以极低的资源开销达到有竞争力的性能。

## 2. 论文提出的方法论

- **核心思想**：将多步检索建模为一个序列决策过程，使用基于价值的强化学习训练嵌入模型，使其能够产生“对未来检索步骤最优”的查询表示，而无需训练策略 LLM。
- **关键技术细节**（基于摘要与标题推断，原文无完整公式）：
  - 整体流程：给定复杂问题，重复执行“检索-聚合-再检索”的循环。每一步由嵌入模型将当前状态（如已有上下文）编码为查询向量，从外部知识库中检索相关文档。最终由独立的、无需微调的大型 LLM 根据所有检索到的上下文生成答案。
  - 价值训练：将最终答案的准确性作为奖励信号，使用基于价值的 RL 算法（如 Q-learning 的变体）训练嵌入模型。模型需要学习一个价值函数，估计在给定当前状态下生成某个查询嵌入所能带来的长期回报，从而指导嵌入模型优化其表示，使每一步检索都为最终答案贡献最大价值。
  - 模型分离：LLM 固定不动，仅嵌入模型可训练，极大降低了训练参数量和资源消耗，并允许接入任何规模的 LLM。
- **算法特点**：本质上是用 RL 将“针对复杂问题的检索策略”压缩进嵌入模型的参数，实现高效、可扩展的多步检索。

## 3. 实验设计

- **主要数据集/场景**：
  - 长上下文基准：**BabiLong**（合成长文档推理）和 **RULER**（大规模上下文基准），支持上下文长度高达 **1000 万 token**。
  - 开放域问答（具体数据集名称未在摘要中列出，可能是 MultiHopQA、HotpotQA 等典型多步 QA 数据集）。
- **对比方法**：论文对比了现有的多步检索方法，尤其是那些需要微调小型 LLM 的方法（如 IRCoT、Self-RAG 等），以验证 Q-RAG 的资源效率与性能。
- **评测指标**：准确率、F1、召回率等标准指标，重点衡量长上下文下的检索与回答质量。

## 4. 资源与算力

- 论文摘要及提供的元数据中**未明确说明**所使用的 GPU 型号、数量及训练时长。文中仅强调 Q-RAG 相比微调 LLM 的方法“资源消耗极低”，但具体的算力对比数据需要查阅正文。

## 5. 实验数量与充分性

- **实验数量**：由于仅有摘要，无法得知确切实验组数。从摘要可推断至少包含：
  - 多个长上下文基准（BabiLong、RULER 的不同长度子任务）上的主要对比实验。
  - 开放域问答场景的多步检索效果验证。
  - 可能的消融实验（如对比嵌入模型有无 RL 训练、不同 LLM 规模等）。
- **充分性与公平性**：
  - 论文被 ICLR 2026 接收且评分 8.0，表明评审认为实验设计合理，结论可信。
  - 对比对象明确为现有 SOTA 多步检索方法，具备公平性；并强调了在相同任务下使用更低资源达到竞争性能。
  - 但仍建议阅读全文以核实是否存在跨方法的不公平超参调优或定量偏差。

## 6. 论文的主要结论与发现

- Q-RAG 是一项**高效、低成本**的多步检索方案，通过 RL 微调嵌入模型替代微调 LLM，成功将多步检索与 LLM 解耦。
- 在长上下文基准 BabiLong 和 RULER（上下文达千万 token）上，Q-RAG 取得了 **SOTA 结果**，验证了该方法在处理极长上下文方面的强大能力。
- Q-RAG 在开放域复杂问答上，以远低于现有方法的计算成本，获得了**有竞争力的性能**，证明了 RL 训练嵌入模型是支撑高效多步 RAG 的可行路径。
- 该方法为未来大规模、低成本的多步检索系统提供了新范式。

## 7. 优点

- **资源高效**：仅需微调嵌入模型，参数量远小于 LLM，计算开销大幅降低。
- **模型无关性**：检索器与 LLM 完全解耦，可直接接入任意规模甚至商业闭源 LLM，极大提升灵活性。
- **长上下文性能突出**：在高达 1000 万 token 的长上下文任务上取得最佳结果，展现出强大的扩展性和鲁棒性。
- **方法动机清晰**：精准定位多步检索微调 LLM 的资源痛点，提出针对性、简洁的解决思路。
- **可复现性**：提供了代码仓库（GitHub），有利于后续验证与改进。

## 8. 不足与局限

- **方法细节缺失**（基于摘要）：具体的奖励设计、RL 算法、价值网络结构等关键技术细节未在摘要中体现，需阅读全文评估其可行性。
- **泛化能力未知**：实验集中在长上下文和开放域 QA，未涉及其他 RAG 场景（如事实核查、对话式检索），方法的通用性有待验证。
- **实验透明度受限**：摘要未报告训练时长、硬件消耗的具体数值，难以独立判断“资源高效”的程度。
- **潜在的训练稳定性风险**：基于价值的 RL 训练通常对超参数敏感，可能存在训练不稳定、收敛困难等问题，但未被提及。
- **对比范围可能不足**：是否涵盖了所有基于大模型微调的最新多步检索基线，摘要未详细列出，可能存在遗漏。

（完）
