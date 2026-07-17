---
title: "UniRAG: Unified Query Understanding Method for Retrieval Augmented Generation"
title_zh: UniRAG：面向检索增强生成的统一查询理解方法
authors: "Rui Li, Liyang He, Qi Liu, Zheng Zhang, Heng Yu, Yuyang Ye, Linbo Zhu, Yu Su"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.693.pdf"
tags: ["query:agentic-rag"]
score: 6.0
evidence: 统一查询理解框架提升复杂查询下的RAG性能
tldr: 针对RAG中查询增强与编码任务割裂导致的误差累积和策略选择困难，提出统一查询理解框架UniRAG。用一个解码器式大模型同步完成查询增强与编码，消除信息共享障碍，并自适应选择最优增强策略。实验表明其在复杂查询下的检索准确率和回答质量均有明显提升。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.693/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1644, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.693/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1658, \"height\": 528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.693/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1644, \"height\": 506, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.693/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 786, \"height\": 376, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1600, \"height\": 794, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 416, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 827, \"height\": 168, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 759, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 366, \"label\": \"Table\"}]"
motivation: 现有查询增强与编码分离降低信息共享，且难以在不同场景下选择最佳增强策略。
method: 采用单一解码器语言模型联合执行查询增强和编码，并通过自适应机制实现动态策略选择。
result: 在复杂查询任务上检索与生成指标均显著优于分离式基线。
conclusion: UniRAG简化了RAG查询处理管线，以统一架构有效处理多样查询类型，提升了RAG系统的鲁棒性。
---

## Abstract
Retrieval-Augmented Generation (RAG) technology effectively addresses the issues of knowledge update lag and hallucinations in large language models (LLMs) by integrating internal and external knowledge. Existing query augmentation methods improve RAG’s performance in handling complex queries but face two key challenges: (1) the separation of query augmentation and encoding tasks, which hinders information sharing and introduces cumulative errors, and (2) the difficulty of selecting the optimal augmentation strategy for different scenarios. In this work, we propose UniRAG, a unified framework for query understanding in RAG. UniRAG employs a decoder-only LLM to jointly perform query augmentation and encoding, eliminating task separation. To facilitate adaptive query augmentation, we categorize existing techniques into query paraphrasing, query expansion, and query abstraction. Our model learns to select the optimal augmentation strategy based on user queries, leveraging retrieval and generation outputs as feedback. Experimental results show that UniRAG significantly outperforms traditional query augmentation methods in five knowledge-intensive benchmark tasks in both closed and open domain question answering.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义
这篇论文聚焦于检索增强生成（RAG）系统中的**查询理解**环节。现有RAG方法虽然通过引入外部知识缓解了大语言模型的幻觉和知识滞后问题，但在处理复杂查询时面临两个核心瓶颈：
- **任务割裂**：查询增强与查询编码通常作为独立阶段/模型处理，阻碍信息共享并可能累积误差。
- **策略选择困难**：不同增强技术（如改写、扩展、抽象）在不同场景下表现各异，缺乏一种自适应选择最优策略的机制。

针对上述问题，论文提出 **UniRAG**，一个统一的查询理解框架，旨在用一个解码器式大语言模型（decoder-only LLM）**同步完成查询增强与编码**，并**自主决定最适合当前查询的增强策略**，从而提升RAG系统在知识密集型任务中的整体性能。

### 方法论
UniRAG 的核心是将查询增强（Query Augmentation）和查询编码（Query Encoding）统一到一个模型中，并通过反馈学习实现自适应策略选择。其训练分为两个阶段：

**1. 查询增强训练**
- **数据合成**：将现有增强技术归类为三类，并为每类选取一个代表性方法：
    - **查询改写**：消除歧义和模糊表达。
    - **查询扩展**：使用HyDE生成假设性文档。
    - **查询抽象**：使用Step-Back Prompting生成更通用的抽象问题。
- **反馈信号收集**：使用GPT-4o-mini对种子查询生成增强查询，然后采集两类反馈分数：
    - **检索器反馈** (`s_ret`)：正相关文档的倒数排名（`1/rank`）。
    - **生成器反馈** (`s_gen`)：给定检索文档后，生成正确答案的对数概率（`log p(r∣C(x))`）。
- **数据过滤**：只保留增强查询反馈分数高于原始查询的样本，同时保留原始查询本身作为“无需增强”的样本。
- **训练目标**：联合训练损失 `L_enh = L_sel + L_gen`。
    - `L_sel`：在动作令牌（`<Paraphrase>`、`<Expand>`、`<Abstract>`、`<Original>`）位置，计算模型预测的概率分布与反馈分数软分布之间的KL散度，让模型学会根据查询选择策略。
    - `L_gen`：标准的下一个令牌预测损失，监督模型生成对应策略的增强查询文本。

**2. 查询编码训练**
- **数据构建**：将原始查询、选中的增强策略和生成的增强查询，与一个预设的指令模板结合，形成用于检索训练的新查询 `q_inst`。同时加入未增强的原始数据，并挖掘难负样本。
- **训练目标**：采用对比学习中的InfoNCE损失 (`L_ret`)，在查询和文档末尾添加`<EOS>`令牌，取最后一层的`<EOS>`向量作为嵌入，拉近正查询-文档对，推远负样本对。

**推理阶段**
- **默认解码**：直接选择概率最高的动作令牌，并贪婪生成增强查询。
- **阈值解码**：当`<Original>`令牌概率与最高增强动作令牌概率之比低于阈值`γ`时，才进行增强，以灵活控制计算成本。
- **树解码**：在高预算场景下，探索所有概率不低于`<Original>`的增强策略，并使用束搜索生成多个增强查询，最后通过倒数排名融合多路检索结果。

### 实验设计
论文在五个知识密集型基准任务上进行了全面验证，覆盖封闭式和开放式问答场景，并使用准确率作为评估指标。
- **数据集**：
    - **封闭式QA**：PubHealth（公共卫生事实核查）、ARC-Challenge（科学推理多选题）。
    - **开放式QA**：PopQA（长尾实体知识）、TriviaQA-unfiltered、TimeQA（时间敏感知识）。
- **基准方法（Baselines）**：
    - **无检索**：零样本提示作为下限。
    - **原始查询**：直接使用未增强的查询进行检索。
    - **单独增强方法**：查询改写、HyDE、Step-Back Prompting分别作为独立的增强阶段。
- **生成器与检索器**：
    - **生成器**：为验证模型无关性，选用了三种大模型：**Llama-3-8B-Instruct**、**Llama-3-70B-Instruct** 和 **GPT-4o-mini**。
    - **检索器**：统一使用 **Contriever-MS MARCO** 作为稠密检索器，检索外部维基百科语料。

### 资源与算力
- **训练数据合成**：使用 **GPT-4o-mini** 对种子数据（来自NQ、MS MARCO等6个数据集）进行增强，最终收集了约26.3万条指令微调样本，其中包含约10.5万条有效反馈信号。
- **训练基座模型**：**Llama-3.1-8B**。
- **训练硬件**：训练使用了 **4块 80GB 显存的 NVIDIA A100 GPU**。
- **训练策略与时间**：
    - 查询增强阶段：指令微调3个epoch，批次大小256，学习率2e-5。
    - 查询编码阶段：使用LoRA（秩16）微调1个 epoch，温度参数τ=0.01。
    - 文中未明确报告总训练时长，但提及采用了DeepSpeed ZeRO-3、梯度检查点和FlashAttention2等显存和加速优化技术。

### 实验数量与充分性
- **主实验**：在5个数据集、3种不同规模的生成器上对比了UniRAG与3种单独增强方法及2个参考基线，共计5×5=25组主实验设置。
- **消融实验**：在3个代表性数据集（PopQA, PubHealth, ARC-Challenge）上，针对查询增强和编码阶段进行了深入的模块消融，共计7组实验。
    - **增强阶段消融**：移除检索器反馈、移除生成器反馈、将软反馈损失替换为拒绝采样。
    - **编码阶段消融**：替换为独立检索器Contriever、跳过增强阶段训练、仅用原始数据训练。
- **分析性实验**：还进行了策略选择准确率分析、不同推理策略的延迟与性能权衡分析，以及合成数据规模对性能影响的扩展性分析。

这些实验设计覆盖了模型的核心组件、推理策略和数据规模效应，对比全面，消融细致，能够充分验证方法的有效性和各组件的作用，具备较高的客观性与公平性。

### 主要结论与发现
- **性能一致领先**：UniRAG在所有数据集和生成器上，性能均**显著优于**任何单一固定的查询增强方法。特别地，在单独增强方法本身就能带来较大提升的数据集上，UniRAG的提升更为明显。
- **统一框架优势明显**：通过消融实验证实，将查询增强和编码统一在单一模型中训练，优于使用独立检索器（如Contriever）或跳过增强阶段，验证了信息共享和联合优化能有效减少累积误差。
- **自适应策略选择有效**：UniRAG的增强策略在超过90%的案例中带来了性能提升，并且其胜率（Win Rate）高于其他所有单独增强方法，证明模型能够准确判断并应用合适的增强动作。
- **反馈信号的重要性**：消融实验表明，生成器反馈和检索器反馈对于学习策略选择都至关重要，其中生成器反馈作用更大。采用简单的拒绝采样替代精细的软标签损失会导致性能大幅下降。

### 优点
- **系统级创新**：首次将查询增强和查询编码统一到单个解码器式大模型中，实现了端到端的查询理解，简化了传统RAG流程。
- **自适应能力强**：通过定义动作令牌并引入软反馈损失，使模型能根据查询内容和检索/生成反馈动态选择增强策略，避免了手工设定策略的弊端。
- **实用性强**：作为一个即插即用方案，UniRAG与多种大模型生成器兼容。同时，它提供了多种可配置的推理策略（如阈值解码），能在性能和计算成本之间做出灵活权衡。

### 不足与局限
- **策略集封闭**：模型依赖预定义的三种增强策略，该集合可能无法覆盖所有应用场景或用户意图，泛化能力受限。
- **依赖检索质量**：性能仍受限于外部知识库的质量。在低资源或高度专业领域，若检索到错误文档，可能引入噪声，影响最终生成效果。
- **计算开销**：尽管设计了阈值解码等策略，树解码等追求极致性能的推理方式会显著增加计算延迟和成本。
- **训练数据偏差**：训练数据合成依赖GPT-4o-mini，且从特定数据集中采样，可能引入外部模型的固有偏差，影响在某些数据分布上的公平性。
- **语料限制**：实验仅在英文维基百科语料上进行，未验证其在其他语言或不同类型知识库（如代码库、学术文献）上的效果。

（完）
