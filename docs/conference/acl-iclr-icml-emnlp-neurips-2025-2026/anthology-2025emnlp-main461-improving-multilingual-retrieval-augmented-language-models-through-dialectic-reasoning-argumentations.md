---
title: Improving Multilingual Retrieval-Augmented Language Models through Dialectic Reasoning Argumentations
title_zh: 通过辩证推理论证改进多语言检索增强语言模型
authors: "Leonardo Ranaldi, Federico Ranaldi, Fabio Massimo Zanzotto, Barry Haddow, Alexandra Birch"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.461.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: Dialectic-RAG通过论证性解释系统评估检索信息
tldr: 针对多语言检索中检索信息可能包含矛盾知识的问题，提出Dialectic-RAG框架，通过结构化的辩证推理过程系统评估、比较和解决冲突视角，使RAG更具分析性和依据性。实验表明该方法能有效处理矛盾信息，提升多语言RAG的可靠性和推理能力。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.461/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1580, \"height\": 970, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.461/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 722, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.461/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1581, \"height\": 316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.461/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 745, \"height\": 446, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 849, \"height\": 993, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 751, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 822, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 839, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 697, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 848, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 834, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 433, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 472, \"height\": 606, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 812, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 777, \"height\": 518, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1541, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 854, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 842, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 810, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 841, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1652, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1653, \"height\": 175, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1617, \"height\": 724, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 515, \"height\": 691, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 774, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 781, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1298, \"height\": 547, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.461/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1657, \"height\": 487, \"label\": \"Table\"}]"
motivation: 多语言RAG面临检索到的知识相互矛盾的挑战，需要更分析性的推理方法。
method: 提出Dialectic-RAG，采用模块化的论证性解释，通过比较、对比和解决冲突视角来指导生成。
result: 实验表明该方法能提升多语言检索的准确性和一致性。
conclusion: 辩证推理能有效增强RAG系统处理矛盾知识的能力。
---

## Abstract
Retrieval-augmented generation (RAG) is key to improving large language models (LLMs) in systematically accessing richer factual knowledge. Yet, using RAG mechanisms brings intrinsic challenges, as LLMs must deal with conflicting knowledge, especially in multilingual retrieval, where the heterogeneity of knowledge retrieved may deliver different outlooks. To make RAG more analytical, critical and grounded, we introduce Dialectic-RAG ( D -RAG), a modular approach guided by Argumentative Explanations , i.e., structured reasoning process that systematically evaluates retrieved information by comparing, contrasting, and resolving conflicting perspectives. Given a query and a set of multilingual related documents, D -RAG selects and exemplifies relevant knowledge for delivering dialectic explanations that, by critically weighing opposing arguments and filtering extraneous content, clearly determine the final response. We show the impact of our framework both as an in-context learning strategy and for constructing demonstrations to instruct smaller models. Our experiments demonstrate that D -RAG significantly improves RAG approaches, requiring low-impact computational effort and providing robustness to knowledge perturbations.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：检索增强生成（RAG）虽能缓解大语言模型（LLM）的幻觉和知识缺口问题，但在多语言场景下，检索回的文档往往包含冲突、不相关或偏误信息，传统 RAG 缺乏对这些异构知识进行批判性评估和辩证整合的能力。
- **整体含义**：提出 **Dialectic‑RAG（D‑RAG）**，通过结构化的“论证性解释”（argumentative explanations）机制，迫使模型在多语言检索过程中系统性地比较、对比与裁决相互矛盾的视角，最终给出有据可依、鲁棒的答案，使 RAG 过程更具分析性与批判性。

### 2. 方法论
- **核心思想**：将辩证推理（dialectic reasoning）引入 RAG 流程，引导 LLM 按四个步骤处理检索到的多语言文档：
  1. **提取（Extraction）**：从给定的多语言文档中识别并提炼出回答查询所需的关键信息。
  2. **解释（Explanation）**：对每条提取的信息构建单条论证，明确其与查询的相关性，并引用原文。
  3. **辩证论证（Dialectic Argumentation）**：将上一步的所有论证整合为一个中立的、权衡多方论点与反驳的最终解释，阐明为何某些证据占优。
  4. **回答（Answer）**：基于上述推理输出简短、规范的最终答案。
- **关键技术细节**：
  - 整个推理过程通过自然语言指令一次性被要求，模型在单一 prompt 中依次产出 `#Extraction:`、`#Explanation:`、`#Dialectic Argumentation:` 和 `#Answer:` 段落。
  - D‑RAG 可以两种方式使用：
    - **上下文学习（ICL）**：直接作为提示模板指导大模型（如 GPT‑4o、Llama‑70B）进行推理。
    - **合成数据微调（SFT）**：利用高性能模型（如 GPT‑4o）生成带有完整推理轨迹的示范样本，再用这些样本微调较小模型（如 Llama‑8B/1B）。微调采用标准语言建模目标最大化期望对数似然。
- **形式化表述**：给定查询 \(q\) 和多语言文档集 \(D\)，目标是生成一个辩证论证 \(A\)，解释为何支持证据子集 \(D^+_q\) 比其余 \(D^-_q\) 更相关，并产出自然语言解释 \(E\)，即 \((q, D, L) \xrightarrow{\text{Dialectic-RAG}} (A, E)\)。

### 3. 实验设计
- **数据集与任务**：
  - **多语言知识密集型 QA**：MLQA（6 种语言）、MKQA（9 种语言）、XOR‑TyDi QA（6 种语言），共计 11 种不同语言。
  - **争议领土一致性测试**：BORDERLINES 数据集，包含英、X 国、Y 国三种语言的问题，用于评估模型在冲突证据下的答案一致性。
  - **英文基线**：Natural Questions（NQ）。
- **检索设置**：知识库为 Wikipedia，使用 Cohere 多语言嵌入模型检索 top‑5 相关文档（也验证了对其他检索系统如 BGE‑m3 的独立性）。
- **对比方法**：
  - 无 RAG 基线。
  - 标准 RAG（仅将检索文档附在提示中）。
  - D‑RAG‑ICL（大模型直接使用 D‑RAG 提示）。
  - D‑RAG‑SFT（使用 D‑RAG 生成示范样本微调小模型，并与标准 SFT 对比）。
  - 部分实验还与 Self‑RAG、C‑RAG 等方法对比。
- **评估指标**：灵活精确匹配准确率（flexible exact‑match），即在生成答案中包含标准答案即视为正确。

### 4. 资源与算力
- **推理**：GPT‑4o 通过 API 调用；开源模型（Llama 系列）使用 greedy decoding，温度=0。
- **微调**：
  - 硬件：4 块 NVIDIA RTX A6000（每块 48 GB 显存）。
  - 超参数：3 个 epoch，batch size=32，学习率 1e‑5，权重衰减 0.001，余弦学习率调度，warmup ratio 0.03。
- **数据标注**：使用 GPT‑4o 生成 D‑RAG 示范，并经过 exact‑match 正确性过滤与 GPT‑4o‑mini 二次质量检验。

### 5. 实验数量与充分性
- **实验覆盖面广**：涉及 4 种不同规模模型（从 1B 到 GPT‑4o）、3 大 QA 任务×多语言、1 个争议领土基准、以及独立英文基准。
- **消融与鲁棒性实验**：
  - 移除 D‑RAG 各步骤（Step 2、3、4），分析每步贡献。
  - 更改内部论证语言（中、阿、德等），观察性能变化。
  - 检索文档随机打乱、混入噪声文档，测试鲁棒性。
  - 训练样本数量缩放实验（50%~100% 训练数据），比较 D‑RAG‑SFT 与标准 SFT 的数据效率。
  - 检查模型对提示指令的遵循程度（IF）和语言一致性（CL）。
  - 验证对多种检索系统的独立性。
- **公平性与客观性**：所有对比均在同一检索结果、同一基座模型下进行；微调对比中，D‑RAG‑SFT 与标准 SFT 使用完全相同的基座、训练配置和底层模型，对比公平。

### 6. 主要结论与发现
- **大幅提升性能**：在 GPT‑4o 上，D‑RAG 相比无 RAG 平均准确率提升 **+51.6%**，相比标准 RAG 提升 **+12.9%**。
- **有效赋能小模型**：用 D‑RAG 示范微调 Llama3‑8B，相较标准 RAG 提升 **+9.6%**，相较标准 SFT 提升 **+5.5%**。
- **处理冲突知识**：在 BORDERLINES 基准上，D‑RAG 将 GPT‑4o 的多语言答案一致性从 RAG 的 81.6% 提升至 **100%**。
- **鲁棒性突出**：在检索结果被随机打乱或混入无关噪声时，D‑RAG 的性能下降幅度显著小于标准 RAG，具备更强的抗干扰能力。
- **组件重要性**：步骤 2（解释）和步骤 3（辩证论证）对最终性能贡献最大，移除后平均准确率分别下降 5.2% 和 6.5%。

### 7. 优点
- **结构化推理**：首次将辩证逻辑显式融入多语言 RAG 的生成过程，使答案有迹可循、可解释。
- **轻量级与即插即用**：无需修改模型架构或检索器，仅通过提示或微调即可实现，计算开销低。
- **跨模型迁移能力强**：既能直接增强大模型，又能作为高质量数据合成策略将推理能力蒸馏到小模型。
- **鲁棒性与实用性**：对检索噪声、文档顺序不敏感，适合真实世界中质量波动较大的多语言知识源。

### 8. 不足与局限
- **小模型直接 ICL 效果不稳定**：Llama3‑8B 和 1B 在直接使用 D‑RAG 提示时性能反而下降，必须借助微调才能获益，说明深层推理能力需要额外训练支撑。
- **论证语言受限**：内部推理要求使用英语，若切换至其他语言会导致准确率下降，可能限制其在非英语逻辑链中的应用。
- **语言覆盖与评估范围**：实验仅覆盖 11 种语言，且多为中高资源语种，对极低资源语言（如 Telugu、Hindi 等）效果不够突出，更广泛的跨语言泛化性有待验证。
- **依赖上游检索质量**：虽然对噪声鲁棒，但若检索结果整体偏离问题，辩证推理也无法凭空产生正确答案。
- **数据集偏差风险**：使用 Wikipedia 作为知识源，可能携带西方中心或特定语言版本文档的不平衡，影响某些文化敏感问题的公平性。

（完）
