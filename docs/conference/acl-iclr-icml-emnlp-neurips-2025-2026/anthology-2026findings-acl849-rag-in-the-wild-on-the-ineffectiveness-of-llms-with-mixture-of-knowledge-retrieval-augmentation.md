---
title: "RAG in the Wild: On the (In)effectiveness of LLMs with Mixture-of-Knowledge Retrieval Augmentation"
title_zh: 野外RAG：大语言模型在混合知识检索增强中的（无效）有效性
authors: "Ran Xu, Yuchen Zhuang, Yue Yu, Haoyu Wang, Wenqi Shi, Carl Yang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.849.pdf"
tags: ["query:agentic-rag"]
score: 4.0
evidence: 大规模混合知识RAG评测揭示局限性并指出需自适应检索
tldr: 探索了从异构知识源检索增强的现实效果，通过大规模实验发现：检索仅对小模型提升明显，重排序器作用有限，且现有模型无法有效路由至混合来源。揭示了当前RAG在开放环境下的关键挑战，为设计自适应检索和混合知识路由提供了重要洞察。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.849/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1632, \"height\": 769, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.849/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1622, \"height\": 765, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.849/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1604, \"height\": 753, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.849/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1649, \"height\": 393, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 761, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 804, \"height\": 729, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1637, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1637, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1646, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1634, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1636, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1640, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1635, \"height\": 382, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1638, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1637, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1636, \"height\": 387, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1636, \"height\": 379, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.849/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1637, \"height\": 386, \"label\": \"Table\"}]"
motivation: 现有RAG评测多限于单一领域知识源，真实混合知识条件下的表现尚不明确。
method: 构建大规模混合知识数据存储，从多角度评估不同模型与检索器组合的RAG性能。
result: 检索增益集中于小模型，重排序和单一知识源无法保证稳定提升，跨源路由困难。
conclusion: 工作指出了现实RAG应用亟需自适应检索机制，为后续鲁棒RAG设计指明了方向。
---

## Abstract
Retrieval-augmented generation (RAG) enhances large language models (LLMs) by integrating external knowledge retrieved at inference time. While RAG demonstrates strong performance on benchmarks largely derived from general-domain corpora like Wikipedia, its effectiveness under realistic, diverse retrieval scenarios remains underexplored. We evaluate RAG systems using MassiveDS, a large-scale datastore with mixture of knowledge, and identified critical limitations: retrieval mainly benefits smaller models, rerankers add minimal value, and no single retrieval source consistently excels. Moreover, current LLMs struggle to route queries across heterogeneous knowledge sources. These findings highlight the need for adaptive retrieval strategies before deploying RAG in real-world settings.

---

## 论文详细总结（自动生成）

好的，以下是对这篇论文的结构化深度总结。

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前检索增强生成（RAG）系统的评测大多基于通用领域语料（如 Wikipedia），其在现实世界中异构、混合知识源下的真实有效性尚未得到充分探究。
- **研究背景**：
    - 现有 RAG 基准多构造自 Wikipedia 等单一来源，查询与语料高度对齐，难以反映真实场景中的噪声、领域错配等挑战。
    - 真实检索场景面临多源、多域知识混合的现实，亟需系统评估 RAG 在这种“混合知识”环境下的泛化能力。
- **整体含义**：本研究旨在揭示当前 RAG 系统部署至开放、多领域场景时存在的关键局限，并为未来自适应、鲁棒的检索增强技术提供实证依据。

## 2. 论文提出的方法论

- 论文本身并未提出新模型或算法，而是构建了一套**系统的多维度实证分析框架**，核心思想是：从混合知识源（Mixture of Knowledge）出发，综合评测 RAG 管线的各个环节。
- **关键技术环节**：
    - **知识存储与检索**：使用 MassiveDS（一个含 1.4T 词元、涵盖 PubMed、Wikipedia、Github、Arxiv 等 10 种来源的大规模混合数据存储）。默认检索器为 `bge-base-en-v1.5`，每次检索 top‑k = 5 个相关段落。
    - **重排序（Reranking）**：先检索 top‑k’ = 30 个段落，再通过 `bge-reranker-v2-m3` 重排序并选取最相关的 5 个段落，以考察检索质量上限的影响。
    - **查询路由（Routing）**：让 LLM 本身作为路由器，根据查询内容从多源中选择最合适的检索源，使用普通提示和思维链（CoT）提示两种方式。
- **评估指标**：
    - 选择题：准确率（Accuracy）。
    - 短答案生成：精确匹配（Exact Match）。
    - 检索增益：相对收益 Δ = (ps − ρ) / ρ，其中 ps 为使用源 s 的 RAG 性能，ρ 为无检索基线性能。

## 3. 实验设计：数据集、基准与对比方法

- **数据集（6 个）**：
    - 通用知识 QA：MMLU、MMLU‑Pro。
    - 科学 QA：ARC‑Challenge、SciQ、CSBench（计算机科学）。
    - 事实性 QA：SimpleQA（已去除基于 Wikipedia 创建的题目）。
- **骨干模型（7 个系列）**：Llama‑3.2‑3B、Llama‑3.1‑8B、Qwen3‑4B/8B/32B、GPT‑4o‑mini、GPT‑4o（均使用指令微调版本）。
- **检索来源对比**：
    - 无检索基线（纯模型生成）。
    - 10 种单一知识源（PubMed、Wikipedia、Pes2o、C4、Github、Math、StackExchange、Book、Arxiv、CommonCrawl）。
    - 所有源混合（All）。
- **RAG 变体对比**：
    - 仅检索（Retrieve then Generate）。
    - 检索 + 重排序（Retrieve + Rerank）。
    - LLM 作为路由器（Plain & CoT 路由）与静态全源检索、Oracle 路由上限进行对比。
- **所有实验均为零样本设定**，以保证公平性。

## 4. 资源与算力

- 文中**未明确说明**所使用的 GPU 型号、数量、具体推理时长或训练开销。
- 鉴于实验以现成模型的推理评测为主，且使用了 MassiveDS 的预构建索引，可以推断主要算力消耗在大量模型、多数据集的检索与生成推理上，但具体的算力规模无法从原文得知。

## 5. 实验数量与充分性

- **实验规模极大**：覆盖 7 个模型 × 6 个数据集 ×（10 种单独源 + 全源 + 重排序变体 + 路由策略），图1–图4 及附录中多个详细表格展示了海量的实验组合。
- **多维度分析**：
    - 研究问题 1：整体 RAG 有效性及模型规模影响（含领域细粒度分析，如 STEM、社会科学）。
    - 研究问题 2：实例级分析不同检索源的独有收益。
    - 研究问题 3：重排序对最终性能的影响。
    - 研究问题 4：LLM 作为跨源路由器的可行性。
- **客观性与公平性**：所有对比基于统一的零样本提示模板，检索过程使用相同的文档过滤和去重，多种模型和来源的对比设计较为全面，可视为一次客观、公平的大规模基准评估。

## 6. 论文的主要结论与发现

- **检索增益随模型增大急剧衰减**：在混合知识源下，检索仅为较小模型（如 3B、8B）带来显著提升（可达 20%+），对于 32B 及 GPT‑4 级别模型，提升微乎其微甚至为负，仅事实性 QA（如 SimpleQA）能保持少量正向增益。
- **重排序无法根除性能瓶颈**：增加重排序阶段后性能提升依然有限，说明问题不在于检索排序能力不足，而是检索系统根本未能召回包含答案的段落，或检索与生成的集成方式存在更深层的失配。
- **不存在单一普适的最佳检索源**：实例级分析显示，有 8%–39% 的查询仅能被某个特定语料库所解答，没有任何一个源能始终表现最优。
- **LLM 难以胜任跨源路由任务**：使用提示驱动的路由策略（包括思维链）均未能稳定超越静态的“全源检索”基线，有时甚至不如无检索基线，表明当前 LLM 缺乏准确评估信息所需来源的能力。

## 7. 优点：方法或实验设计上的亮点

- **现实性高**：使用 MassiveDS 这一 1.4T 词元的异构混合知识存储，比仅用 Wikipedia 的评测更贴近真实 RAG 部署环境。
- **系统性极强**：同时考察了模型规模、检索源多样性、重排序、查询路由等多个维度，分析层次丰富。
- **提供可操作的洞察**：明确指出简单扩大模型、优化排序或提示式路由不能解决核心问题，为后续“自适应检索”和“检索‑生成深度集成”指明了方向。
- **实验对照严密**：包含无检索、单源、全源、重排序、路由及 Oracle 上限，多级对比结果说服力强。

## 8. 不足与局限

- **任务类型单一**：仅评估了短答案 QA（选择题和短文本生成），未涉及长文本生成、多跳推理或开放式对话等更复杂的 RAG 应用场景。
- **模型覆盖面不全**：受限于算力，未纳入更大的开源模型（如 DeepSeek‑V3、Llama‑4）及其他检索范式（如基于 agent 的迭代检索），结论的普适性有待扩展。
- **路由评测过于简单**：仅使用提示方式调用 LLM 做源选择，缺少针对性的路由训练模块，可能低估了潜在路由性能。
- **缺乏效率分析**：完全没有讨论检索、重排序、路由等环节的延迟与计算开销，而这些正是现实部署的关键约束。
- **可能存在源选择偏差**：尽管 MassiveDS 覆盖面广，但各源规模、质量差异可能影响公平性，且路由实验平台仅限于 Qwen‑3 系列，结论可推广性受限。

（完）
