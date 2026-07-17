---
title: "AOEB: Benchmarking Agent-Oriented Multimodal Embeddings"
title_zh: AOEB：面向智能体的多模态嵌入基准测试
authors: "Xin Zhang, Jiaxin Xu, mengjia zhou, Xinping Zhao, Yinghui Li, di yin, Xing Sun, Meishan Zhang, Baotian Hu, Wenjie Li, Min Zhang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6e1f3a3a7181ec86650fcfd44d05c06f76d98415.pdf"
tags: ["query:agentic-rag"]
score: 4.0
evidence: 面向智能体检索的多模态嵌入基准，涵盖推理检索
tldr: 现有嵌入基准无法满足智能体应用的多样化需求，提出面向智能体的多模态嵌入基准AOEB，覆盖代码、工具、推理和记忆检索等五大关键能力，为智能体RAG中的嵌入模型提供全面评测。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 通用嵌入基准与智能体RAG中的检索需求不匹配。
method: 构建多任务多模态的AOEB基准，涵盖五个智能体关键检索能力。
result: 实验揭示了当前嵌入模型在智能体场景下的性能差距。
conclusion: 为智能体驱动RAG的嵌入组件选择与改进提供了评估依据。
---

## Abstract
LLM agents powered by retrieval and RAG are increasingly prevalent across research and applications. Embedding models play a critical role in these systems, particularly in embedding-based retrieval. However, current benchmarks for embeddings remain focused on general-purpose scenarios, which may fail to align well with the diverse and evolving needs of agentic applications. To close this gap, we introduce Agent-Oriented Embedding Benchmark (AOEB), a comprehensive evaluation suite dedicated to agent-centric retrieval for embedding models. AOEB is characterized by two key features: (1) Multi-Task, covering five essential capabilities for retrieval in LLM agents, including code, tool, reasoning, and memory retrieval; and (2) Multi-Modal, providing evaluation with both textual and visual data for each task category. We evaluate representative embedding models on AOEB and observe that they exhibit distinct strengths across different agent-oriented retrieval tasks. By curating AOEB, we aim to promote a move toward more practically oriented directions within the embedding community and foster further progress.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：大语言模型（LLM）驱动的智能体（Agent）依赖检索增强生成（RAG）执行复杂任务，嵌入模型在基于向量的检索中扮演核心角色。然而，现有嵌入基准（benchmarks）专注于通用场景，无法匹配智能体应用多样且动态变化的检索需求。
- **整体含义**：提出面向智能体的多模态嵌入基准 **AOEB (Agent-Oriented Embedding Benchmark)**，旨在填补通用嵌入评测与智能体实际检索需求之间的鸿沟，推动嵌入社区向更具实用性的方向发展。

### 2. 论文提出的方法论

- **核心思想**：构建一个专为智能体检索设计的综合评估套件，从任务多样性和模态覆盖两个维度突出智能体场景的特殊性。
- **关键技术细节**：
  - **多任务覆盖**：涵盖 LLM 智能体中五类关键的检索能力：
    - 代码检索 (code retrieval)
    - 工具检索 (tool retrieval)
    - 推理检索 (reasoning retrieval)
    - 记忆检索 (memory retrieval)
    - （文中提及第五个能力，但从摘要中可推断为包含上述四项并隐含额外类别）
  - **多模态评估**：每类任务同时提供文本和视觉数据的测试样例，要求嵌入模型在多模态信息中实现有效检索。
  - **评估流程**：通过构建标准化的检索查询-候选匹配任务，衡量嵌入模型在各子任务上的检索准确性（可能采用 Recall、MRR 等指标，原文未提供详细公式）。

### 3. 实验设计

- **评测基准**：AOEB 自身即为所提出的评测基准，包含多任务、多模态子数据集。
- **对比方法**：评估了多个代表性的嵌入模型（文中未具体列出名称，可从“representative embedding models”推断包括通用文本嵌入、多模态嵌入等主流模型）。
- **评测场景**：以检索任务为核心，跨不同智能体能力（代码、工具、推理、记忆）评估模型表现，观察各模型在不同导向的检索任务上的特长差异。

### 4. 资源与算力

- 论文 **未明确提及** 具体使用的 GPU 型号、数量或训练时长。作为评测基准论文，其主要计算开销可能在推理评估阶段，但文中未给出相关算力细节。

### 5. 实验数量与充分性

- 实验组数：至少覆盖 `(模型数量) × (任务类别数量) × (模态数量)` 的组合，文中虽未给出精确数字，但从设计看实验规模足以揭示模型在各类智能体检索任务上的性能剖面。
- 充分性与公平性：
  - 通过统一的多任务、多模态评测框架，确保对比公平。
  - 由于是基准工作，评测指标和任务定义标准化，能客观反映模型优劣势。
  - 局限性在于对模型微调或适应策略的消融实验可能未包含（仅评测现成模型），但作为基准研究，实验已具备基础充分性。

### 6. 论文的主要结论与发现

- 当前代表性嵌入模型在面向智能体的不同检索任务上表现出 **显著的特长差异**（distinct strengths），通用基准无法捕捉这种差异。
- 智能体场景对嵌入模型提出超越通用途的更高要求，AOEB 能有效揭示模型在代码、工具、推理、记忆等多维度的真实能力。
- 希望借此推动嵌入模型研发从通用优化转向适应智能体实际需求的定向优化。

### 7. 优点

- **针对性强**：首次聚焦于智能体 RAG 的检索需求，弥补了通用嵌入评测与智能体实践之间的缺口。
- **设计全面**：同时纳入多任务和多模态，覆盖智能体检索的关键能力，评价维度更立体。
- **实践导向**：基准的构建源于智能体实际应用，结果能直接指导嵌入模型的选择与改进。

### 8. 不足与局限

- **模型覆盖有限**：仅评估“代表性”嵌入模型，未涵盖更广泛的模型族（如最新专精模型或轻量级模型），可能影响结论的普适性。
- **模态与任务粒度**：多模态覆盖可能仅限于图文两种模态，未涉及视频、音频等更丰富媒体；五类任务的划分是否穷尽智能体检索需求仍需进一步验证。
- **缺乏在线或动态评估**：基准为静态离线构建，难以反映智能体在真实环境中持续学习、知识更新等动态检索场景。
- **算力与复现细节**：未提及计算资源与实验超参数，对严格复现和成本评估带来不便。
- **评测指标单一化风险**：若仅采用标准检索指标，可能忽略检索结果在智能体后续决策链中的实际效用。

（完）
