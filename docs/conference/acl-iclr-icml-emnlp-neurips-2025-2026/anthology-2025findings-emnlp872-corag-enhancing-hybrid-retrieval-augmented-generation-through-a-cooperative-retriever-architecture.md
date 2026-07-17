---
title: "CoRAG: Enhancing Hybrid Retrieval-Augmented Generation through a Cooperative Retriever Architecture"
title_zh: CoRAG：通过协同检索架构增强混合检索增强生成
authors: "Zaiyi Zheng, Song Wang, Zihan Chen, Yaochen Zhu, Yinhan He, Liangjie Hong, Qi Guo, Jundong Li"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.872.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 结合文本与图结构的混合RAG协同检索器
tldr: 传统RAG忽视文档间依赖，混合RAG仅利用局部图结构，提出协同检索架构CoRAG，动态结合文本检索与图遍历，从全局视角捕捉远距离相关信息，在知识密集型任务中提升检索覆盖度与生成质量。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.872/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 713, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.872/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1634, \"height\": 836, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.872/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 722, \"height\": 535, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.872/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 721, \"height\": 634, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1299, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1638, \"height\": 945, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1578, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1662, \"height\": 1645, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1671, \"height\": 479, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1464, \"height\": 251, \"label\": \"Table\"}]"
motivation: 混合RAG中本地子图检索无法捕获全局远距离信息。
method: 设计CoRAG协同检索架构，动态选择文本或图路径实现全局知识检索。
result: 在多个基准上，CoRAG提升了信息覆盖和答案准确性。
conclusion: 协同检索架构为混合RAG中的文档间关联建模提供了新思路。
---

## Abstract
Retrieval-Augmented Generation (RAG) is introduced to enhance Large Language Models (LLMs) by integrating external knowledge. However, conventional RAG approaches treat retrieved documents as independent units, often overlooking their interdependencies. Hybrid-RAG, a recently proposed paradigm that combines textual documents and graph-structured relational information for RAG, mitigates this limitation by collecting entity documents during graph traversal. However, existing methods only retrieve related documents from local neighbors or subgraphs in the knowledge base, which often miss relevant information located further away from a global view. To overcome the above challenges, we propose CoRAG that dynamically chooses whether to retrieve information through direct textual search or explore graph structures in the knowledge base. Our architecture blends different retrieval results, ensuring the potentially correct answer is chosen based on the query context. The textual retrieval components also enable global retrieval by scoring non-neighboring entity documents based on semantic relevance, bypassing the locality constraints of graph traversal. Experiments on semi-structured (relational and textual) knowledge base QA benchmarks demonstrate the outstanding performance of CoRAG.

---

## 论文详细总结（自动生成）

好的，以下是对这篇论文的结构化总结：

### 1. 论文的核心问题与整体含义

*   **研究背景**：检索增强生成（RAG）通过引入外部知识来弥补大语言模型（LLMs）的事实性错误和幻觉问题。然而，传统的 RAG 将检索到的文档视为独立单元，忽略了文档之间的相互依赖关系。
*   **现有方法的不足**：混合 RAG（Hybrid-RAG）作为一种新兴范式，尝试结合文本信息和图谱结构化的关系信息。但现有的混合 RAG 方法存在两个关键挑战：
    *   **缺乏全局信息**：检索范围通常局限于局部邻居或子图，可能会遗漏位于远距离的、但语义相关的实体和文档。
    *   **缺乏查询感知的检索器选择**：现存方法通常不加区分地融合文本和关系检索结果，这可能会引入噪声、增加输入长度，并让 LLM 难以辨别信息优先级。
*   **核心问题**：如何设计一个能够动态、自适应地融合文本和关系信息，并具备全局检索视野的混合 RAG 框架，以提升在知识库问答（KBQA）任务中的性能。

### 2. 论文提出的方法论

论文的核心是提出了一个名为 **CoRAG** 的新型混合 RAG 框架，其关键在于名为 **Cooperative-Retrievers (CoR)** 的协同检索器架构。该架构采用分层门控网络动态融合不同来源的检索结果。

**关键技术细节与流程：**

1.  **话题实体提取**：首先，使用基于 Aho-Corasick 自动机的算法识别查询中的话题实体，并通过 LLM 进行可选的剪枝，以精确锚定查询涉及的图谱实体。
2.  **两类基础检索器**：
    *   **文本检索器**：根据实体类型（如疾病、药物）对知识库中的实体进行分组。每个实体类型都有一个独立的检索器，通过计算查询与文档的语义相似度，**在整个知识库范围内**进行检索，从而具备全局视野。其评分公式为 \( s(q, e) = \langle E_q(q), E_d(D_e) \rangle \)，仅在实体类型匹配时才有效。
    *   **关系检索器**：根据关系类型（如“表型存在”、“药物靶点”）进行分组。检索范围**仅限**于话题实体的图谱邻居，旨在捕捉局部结构化信息。
3.  **协同检索器架构 (CoR) —— 核心创新**：
    *   采用**分层门控网络**来动态选择和融合检索结果：
        *   **源级门控（文本门和关系门）**：分别为同类型的多个检索器分配权重，生成一个融合后的文本分数 \( s^{(t)} \) 和关系分数 \( s^{(r)} \)。
        *   **顶层混合门控**：动态地为文本分数和关系分数分配最终权重，生成最终的预测分数 \( \hat{s}(q, e) \)。这使得模型能够根据查询上下文，自适应地决定更偏重文本信息还是关系信息。
    *   每一个门控网络都基于查询的嵌入，并通过 softmax 函数输出权重向量。整个 CoR 模块通过最小化预测分数与真实答案分数的均方误差损失进行训练。
4.  **CoRAG 的完整流程**：首先用 CoR 检索出 top-\(k\) 个候选实体，然后利用一个 **LLM 重排器**（如 GPT-4o-mini）对这些候选实体进行二次打分，最后将 CoR 的分数与重排器的分数相加，进行最终排序。

### 3. 实验设计

*   **数据集**：使用了三个具有挑战性的、真实的半结构化知识库问答基准，来自 STaRK 基准，覆盖多个领域：
    *   **STaRK-Amazon**（电子商务）
    *   **STaRK-MAG**（学术）
    *   **STaRK-Prime**（医药）
*   **评估指标**：使用了 Hits@1, Hits@5, Recall@20, **MRR**（平均倒数排名）。
*   **对比方法**：
    *   **检索器基线**：DPR（密集段落检索）和 Multi-VSS，用于与 CoR 模块单独比较。
    *   **RAG 基线**：用于与完整的 CoRAG 框架比较，包括传统 RAG 方法（ReAct, Reflexion）、图 RAG 方法（QAGNN, ToG）以及混合 RAG 方法（AvaTaR, AGR）。

### 4. 资源与算力

*   **硬件配置**：论文提到实验在配备 48 核 CPU 和 NVIDIA A100 GPU 的服务器上执行。
*   **软件与框架**：使用 Python 3.11 和 PyTorch 2.6.0 实现。
*   **核心配置**：门控网络是一个两层 MLP，其输入是 OpenAI 的 `text-ada-002` 模型生成的查询嵌入。所有基础检索器的骨干编码器也默认使用 `text-ada-002` 模型。LLM 重排器使用 OpenAI 的 `gpt-4o-mini` 模型。
*   **算力消耗说明**：论文**未明确说明**使用的 GPU 具体数量或整体的模型训练/推理时长。

### 5. 实验数量与充分性

论文设计了较为全面的实验来验证其方法，体现了较好的充分性、客观性和公平性：
*   **多数据集、多指标评估**：在 3 个不同领域的数据集上，使用 4 个评估指标，与多达 7 个基线模型（涵盖 RAG、图 RAG、混合 RAG）进行对比。
*   **消融实验**：通过系统性地移除文本检索器、关系检索器和混合门控模块，验证了每个组件的必要性。
*   **敏感性分析**：探究了门控网络隐藏层维度大小对模型性能的影响。
*   **编码器通用性验证**：实验表明，使用不同的文本编码器（MiniLM, mpnet）作为骨干网络时，CoR 均一致地优于 DPR 基线。
*   **人类查询泛化性测试**：在 STaRK 数据集中专门的人类生成查询子集上验证了 CoR 的性能。
*   **案例研究**：通过可视化门控网络的注意力气，直观地展示了 CoR 设计的可解释性。

整体来看，实验设计从主要结果、内部机制、超参数影响、模型通用性和可解释性等多个角度进行了验证，充分且公平。

### 6. 论文的主要结论与发现

1.  **卓越的性能**：CoR（检索器模块）显著优于 DPR、Multi-VSS 等纯文本检索器；加上 LLM 重排器后的完整 CoRAG 框架在几乎所有指标上超越了现有的 RAG 和图 RAG 方法，证明了混合检索的潜力和当前瓶颈在于检索器。
2.  **关系信息的价值**：在需要更深层次语义推理和知识合成的领域（如学术、医药），引入关系信息的提升效果更为明显。
3.  **组件的协同作用**：消融实验证实，文本检索器、关系检索器和混合门控都是构成 CoR 高性能的关键部分，任一模块的移除都会导致性能下降，尤其是在医学数据集上，关系检索器的作用至关重要。
4.  **鲁棒性与可解释性**：CoR 在不同模型规模和数据集上表现稳定，并通过案例研究证明了其门控网络能自适应地为问题分配更高的注意力给最相关的检索器。

### 7. 优点

*   **创新性的架构**：提出的协同检索器（CoR）通过分层门控网络，优雅地解决了混合 RAG 中“何时使用何种信息”的挑战，实现了查询感知的动态融合。
*   **突破局部限制**：通过文本检索器的全局检索能力，弥补了传统图遍历方法只能访问局部邻居的缺陷。
*   **方法简洁且有效**：核心思想直观，架构清晰。实验证明，一个简单的前向网络加上 LLM 重排器就能取得显著的性能提升。
*   **实验全面扎实**：在多个跨领域数据集上，从多角度进行了充分的对比和消融实验，验证了方法的有效性和各组件的价值，结论具有很强的说服力。
*   **可解释性**：通过可视化门控网络的注意力，让模型的决策过程变得透明，展示了其“思考”过程与人类直觉的符合程度。

### 8. 不足与局限

*   **复杂的多跳推理能力不足**：论文明确指出，当前 CoR 模块的训练仅依赖最终答案的监督，导致其难以处理需要复杂逻辑和多跳推理的查询。这也是未来工作的重点。
*   **对 LLM 的依赖与成本**：话题实体提取使用 LLM 剪枝，重排阶段也依赖一个单独的 LLM，这会带来额外的计算开销和 API 调用成本。
*   **训练目标的简单性**：使用均方误差损失来拟合 0/1 的二元答案标签，可能不是优化排序任务的最优损失函数。
*   **话题实体提取的瓶颈**：整个框架严重依赖第一步话题实体提取的准确性。如果话题实体提取错误，则关系检索和最终的答案预测都可能失效。
*   **算力信息缺失**：未提供训练时长、GPU 算力消耗等具体信息，使得复现论文实验的硬件成本不够透明。

（完）
