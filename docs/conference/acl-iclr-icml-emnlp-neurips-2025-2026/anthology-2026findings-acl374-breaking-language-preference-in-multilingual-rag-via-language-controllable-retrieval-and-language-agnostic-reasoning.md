---
title: Breaking Language Preference in Multilingual RAG via Language-Controllable Retrieval and Language-Agnostic Reasoning
title_zh: 打破语言偏好：通过语言可控检索与语言无关推理实现多语言RAG
authors: "Wenshuai Huo, Xiaocheng Feng (冯骁骋), Baohang Li, Chengpeng Fu, Yichong Huang, Hui Wang, Bing Qin (秦兵)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.374.pdf"
tags: ["query:agentic-rag"]
score: 7.0
evidence: 语言无关推理使RAG能基于语义而非表面语言形式进行推理
tldr: 针对多语言RAG中检索语言敏感和生成模型受语言形式影响的偏好问题，提出语言可控检索与语言无关推理方法。通过解耦语言形式与语义检索，并训练模型忽略表层语言差异直接基于语义推理，在多种语言上实现一致的检索精度和生成质量。实验证明该方法有效消除了语言偏好，提升了多语言RAG的鲁棒性与跨语言迁移能力。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.374/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 626, \"height\": 997, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.374/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1391, \"height\": 727, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.374/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 788, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.374/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 599, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.374/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1653, \"height\": 556, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.374/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1566, \"height\": 774, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.374/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1057, \"height\": 486, \"label\": \"Table\"}]"
motivation: 多语言RAG中检索结果因查询语言不同而差异大，且生成模型易受文档语言形式干扰而非基于语义推理。
method: 提出语言可控检索以分离语言形式与语义，以及语言无关推理迫使模型忽略语言表层差异。
result: 在多种语言上取得一致的检索与生成表现，消除了语言偏好导致的性能波动。
conclusion: 该方法从检索和推理两端保障了多语言RAG的公平性与准确性，可广泛应用于跨语言知识问答。
---

## Abstract
Retrieval-Augmented Generation (RAG) significantly improves the factual accuracy and generation quality of large language models by incorporating external knowledge. However, in multilingual settings, RAG systems suffer from severe language preference. On the one hand, the retrieval stage is sensitive to the query language: semantically equivalent queries expressed in different languages often lead to substantially different retrieval results. On the other hand, when retrieved documents contain knowledge written in multiple languages, large language models tend to be influenced by surface-level language forms, rather than reasoning solely based on semantic relevance to the query.To address these challenges, we propose a unified optimization framework that explicitly disentangles multilingual RAG into language-controllable retrieval and language-agnostic reasoning. Our framework allows LLM to adaptively select retrieval languages while enforcing cross-lingual consistency during reasoning, thereby mitigating language bias without modifying existing retrievers or translators. Experimental results demonstrate that our approach effectively reduces language bias in multilingual RAG and consistently outperforms baselines across multiple multilingual benchmarks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题**：在多语言检索增强生成（mRAG）中，系统存在严重的“语言偏好”（language preference），导致性能下降。
- **具体表现**：
  - **检索阶段**：语义相同但语言不同的查询，获取到的文档集合差异很大，低资源语言检索效果更差。
  - **生成阶段**：大语言模型倾向于被文档的表层语言形式影响，而非纯粹基于语义相关性进行推理，即使文档包含关键证据，也可能因语言而被忽略。
- **动机**：现有方法主要依赖启发式翻译策略（如查询翻译为英语、文档统一翻译后再生成），但这些静态方案缺乏灵活性，难以适应多样化的语言分布。

### 2. 论文提出的方法论

- **核心思想**：将多语言 RAG 显式解耦为“语言可控检索”（language-controllable retrieval）和“语言无关推理”（language-agnostic reasoning），通过强化学习对这两个阶段分别优化。
- **关键技术细节**：
  - **语言可控检索**：
    - 模型根据输入查询`q`，自行选择一个检索语言`ℓr`（从候选语言集合`L`中）。
    - 若需要，利用翻译工具将查询转换为`ℓr`，然后交由固定检索器从同一多语言语料库获取 top-k 文档。
    - 奖励信号`rLcR`基于检索结果是否包含正确答案（或答案的多语言翻译），引导模型选择更可能命中相关证据的语言。
  - **语言无关推理**：
    - 对检索到的文档集`D`，分别基于原始文档和经翻译统一语言后的文档`˜D`，让模型给出相关性排序`πorig`和`πtrans`。
    - 通过 Rank-Biased Overlap (RBO) 衡量两个排序的一致性，作为语言无关排序奖励`rLaR`，促使模型仅关注语义而非语言形式。
    - 结合任务准确率奖励`racc`（答案是否与参考答案精确匹配），通过 PPO 优化生成器参数。
- **框架特点**：生成器是唯一可学习组件，检索器和翻译工具保持冻结，无需修改现有系统。

### 3. 实验设计

- **数据集与场景**：
  - `MKQA`：包含约10,000条/语言的多语言开放域问答数据，筛选无答案实例后，每语言取500条测试，其余训练。覆盖13种语言：阿拉伯语、德语、英语、西班牙语、芬兰语、法语、意大利语、日语、韩语、葡萄牙语、俄语、泰语、中文。
  - `XOR-TyDi`：多语言问答数据集，用于评估领域外泛化能力，包含训练中未见的孟加拉语和泰卢固语。
- **基准模型（Baselines）**：
  - `MRAG`：直接多语言检索与生成。
  - `TRANS_RAG`：查询翻译为英语后再检索。
  - `DOC_TRANS`：保留原始查询检索，但文档翻译为英语后生成。
  - `DKM-RAG`：检索后文档翻译成查询语言，并用 LLM 重写精炼。
- **主要组件**：骨干模型为 LLaMA-3.2-8B-Instruct 和 Qwen2.5-7B-Instruct；检索器为 BGE-M3，重排序器 bge-reranker-v2-m3；翻译工具为 NLLB-3.3B；质量评估模型过滤低置信翻译。

### 4. 资源与算力

- 文中明确提及：所有实验在 **8 块 NVIDIA A100 GPU** 上运行，总批次大小为 512。最大序列长度设为 4096 tokens。  
- 未提及具体训练时长，但给出了训练配置（如 PPO 强化学习框架、批次大小等），能为复现提供参考。

### 5. 实验数量与充分性

- **总体实验组数**：
  - 2 个骨干模型 × 2 个数据集（MKQA 主实验，XOR-TyDi 泛化实验），共 4 组大规模对比实验。
  - 在 MKQA 上对比了 4 个 baseline，涵盖 13 种语言。
  - 消融实验：逐步去除奖励项（仅准确率奖励、加入语言无关推理奖励、再加入语言可控检索奖励），评估各组件贡献。
  - 单独分析检索语言选择效果、案例研究、领域外泛化。
- **充分性与公平性**：
  - 基准选择全面，涵盖查询翻译、文档翻译等典型 mRAG 策略，且各方法使用相同的骨干模型、检索器和翻译工具，比较公平。
  - 消融实验清晰展示了各奖励信号的作用，验证了提出的核心组件有效。
  - 跨数据集评估（MKQA 与 XOR-TyDi）检验了方法的泛化性。
  - 总体实验设计充分，能够支撑结论。

### 6. 论文的主要结论与发现

- 所提方法在 MKQA 和 XOR-TyDi 上几乎对所有语言均取得一致提升，低资源语言的增益尤其显著。
- 语言可控检索帮助模型自主选择更合适的检索语言，提高文档召回率；语言无关推理使模型聚焦语义，减少语言形式的干扰。
- 强化学习框架结合下游任务反馈，比静态翻译策略更灵活，能够平衡检索和推理中的语言偏好。
- 方法展现出良好的跨域泛化能力，对训练中未见的语言也能带来明显提升。

### 7. 优点

- **问题解耦清晰**：将 mRAG 分为两个阶段并针对性优化，思路直观。
- **端到端优化**：直接以任务准确率和排序一致性为信号，无需设计复杂的启发式规则。
- **兼容性强**：不改动现有检索器和翻译工具，易于与现有流水线集成。
- **实验扎实**：覆盖多语言、多模型、多基线，且包含消融和泛化分析，结论可信。
- **关注低资源语言**：显著缓解了低资源场景下的性能瓶颈。

### 8. 不足与局限

- **推理延迟增加**：推理时需额外步骤确定检索语言，带来计算开销。
- **依赖翻译质量**：方法效果受翻译工具性能制约，翻译错误可能引入噪声。
- **训练成本**：虽然推理时主要额外开销是语言选择，但训练阶段需强化学习与多次翻译，算力需求较高。
- **规模局限**：实验限定在 7B-8B 参数模型，更大规模模型上的表现未验证。
- **语种覆盖**：虽包含多种语言，但依然有限，对真正的极低资源语言或非拉丁文字系统未做验证。
- **翻译工具固定**：使用单一翻译系统（NLLB），未考察翻译工具的鲁棒性影响。

（完）
