---
title: "KiRAG: Knowledge-Driven Iterative Retriever for Enhancing Retrieval-Augmented Generation"
title_zh: "KiRAG: 用于增强检索增强生成的知识驱动迭代检索器"
authors: "Jinyuan Fang, Zaiqiao Meng, Craig Macdonald"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.929.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 知识驱动的迭代三元组检索用于多跳问答
tldr: 本文针对迭代RAG在检索时易受无关文档干扰、检索器无法动态适应多步推理信息需求的问题，提出KiRAG框架。该框架将文档分解为知识三元组，并以此为基础进行知识驱动的迭代检索，动态补全每一步所需信息。实验结果表明，KiRAG在多跳问答任务上显著提升了检索精度和答案质量，为迭代RAG的鲁棒性提供了解决方案。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.929/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 760, \"height\": 294, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.929/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1573, \"height\": 715, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.929/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.929/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 807, \"height\": 355, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.929/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 715, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.929/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 760, \"height\": 648, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.929/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 795, \"height\": 253, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.929/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 804, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.929/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 806, \"height\": 363, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 802, \"height\": 543, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 802, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 244, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1635, \"height\": 300, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1486, \"height\": 424, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 590, \"height\": 173, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 756, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 801, \"height\": 416, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 801, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 799, \"height\": 903, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 802, \"height\": 453, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 798, \"height\": 447, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1548, \"height\": 712, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 797, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.929/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 799, \"height\": 229, \"label\": \"Table\"}]"
motivation: 迭代RAG检索器无法动态适应多步推理需求，且易受无关文档干扰。
method: 将文档分解为知识三元组，进行知识驱动的迭代检索，动态补全信息。
result: 在多跳问答任务上显著提升检索精度和答案质量。
conclusion: 知识驱动的迭代检索增强了多步推理的鲁棒性和准确性。
---

## Abstract
Iterative retrieval-augmented generation (iRAG) models offer an effective approach for multihop question answering (QA). However, their retrieval processes face two key challenges: (1) they can be disrupted by irrelevant documents or factually inaccurate chain-of-thoughts; (2) their retrievers are not designed to dynamically adapt to the evolving information needs in multi-step reasoning, making it difficult to identify and retrieve the missing information required at each iterative step. Therefore, we propose KiRAG, which uses a knowledge-driven iterative retriever model to enhance the retrieval process of iRAG. Specifically, KiRAG decomposes documents into knowledge triples and performs iterative retrieval with these triples to enable a factually reliable retrieval process. Moreover, KiRAG integrates reasoning into the retrieval process to dynamically identify and retrieve knowledge that bridges information gaps, effectively adapting to the evolving information needs. Empirical results show that KiRAG significantly outperforms existing iRAG models, with an average improvement of 9.40% in R@3 and 5.14% in F1 on multi-hop QA datasets.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：迭代式检索增强生成（iRAG，如 IRCoT）虽能有效解决多跳问答，但其检索过程仍面临两大痛点：
  - **噪声干扰**：先前检索到的文档常含无关信息，LLM 生成的思维链也可能包含事实性错误，这些噪声在迭代中会不断传播，破坏检索质量。
  - **信息需求动态变化**：多跳推理每一步所需的信息不同，现有基于语义相似度的通用检索器无法动态识别并补全当前步骤缺失的关键信息。
- **整体含义**：提出 **KiRAG**，一种知识驱动的迭代检索器，通过将文档级信息细化为**知识三元组**，并在检索过程中显式地、动态地填补信息缺口，从而让 iRAG 的检索过程更加可靠且适应多步推理。

### 2. 论文提出的方法论
- **核心思想**：将迭代检索从文档/句子层面下沉到**知识三元组层面**，构建一条逐步扩展的“知识三元组推理链”，每一步精确抓取缺失知识，最终基于这些三元组重排源文档。
- **关键技术细节与流程**：
  - **离线阶段**：对语料库中所有文档，利用 LLM 预抽取形如 `⟨头实体; 关系; 尾实体⟩` 的三元组，构建知识图谱语料库。
  - **迭代检索（在线）**：
    - **知识分解**：用通用检索器检索一批候选文档，从中获取预计算的三元组。
    - **候选知识识别**：使用一个经过专门训练的**双编码器（Reasoning Chain Aligner）**，为当前推理链与问题编码，从候选三元组中选取最可能补充信息缺口的前 *N* 个三元组。
    - **推理链构建**：将候选三元组交给 LLM（Reasoning Chain Constructor），通过生成“知识链（CoK）”的方式选出用于扩展当前链的下一跳三元组，输出形式为 `… ⟨关系; 尾实体⟩`。仅取第一个新三元组追加到链。
  - **文档排序**：迭代结束后，收集所有被选三元组对应的源文档，按其对应三元组的 Aligner 得分进行排序，返回 top-*K* 文档。
  - **答案生成**：将问题和排序后的文档送入读者模型（LLM）生成最终答案。
- **训练策略**：
  - **训练数据构造**：利用多跳 QA 训练集，用 TRACE 方法为每个问题构造知识三元组推理链，并选出能回答正确的那一条作为银标准标签。
  - **对比学习**：对于推理链中的每个不完整链，将正确的下一个三元组作为正样本，同一迭代步中的其他候选三元组作为负样本，通过对比损失训练 Aligner。

### 3. 实验设计
- **数据集**：
  - **多跳 QA**：HotPotQA、2WikiMultiHopQA、MuSiQue、Bamboogle、WebQuestions。
  - **单跳 QA**：Natural Questions（测试泛化能力）。
- **基准方法**：
  - **标准 RAG**：单步检索 + 阅读。
  - **迭代 RAG**：IRCoT、FLARE、DRAGIN。
  - **增强检索**：BeamDR、Vector-PRF。
  - **变体**：KiRAG-Doc（用文档代替三元组迭代）、KiRAG-Sent（用句子代替三元组）。
- **评估指标**：检索用 R@3 和 R@5；问答用 EM 和 F1。
- **实验设置**：基础检索器用 E5 或 BGE，阅读器用 Llama3、Qwen2.5 等，Aligner 初始化为 E5 后进行微调，三元组抽取和推理链构建均用 Llama3（可替换）。

### 4. 资源与算力
- **硬件**：实验在一台 3.5 GHz、32 核 AMD Ryzen Threadripper 处理器搭配 **NVIDIA A6000 GPU** 的环境下完成。
- **训练配置**：Aligner 训练使用 Adam 优化器，学习率 2e-5，batch size 64，每样本 7 个负例，温度 τ=0.01，共训练 10 轮，在开发集上选择最佳 checkpoint。
- **说明**：论文未明确给出训练总时长或所需的 GPU 数量，仅描述了单个 GPU 型号和训练超参数。

### 5. 实验数量与充分性
- **主实验**：在 5 个多跳、1 个单跳数据集上对比 6 类基准，覆盖检索和问答指标。
- **消融实验**：移除 Retriever、移除 Aligner、移除 Constructor、移除 Aligner 训练（使用冻结的 E5）等，分别在 3 个多跳数据集上验证。
- **分析实验**：
  - 不同推理步数 L 的影响；
  - 初始检索文档数 K0 的影响；
  - 候选三元组数 N 的影响；
  - 不同 LLM 作 Constructor 的效果；
  - 不同 Retriever 和不同 Reader 的组合效果；
  - 效率分析（时延 vs. R@3）；
  - 案例分析与三元组检索质量人工评估（100 条标注数据）。
- **评价**：实验设计**充分且公平**，基线均采用与 KiRAG 相同的底层检索器和阅读器，多维度消融证实各组件的有效性，且包含泛化性测试和效率分析。

### 6. 论文的主要结论与发现
- KiRAG 在所有多跳 QA 数据集上均**显著优于**现有 iRAG 模型，平均提高 9.40% R@3、5.14% F1。
- 相较于基于文档或句子的迭代检索，知识三元组能有效抑制噪声，提升后续步骤的检索召回。
- 相比依赖 LLM 生成思维链的 IRCoT，KiRAG 的知识三元组建模更忠实于文档，避免了幻觉性错误传播。
- 训练 Aligner 以识别信息缺口是必要的，移除训练后性能大幅下降。
- KiRAG 在未见过的多跳和单跳 QA 上均展现出强泛化能力。

### 7. 优点
- **细粒度抗噪**：将检索单元从文档下沉到三元组，减少噪声累积。
- **动态适应性**：通过 Aligner 和 Constructor 显式建模“当前还缺什么知识”，能针对性地补全信息。
- **训练高效**：只微调 Aligner 双编码器，其他组件（检索、LLM）冻结，保持模型的可替换性和灵活性。
- **实验扎实**：多数据集、多基线、多消融、多 reader/retriever，验证全面，结果一致性强。
- **实际可行**：离线预抽取三元组的方式大幅降低了在线耗时，在效率和效果间取得平衡。

### 8. 不足与局限
- **训练数据局限**：Aligner 的训练数据仅由三个多跳 QA 数据集通过规则方法构造，银标准质量可能影响对齐能力，且未探索更大规模语料。
- **Constructor 未微调**：LLM 作为推理链构建器保持冻结，可能限制其在特定场景下的最优表现。
- **检索组件依赖**：仍需启动通用检索器取回一批文档，初期检索错误会传播；移除该步骤会掉点。
- **预抽取成本**：虽然加速了在线推理，但对全语料库做三元组抽取需要额外存储和预处理，动态变化的语料维护开销大。
- **领域泛化未评估**：所有实验均在 Wikipedia 背景的数据集上，在新闻、法律、医学等垂直领域的适应性未知。
- **可解释性有限**：虽生成推理链，但链中三元组的选择逻辑仍受 LLM 黑盒影响，Aligner 提供的分数也未与人类可理解的理由关联。

（完）
