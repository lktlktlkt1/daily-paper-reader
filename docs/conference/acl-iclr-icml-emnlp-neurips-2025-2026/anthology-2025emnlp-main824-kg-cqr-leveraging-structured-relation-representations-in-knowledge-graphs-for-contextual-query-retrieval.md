---
title: "KG-CQR: Leveraging Structured Relation Representations in Knowledge Graphs for Contextual Query Retrieval"
title_zh: KG-CQR：利用知识图谱结构化关系表示进行上下文查询检索
authors: "Chi Minh Bui, Ngoc Mai Thieu, Vinh Van Nguyen, Jason J. Jung, Khac-Hoai Nam Bui"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.824.pdf"
tags: ["query:agentic-rag"]
score: 6.0
evidence: 基于知识图谱的上下文查询丰富，优化RAG检索
tldr: RAG检索阶段常忽略查询的上下文信息丢失问题。本文提出KG-CQR框架，利用语料库中心的知识图谱，通过子图提取、补全和上下文生成来丰富输入查询，使检索出的文档与查询意图更匹配。实验表明，该方法在复杂问题检索上提升了效果，为改善RAG的检索模块提供了实用方案。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.824/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 1034, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.824/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 784, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.824/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1647, \"height\": 1080, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.824/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 795, \"height\": 596, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1659, \"height\": 673, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1657, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 814, \"height\": 1110, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 810, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 812, \"height\": 1090, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1657, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1657, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1658, \"height\": 582, \"label\": \"Table\"}]"
motivation: 查询中上下文信息损失导致检索到的文档不相关。
method: 利用知识图谱提取子图并生成语义丰富的查询上下文。
result: 复杂查询的检索相关性得到提升。
conclusion: 结构化关系表示增强了查询的语义上下文，优化了RAG检索。
---

## Abstract
The integration of knowledge graphs (KGs) with large language models (LLMs) offers significant potential to enhance the retrieval stage in retrieval-augmented generation (RAG) systems. In this study, we propose KG-CQR, a novel framework for Contextual Query Retrieval (CQR) that enhances the retrieval phase by enriching complex input queries with contextual representations derived from a corpus-centric KG. Unlike existing methods that primarily address corpus-level context loss, KG-CQR focuses on query enrichment through structured relation representations, extracting and completing relevant KG subgraphs to generate semantically rich query contexts. Comprising subgraph extraction, completion, and contextual generation modules, KG-CQR operates as a model-agnostic pipeline, ensuring scalability across LLMs of varying sizes without additional training. Experimental results on the RAGBench and MultiHop-RAG datasets demonstrate that KG-CQR outperforms strong baselines, achieving improvements of up to 4–6% in mAP and approximately 2–3% in Recall@25. Furthermore, evaluations on challenging RAG tasks such as multi-hop question answering show that, by incorporating KG-CQR, the performance outperforms the existing baseline in terms of retrieval effectiveness.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
RAG系统中的检索阶段常因查询与文档嵌入空间不匹配而效果不佳，尤其是复杂、领域特定的查询面临上下文丢失的严峻挑战。现有方法如查询分解或生成假设文档，要么语义对齐不足，要么依赖LLM容易产生幻觉。KG-CQR旨在**通过语料库中心的知识图谱为查询注入结构化关系信息**，生成富含语义的上下文，从而提升检索质量。核心思想是：不直接编码原始查询，而是利用KG提取与补全子图，并生成一段连贯的上下文本，使查询表示更接近文档空间。

### 2. 论文提出的方法论
KG-CQR 是一个与模型无关的流水线框架，包含三个主要模块：

- **结构化关系表示与文本三元组表示（TTR）**  
  从非结构化语料中，使用LLM（如LLaMA-3.3-70B）构建知识图谱，并为每个三元组生成一段自然语言描述，即文本三元组表示（TTR），形式为 $(u, r, v, TTR(u, r, v))$。这样就将结构化三元组映射到语义丰富的文本空间，便于后续相似度计算。

- **子图提取**  
  对输入查询 $q$，计算其嵌入 $v_q$ 与所有三元组TTR嵌入 $v_{ir}$ 的余弦相似度，提取Top- $k$ 个相关三元组，再用LLM过滤掉不相关的三元组，得到初始子图 $\hat{T}'_{KG}$。

- **子图补全**  
  在初始子图实体对上运行带启发式引导的束搜索BFS（BFSBeam），以语义相似度为启发函数，寻找连接实体对的高相关路径，并添加这些路径涉及的新三元组，得到补全后的子图 $\hat{T}''_{KG}$。

- **上下文生成**  
  将补全子图输入LLM，生成一段连贯的上下文本 $KG\text{-}CQR(q)$。

- **检索融合**  
  将原始查询嵌入 $v_q$ 与生成上下文的嵌入 $v_{KG\text{-}CQR(q)}$ 通过加权求和融合：  
  $v_{fuse}(q) = \alpha \cdot v_q + (1-\alpha) \cdot v_{KG\text{-}CQR(q)}$，  
  再以该融合向量计算与文档的相似度，实现检索。

整个流程无需额外训练，可适应不同规模的LLM。

### 3. 实验设计
- **数据集**：  
  - RAGBench（约11,000条测试实例，覆盖5个产业领域）  
  - MultiHop-RAG（2,556条多跳查询）  
  另有HotpotQA和MuSiQue用于多步推理RAG评估（各采样500条）。

- **基准方法**：  
  - 稀疏检索：BM25  
  - 密集检索：DPR、BGE  
  - 查询增强方法：查询扩展（QE）、假设文档生成（HyDE）  
  - 在计算KG-CQR时，以上述检索器为基础，对比QE+检索器、HyDE+检索器。

- **实验类型**：  
  - 主要检索性能对比（mAP、Recall@5/10/25）  
  - LLM骨干（3B、8B、70B）的影响  
  - 消融实验（TTR与子图补全的作用）  
  - 多步推理RAG任务（与IRCoT框架集成）  
  - 检索延迟对比  
  - 与HippoRAG2的互补性实验  
  - 融合系数 $\alpha$ 的灵敏度分析

- **实现细节**：  
  使用LLaMA-3.3-70B构建KG并生成上下文，子图提取 $k=20$，束搜索宽度3，融合系数 $\alpha=0.7$。

### 4. 资源与算力
论文未明确提及所用的GPU型号、数量或训练时长。由于KG-CQR本身是免训练的推理框架，主要算力开销来自以下部分，但均未给出具体硬件与运行时间数据：
- 知识图谱构建：使用LLaMA-3.3-70B通过提示生成三元组与TTR。
- 推理阶段：子图提取、补全与上下文生成都需要LLM调用，实验对比了3B、8B、70B规模模型，但没有报告硬件配置与延迟/吞吐量（第4.3.4节只给出相对延迟对比，但无绝对数值）。

### 5. 实验数量与充分性
论文设置了较为丰富的实验组：
- 2个主数据集 × 6种对比方法 + 多种KG-CQR变体 ≈ 10余组主实验。
- LLM规模对比：3种模型（3B、8B、70B）× 各评估指标 → 3组。
- 消融实验：2个组件各移除一次 → 2组（加完整模型）。
- 多步推理RAG任务：3个数据集 × 2种检索器（BM25, BGE）× 3种LLM规模 → 大量组合。
- 融合系数 $\alpha$ 测试（0.3, 0.5, 0.7）× 2种检索器 × 3种模型规模 → 多组。
- 延迟对比与互补性实验各1组。
总体实验量足以支持论文结论，对比公平（均以相同基准检索器运行，超参固定），但**部分实验（如延迟）缺乏绝对数值，可重复性细节稍显不足**（如未公开KG构建的LLM调用次数等）。

### 6. 论文的主要结论与发现
- KG-CQR在RAGBench和MultiHop-RAG上均取得显著提升：最高mAP提升4–6%，Recall@25提升2–3%。
- 该框架与模型规模无关，但更大LLM可获得更好效果，小模型（3B/8B）依然有效。
- 消融实验证实文本三元组表示（TTR）和子图补全均对性能有重要贡献，其中TTR更为关键。
- 在多步推理RAG任务中，KG-CQR可提高F1和GPT-Score，同时减少推理所需的平均迭代步数。
- 与HippoRAG2结合后，性能进一步提升，说明KG-CQR可与语料库中心的KG方法互补。
- 相对延迟分析表明，带束搜索的子图补全在效率和语义表达间取得良好平衡，优于朴素BFS和HyDE。

### 7. 优点
- **新颖的查询补充范式**：首次将语料库中心KG的结构化三元组转换成自然语言上下文，再与原始查询融合，解决了查询-文档语义鸿沟。
- **模型无关、免训练**：可在不同规模LLM上即插即用，无需微调，实用性强。
- **技术细节扎实**：子图提取中采用TTR进行句子级匹配，过滤机制提升精度；子图补全通过聚合路径相关性扩展上下文，设计巧妙。
- **实验全面**：覆盖多种检索器、多个复杂数据集、多步推理任务，并对关键模块进行消融，结论说服力强。
- **效率考量**：采用束搜索权衡精度与效率，并在延迟分析中体现。

### 8. 不足与局限
- **KG构建依赖外部LLM**：实体/关系抽取的错误会向下游传播，实验未分析KG质量对检索的影响。
- **大规模KGs下的可扩展性未验证**：子图提取需对所有TTR做嵌入相似度计算，当KG包含数百万三元组时计算开销可能难以承受。
- **上下文生成的幻觉风险**：依赖LLM生成连贯上下文，若生成内容有误，可能降低检索准确性，文中未深入分析该风险。
- **实验覆盖的局限性**：仅在少量英文数据集上评估，缺少多语言、跨领域（如医学、法律）场景，也未对比更新近的检索增强方法（如图检索RAG）。
- **可重复性信息不足**：未公开KG构建的具体配置（LLM调用次数、提示细节），缺少绝对延迟数据与硬件信息。
- **对时间敏感和细粒度比较查询处理不佳**：错误分析显示，KG-CQR在需要时间推理或比较分析时仍存在上下文漂移和检索不相关的问题。

（完）
