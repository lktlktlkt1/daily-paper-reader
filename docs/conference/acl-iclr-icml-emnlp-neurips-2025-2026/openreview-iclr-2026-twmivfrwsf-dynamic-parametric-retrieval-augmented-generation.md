---
title: Dynamic Parametric Retrieval Augmented Generation
title_zh: 动态参数化检索增强生成
authors: "Yuqiao Tan, Shizhu He, Huanxuan Liao, Tian Liang, Jun Zhao, Kang Liu"
date: 2025-09-13
pdf: "https://openreview.net/pdf?id=TWMiVfRwSF"
tags: ["query:agentic-rag"]
score: 6.0
evidence: 引入动态参数化RAG以提升检索效率和泛化性
tldr: 检索增强生成（RAG）通过注入外部文档增强语言模型，但大幅增加推理成本并引发知识冲突。参数化RAG（PRAG）虽通过离线训练将文档嵌入参数来缓解，却面临高训练存储开销和泛化困难。本文提出动态参数化RAG（DyPRAG），在推理时动态将所需文档转换为参数，克服静态嵌入局限。实验表明，DyPRAG在维持生成质量的同时降低推理成本，并有效减少知识冲突。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 传统RAG推理成本高且存在知识冲突，参数化RAG又难以泛化到新文档。
method: 提出动态参数化RAG (DyPRAG)，推理时动态嵌入文档参数，降低开销并提升泛化。
result: 实验表明DyPRAG可减少推理成本与知识冲突，同时保持生成质量。
conclusion: DyPRAG为高效、可扩展的RAG提供了动态参数化解决方案。
---

## Abstract
Retrieval-augmented generation (RAG) enhances large language models (LLMs) by injecting externally retrieved documents into the input context. It significantly increases inference costs and introduces knowledge conflicts, primarily caused by the lack of corresponding parametric knowledge in LLMs. Recently, Parametric RAG (PRAG) proposed to overcome these limitations by embedding symbolic documents into LLMs parameters, effectively reducing the inference costs and conflicts through offline training. However, PRAG needs to convert all documents into parameters in advance, which incurs high training and storage costs and renders it difficult to generalize to unseen documents. To address these challenges, we propose Dynamic Parametric RAG (DyPRAG), a novel framework that leverages a lightweight parameter translator model to efficiently convert symbolic documents into parametric knowledge online. Specifically, the parameter translator employs several linear layers to convert document embeddings into LoRA modules of feed-forward networks of LLMs directly. DyPRAG achieves test-time parametric knowledge enhancement by dynamically generating the requisite parameters, which not only reduces the inference cost and mitigates knowledge conflicts inherent in RAG, but also lowers the training and storage overhead of PRAG. Extensive experiments on multiple datasets demonstrate the effectiveness and generalization capabilities of DyPRAG. Furthermore, the combination of contextual knowledge with test-time generated parametric knowledge offers a practical and more powerful RAG paradigm which updates parametric knowledge adaptively, enables superior knowledge fusion and alleviates knowledge conflicts in real-world applications. Our code is available at https://anonymous.4open.science/r/DyPRAG_ICLR.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究动机**：检索增强生成（RAG）虽能通过外部文档提升大语言模型（LLM）的表现，但会急剧增加推理成本，并因 LLM 缺少对应参数化知识而引发知识冲突。
- **现有方法局限**：参数化 RAG（PRAG）通过离线训练将文档嵌入模型参数，虽可降低推理成本与冲突，但需预先转换全部文档，导致极高的训练与存储开销，且难以泛化到未见文档。
- **本文目标**：提出 **动态参数化 RAG（DyPRAG）**，在推理阶段在线将文档动态转换为参数化知识，既保留 PRAG 的优势，又克服其高昂开销与泛化困难。

## 2. 论文提出的方法论
- **核心思想**：利用一个轻量的**参数翻译器（parameter translator）**，在测试时将符号化文档实时转化为 LLM 前馈网络（FFN）层的 LoRA 模块参数，实现“即需即生成”的参数增强。
- **关键技术细节**：
  - 参数翻译器由若干线性层组成，其输入是文档的嵌入向量，输出直接对应 LLM 中 FFN 层的 LoRA 权重（包含降维、升维矩阵等）。
  - 推理时，对检索到的文档，先将其编码为嵌入，再由翻译器生成 LoRA 参数，动态注入 LLM，无需提前训练所有文档。
- **算法流程（文字描述）**：
  1. 用户查询到达，检索出相关文档。
  2. 将文档通过嵌入编码器转为向量表示。
  3. 参数翻译器（轻量网络）将文档向量映射为一组 LoRA 参数。
  4. 将生成的 LoRA 参数附加到 LLM 的指定 FFN 层上。
  5. LLM 结合上下文与动态参数化知识生成回答。

## 3. 实验设计
- 摘要中提到实验在**多个数据集**上进行，但未列出具体名称。推断可能涵盖开放域问答、知识密集型任务等。
- **基准对比方法**：隐含与传统 RAG（上下文注入）和离线 PRAG 进行对比。
- **验证维度**：生成质量、推理成本、知识冲突程度、训练/存储开销，以及结合上下文与参数化知识的联合范式。

## 4. 资源与算力
- 论文摘要**未明确说明**所使用的 GPU 型号、数量或训练时长。仅提到代码开源仓库，但未提供硬件配置等细节。

## 5. 实验数量与充分性
- 摘要宣称进行了“大量实验”（extensive experiments），并覆盖多数据集，以验证效果和泛化能力。但未给出具体实验组数、消融实验、统计显著性等信息。
- 从现有描述看，实验可能包含：
  - 不同数据集上的整体性能比较。
  - 推理成本与知识冲突的量化分析。
  - 对未见文档的泛化测试。
  - 结合上下文与参数化知识的混合方案评估。
- 由于缺少详细实验列表，**充分性无法完全评估**，但声明符合全面评估的常见模式。

## 6. 论文的主要结论与发现
- DyPRAG 在保持生成质量的同时，能够显著**降低推理成本**并**缓解知识冲突**。
- 与离线 PRAG 相比，大幅**减少了训练和存储开销**，且能有效**泛化到新文档**。
- 测试时动态生成的参数化知识与上下文知识相结合，可形成一种更强大、更实用的 RAG 范式，实现自适应知识更新、更优的知识融合以及冲突缓解。

## 7. 优点
- **创新性强**：首次提出动态在线生成文档参数，打破离线转换的僵化模式。
- **效率与泛化兼顾**：利用轻量翻译器避免全量文档预训练，降低存储负担，同时保留对未见文档的适应能力。
- **实用价值高**：动态参数增强可天然嵌入实际应用，实现按需知识注入，减少延迟和算力浪费。
- **兼容现有架构**：使用 LoRA 方式干预 FFN，可与主流 LLM 直接结合，无需改动模型主体。

## 8. 不足与局限
- 摘要中**未提及方法本身的局限性**，从原理推测可能存在：
  - 参数翻译器的质量可能高度依赖文档嵌入的表示能力，若嵌入表达不足或文档长度差异大，生成的 LoRA 参数可能次优。
  - 推理时需额外执行检索与翻译步骤，其计算开销是否完全低于传统 RAG 需更细致的剖析（摘要虽声称减少开销，但未给出绝对数值）。
  - 若检索返回多篇文档，如何高效融合多个动态生成的参数模块尚无讨论。
  - 实验部分未公开具体数据集与基线细节，无法验证结论的普遍性及公平性。
- 此外，论文仅提供摘要信息，完整的实验覆盖、消融分析、偏差风险及应用限制有待全文揭示。

（完）
