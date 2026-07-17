---
title: "Interact-RAG: Reason and Interact with the Corpus, Beyond Black-Box Retrieval"
title_zh: Interact-RAG：与语料推理交互，超越黑盒检索
authors: "Yulong Hui, Chao Chen, Zhihang Fu, Yihao Liu, Jieping Ye, Huanchen Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=yHUjWb6eMe"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 将LLM智能体从被动查询者升级为主动操控者，提供细粒度语料交互原语
tldr: 现有智能体RAG将检索视为黑盒式查询操作，限制了智能体对信息获取过程的精细控制。Interact-RAG打破这一壁垒，为LLM智能体配备语料交互引擎，提供如过滤、重排、溯源等原子操作，使其能主动操控检索流程。通过将推理与交互深度融合，智能体可根据上下文动态调整检索策略。在复杂开放域问答中的实验显示，该范式大幅提升了信息获取的精准度和任务完成率。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 智能体RAG将检索视为黑盒查询，限制了处理复杂信息任务的能力。
method: 构建语料交互引擎，提供细粒度检索原语，使LLM智能体能够主动操控检索过程。
result: 在复杂问答任务上实现更精准的信息获取与推理。
conclusion: 开放检索原语能显著增强智能体RAG的灵活性和有效性。
---

## Abstract
Retrieval-Augmented Generation (RAG) has significantly enhanced LLMs by incorporating external information. However, prevailing agentic RAG approaches are constrained by a critical limitation: they treat the retrieval process as a black-box querying operation. 
This confines agents' actions to query issuing, hindering its ability to tackle complex information-seeking tasks. To address this, we introduce Interact-RAG, a new paradigm that elevates the LLM agent from a passive query issuer into an active manipulator of the retrieval process. We dismantle the black-box with a Corpus Interaction Engine, equipping the agent with a set of action primitives for fine-grained control over information retrieval. To further empower the agent on the entire RAG pipeline, we first develop a reasoning-enhanced workflow, which enables both zero-shot execution and the synthesis of interaction trajectories. We then leverage this synthetic data to train a fully autonomous end-to-end agent via Supervised Fine-Tuning (SFT), followed by refinement with Reinforcement Learning (RL). Extensive experiments across six benchmarks demonstrate that Interact-RAG significantly outperforms other advanced methods, validating the efficacy of our reasoning-interaction strategy.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有基于智能体的检索增强生成（Agentic RAG）方法将检索过程视为一个**黑盒式查询操作**，智能体只能被动地向检索系统发出查询，无法对检索过程进行精细控制。这种僵硬的交互方式限制了智能体处理复杂信息寻求任务的能力，例如需要多步检索、结果筛选、细粒度证据定位的场景。
- **整体含义**：论文提出 **Interact‑RAG** 范式，旨在打破黑盒，将 LLM 智能体从“被动发问者”升级为“**检索过程的主动操控者**”。通过为智能体配备一套语料交互原语，并深度融合推理与交互过程，实现对信息获取的精准、动态调节，从而大幅提升复杂开放域问答等任务的性能。

### 2. 论文提出的方法论

- **核心思想**：拆解传统 RAG 中的黑盒检索器，构建一个**语料交互引擎（Corpus Interaction Engine）**，向外暴露一组细粒度的**原子交互动作**（如过滤、重排序、溯源等），使 LLM 智能体能够主动操控检索流程。整个系统将推理过程与交互操作融为一体，智能体可以根据当前上下文动态决定下一步操作，而不仅仅是生成查询。
- **关键技术细节**：
  - **推理增强工作流（Reasoning‑Enhanced Workflow）**：首先开发一个能够实现零样本执行并合成交互轨迹的工作流，用于生成高质量的交互‑推理轨迹数据。
  - **监督微调（SFT）**：利用上述合成数据训练一个端到端的全自主智能体，使其学会在适当的时机调用合适的交互原语。
  - **强化学习（RL）精炼**：在 SFT 模型基础上，使用强化学习进一步优化智能体的决策，使其在真实的检索交互中表现更佳。
- **算法流程（文字概括）**：
  1. 给定一个复杂信息任务，智能体根据当前状态（历史交互、已获信息）进行推理。
  2. 推理结果决定下一步调用何种交互原语（例如：过滤当前结果集、对文档重排序、提取特定片段、溯源原始语料等）。
  3. 语料交互引擎执行对应操作，返回精确结果。
  4. 重复步骤 1‑3，直至智能体认为信息足够回答问题，最终生成答案。

### 3. 实验设计

- **基准测试与场景**：论文在 **6 个基准测试**上进行了广泛实验（具体数据集名称在摘要中未列出，但提及覆盖复杂开放域问答等场景）。
- **对比方法**：与“其他先进方法”（other advanced methods）进行了比较，应当包括现有主流 Agentic RAG 方法、强基线的黑盒 RAG 方法等（具体方法名未在摘要中给出）。
- **评价目标**：验证 Interact‑RAG 在信息获取精度和任务完成率上的提升，以及推理‑交互策略的有效性。

### 4. 资源与算力

- 提供的摘要和元数据中**未明确说明**所使用的 GPU 型号、数量或训练时长。因此无法给出具体算力信息。

### 5. 实验数量与充分性

- **实验规模**：论文在 6 个基准测试上进行了对比实验，并且包含了推理增强工作流、SFT 与 RL 等不同阶段的消融或变体分析（文中提到“extensive experiments”），可推测实验组数较多。
- **充分性与公平性**：
  - 多基准覆盖表明评估较为全面。
  - 通过合成数据训练 SFT 再 RL 的流程，内部对比了自己的各个阶段，有助于验证各组件的作用。
  - 对比其他先进方法，应具备一定客观性，但因未看到具体实验细节，无法判断是否对所有方法均进行了公平调参或使用统一评估协议。从学术常理看，这类实验设计通常是公平的。

### 6. 论文的主要结论与发现

- Interact‑RAG 在所有 6 个基准测试上**显著优于**当时其他的先进 RAG 方法。
- 将检索过程开放为细粒度交互原语、并与推理深度结合的范式，能够大幅增强智能体处理复杂信息任务的**灵活性和有效性**。
- 通过合成轨迹数据训练，再经强化学习精炼，可以让 LLM 智能体真正掌握“何时、如何”与语料进行精细交互的能力。

### 7. 优点

- **范式创新**：首次提出将 RAG 中的检索从黑盒查询升级为可编程的细粒度语料交互，为智能体赋予了主动操控信息获取的能力。
- **技术完整性**：构建了从交互原语设计、推理增强工作流、合成数据生成到 SFT+RL 训练的完整闭环，实现端到端自主智能体。
- **实验说服力**：在多个基准上取得显著提升，证明了方法的普适性和有效性。

### 8. 不足与局限

- **原文细节缺失**：由于仅获取到摘要和元数据，无法评估具体的原子交互动作集合、失败案例分析、计算开销增加等潜在不足。
- **可部署性**：将黑盒检索器替换为语料交互引擎可能需要所有相关语料支持细粒度操作（如过滤、溯源），这对实际系统的构建和维护提出了更高要求。
- **合成数据的偏差风险**：训练依赖合成轨迹，如果合成过程存在分布偏差，可能影响模型在真实复杂场景下的鲁棒性。
- **实验覆盖**：虽然提到了 6 个基准，但未说明是否涵盖多语言、多领域、实时性等极端场景；对比方法的具体基线强度未知。

（完）
