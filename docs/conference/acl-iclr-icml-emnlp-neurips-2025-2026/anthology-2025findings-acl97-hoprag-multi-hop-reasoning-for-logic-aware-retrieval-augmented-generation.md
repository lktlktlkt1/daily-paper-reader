---
title: "HopRAG: Multi-Hop Reasoning for Logic-Aware Retrieval-Augmented Generation"
title_zh: "HopRAG: 面向逻辑感知检索增强生成的多跳推理"
authors: "Hao Liu, Zhengren Wang, Xi Chen, Zhiyu Li, Feiyu Xiong, Qinhan Yu, Wentao Zhang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.97.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 基于图的逻辑推理多跳检索
tldr: 本文针对RAG中传统检索器注重语义相似性而忽略逻辑相关性的问题，提出HopRAG框架。该框架在索引阶段构建基于伪查询的篇章图，在检索阶段通过检索-推理-剪枝机制进行多跳逻辑探索，从而发现逻辑相关的段落。实验结果显示，HopRAG在多个多跳推理基准上提升了答案准确性，证明了逻辑感知检索对复杂推理任务的重要性，为增强RAG的推理能力提供了有效方法。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 743, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1594, \"height\": 339, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1624, \"height\": 815, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1243, \"height\": 1227, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1245, \"height\": 1242, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1255, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1153, \"height\": 296, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 726, \"height\": 1043, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1153, \"height\": 545, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1156, \"height\": 544, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1483, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1487, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1485, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1319, \"height\": 886, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1523, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1630, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1607, \"height\": 2314, \"label\": \"Table\"}]"
motivation: 传统检索器注重语义相似性，忽略逻辑关联，导致检索不完美。
method: 构建篇章图，通过检索-推理-剪枝机制实现逻辑感知的多跳检索。
result: 在多跳推理基准上提升了答案准确性，验证了逻辑检索的有效性。
conclusion: 逻辑感知检索能显著改善RAG在复杂推理任务中的表现。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems often struggle with imperfect retrieval, as traditional retrievers focus on lexical or semantic similarity rather than logical relevance. To address this, we propose HopRAG , a novel RAG framework that augments retrieval with logical reasoning through graph-structured knowledge exploration. During indexing, HopRAG constructs a passage graph, with text chunks as vertices and logical connections established via LLM-generated pseudo-queries as edges. During retrieval, it employs a retrieve-reason-prune mechanism: starting with lexically or semantically similar passages, the system explores multi-hop neighbors guided by pseudo-queries and LLM reasoning to identify truly relevant ones. Experiments on multiple multi-hop benchmarks demonstrate that HopRAG’s retrieve-reason-prune mechanism can expand the retrieval scope based on logical connections and improve final answer quality.

---

## 论文详细总结（自动生成）

好的，我们基于论文内容，生成结构化的中文总结如下。

### 1. 论文的核心问题与整体含义
- **核心问题**：现有检索增强生成（RAG）系统依赖的检索器（稀疏或稠密）通常只关注词法或语义相似度，而**忽略了文档与查询之间的逻辑相关性**。这种“不完美检索”现象导致检索到的段落虽然相似但不直接相关，或者遗漏了关键信息，进而引发大模型回答不准确或不完整，尤其在需要多条证据的多跳问答任务中尤为突出。
- **整体含义**：本文旨在**将逻辑推理能力引入检索模块**，首次明确利用不直接相关但语义相似的段落作为跳板，通过多步逻辑探索来发现真正支撑答案的段落，从而将检索的“废料”变为“宝藏”，提升复杂问答的质量。

### 2. 论文提出的方法论
论文提出 **HopRAG** 框架，由两部分组成：**图结构索引构建**与**推理增强的图遍历检索**。

- **图结构索引**：
  - **顶点**：每个段落文本块作为一个顶点。
  - **边**：通过大模型为每个段落生成两类**伪查询**来建立逻辑连接。
    - **出站问题**：由该段落引出但不能被自身回答的问题。
    - **入站问题**：答案包含在该段落内的问题。
  - **边合并**：利用命名实体识别和嵌入模型，计算段落间的出站问题与入站问题的混合相似度，将匹配度最高的段落用有向边连接起来，边特征为对应的问题、关键词及语义向量。
- **推理增强的图遍历检索**：
  采用 **Retrieve-Reason-Prune** 三步范式。
  - **检索**：对用户查询进行关键词和向量混合检索，找到 `top_k` 个相似边，将其目标顶点作为起始点，加入上下文队列 `Cqueue`。
  - **推理**：进行 `nhop` 轮宽度优先搜索。在每轮中，让大模型推理队列中每个顶点的所有出边问题，选择对回答原始查询最有帮助的问题，并跳到其连接的顶点。访问次数的计数器 `Ccount` 用于衡量顶点的重要性。
  - **剪枝**：提出 **Helpfulness** 新指标，综合混合文本相似度和归一化访问次数（逻辑重要性）对 `Ccount` 中的顶点重排序，保留前 `top_k` 个顶点作为最终上下文。
  - **公式**：Helpfulness (Hi) = SIM(vi, q) + IMP(vi, Ccount) / 2，其中IMP是基于访问次数的归一化值。

### 3. 实验设计
- **数据集**：在三个典型的多跳问答基准上进行实验：
    - **HotpotQA**
    - **2WikiMultiHopQA**
    - **MuSiQue**
    每个数据集的验证集采样1000个问题。
- **对比方法**：对比了多种基线方法，涵盖非结构化、树结构、图结构RAG。
    - **非结构化**：BM25、稠密检索器（BGE）、查询分解、重排序。
    - **树结构**：RAPTOR、SiReRAG。
    - **图结构**：GraphRAG、HippoRAG。
- **评价指标**：答案准确度（EM和F1分数）以及检索F1分数。
- **设置**：使用BGE模型生成语义向量；大模型方面，索引构建和推理遍历使用 GPT-4o-mini，最终回答生成分别使用 GPT-4o 和 GPT-3.5-turbo。默认检索上下文 `top_k=20`，跳数 `nhop=4`。

### 4. 资源与算力
- 论文**未明确说明**使用了何种 GPU 型号、数量以及具体的训练或索引构建时长。
- 文中唯一涉及的算力估算出现在附录的“检索效率”分析中，提到使用本地部署的 Qwen2.5-1.5B-Instruct 作为遍历模型时，每个查询额外增加的 LLM 推理延时约为 18.86 秒（基于 BF16 和 Transformer），若采用 vLLM 和 GPTQ-Int4 技术则可降至 4.43 秒。这表明主要的资源开销来自遍历阶段的大模型调用。

### 5. 实验数量与充分性
- **实验组数较多**：总计至少包含 3 个数据集 × 多种基线方法的主实验、`top_k` 变化的鲁棒性实验（6种设置）、`nhop` 变化的消融实验（4种设置）以及遍历模型的消融实验（3种变体加两个基线）。实验设计较为全面。
- **充分性与公平性**：
    - 对比基线丰富，涵盖了从稀疏到稠密、从非结构化到图结构的多种先进方法，比较公平。
    - 消融实验深入考察了关键超参数（`top_k`, `nhop`）和遍历模型（非LLM、小模型、强模型）的影响，揭示了性能与成本的权衡。
    - 在 `top_k` 实验中，通过少量上下文（如12条）就能达到与基线20条相近的效果，证明了逻辑跳跃的有效性。
    - 对于树状结构RAG因生成新候选（摘要节点）而无法公平比较检索指标的问题，论文明确指出并仅在图方法间比较了检索指标，处理得当。

### 6. 论文的主要结论与发现
- **HopRAG 在多个多跳 QA 基准上均取得最优性能**，平均答案指标比稠密检索器BGE高出约 76.78%，比先进的图/树结构方法（如HippoRAG、SiReRAG）也稳定提升。
- **逻辑感知检索机制显著有效**：通过“检索-推理-剪枝”过程，能够从间接相关的段落有效跳转到真正相关的段落，解决了传统检索器只关注相似性而忽略逻辑性的痛点。
- **超参数 `top_k` 和 `nhop` 的实验表明**：HopRAG 能在较小的上下文窗口内实现高效检索；增加跳数虽能提升检索性能，但会线性增加 LLM 的调用开销，需要权衡。
- **遍历模型的消融证实**：即使不用大模型推理，单纯基于相似度匹配的图遍历也能大幅超越传统检索器，但引入大模型推理能将性能再提升约 45.78%，且使用轻量级小模型（Qwen2.5-1.5B）即可取得接近GPT-4o-mini的竞争力，为效率优化提供了方向。

### 7. 优点
- **创新性地解决关键痛点**：首次揭示并量化了“间接相关”段落在多跳推理中的价值，提出了将其作为“垫脚石”的思想，是对现有RAG研究的有力补充。
- **优雅的图索引设计**：利用LLM生成伪查询建立边，灵活建模段落间的逻辑关系，既避免了传统知识图谱严格的模式限制和实体抽取误差，又无需引入摘要节点等额外信息，保持了结构的轻量性和文本的原始性。
- **检索-推理-剪枝机制高效**：将检索、大模型推理和基于访问频率的剪枝有机结合，使检索过程具备“航行”能力，即从相似段落出发，沿逻辑边有目的地探索。
- **实验扎实且分析透彻**：对比基线全面，消融实验不仅证明了各模块的有效性，还深入分析了“性能-成本”的权衡，为实际部署提供了建议。

### 8. 不足与局限
- **评估任务单一**：目前实验仅集中于多跳/多文档问答任务，尚未在更多样化的领域或任务（如摘要、对话）上验证其泛化能力。
- **索引构建与遍历开销**：生成伪查询和推理遍历依赖大模型调用，这会带来不可忽略的计算成本和延迟。尽管小模型可作为一种优化策略，但在大规模、高实时性场景下仍是一大挑战。
- **图结构的理想化假设**：文中的段落图是建立在理想分块（数据集原始支持事实分块）基础上的，现实异构文档的分块质量会直接影响逻辑边的有效性和图遍历的效果。
- **实验范围局限**：未研究不同嵌入模型、不同参数量的遍历模型对性能的系统性影响，也未报告索引构建阶段的具体时间和资源消耗。

（完）
