---
title: "SeaKR: Self-aware Knowledge Retrieval for Adaptive Retrieval Augmented Generation"
title_zh: SeaKR：面向自适应检索增强生成的自我感知知识检索
authors: "Zijun Yao, Weijian Qi, Liangming Pan, Shulin Cao, Linmei Hu, Liu Weichuan, Lei Hou, Juanzi Li"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1312.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 自感知不确定性驱动的自适应检索与多步检索
tldr: 自适应RAG动态决策知识检索，提出SeaKR模型，从LLM内部状态提取自感知不确定性，当不确定性高时激活检索，并利用该不确定性重排序片段，支持多步检索以解决复杂任务。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1312/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 771, \"height\": 677, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1312/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1613, \"height\": 745, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1312/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 788, \"height\": 388, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 789, \"height\": 483, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 789, \"height\": 438, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 784, \"height\": 785, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 787, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1640, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 784, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1261, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 622, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 782, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1566, \"height\": 1873, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1638, \"height\": 2425, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1312/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1634, \"height\": 2211, \"label\": \"Table\"}]"
motivation: 现有自适应RAG未能充分利用LLM的内部状态来指导检索时机和质量。
method: 设计SeaKR，通过LLM自感知不确定性触发和重排序检索，实现多步自适应知识检索。
result: 在复杂问答任务中，SeaKR的多步自适应机制有效减少幻觉。
conclusion: 自感知不确定性为RAG的检索时机和内容选择提供了新的有效信号。
---

## Abstract
Adaptive Retrieval-Augmented Generation (RAG) is an effective strategy to alleviate hallucination of large language models (LLMs). It dynamically determines whether LLMs need external knowledge for generation and invokes retrieval accordingly. This paper introduces Self-aware Knowledge Retrieval (SeaKR), a novel adaptive RAG model that extracts self-aware uncertainty of LLMs from their internal states. SeaKR activates retrieval when the LLMs present high self-aware uncertainty for generation. To effectively integrate retrieved knowledge snippets, SeaKR re-ranks them based on LLM’s self-aware uncertainty to preserve the snippet that reduces their uncertainty to the utmost. To facilitate solving complex tasks that require multiple retrievals, SeaKR utilizes their self-aware uncertainty to choose among different reasoning strategies. Our experiments on both complex and simple Question Answering datasets show that SeaKR outperforms existing adaptive RAG methods.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义
*   **研究动机**：检索增强生成（RAG）是缓解大语言模型（LLM）幻觉的有效方法，但传统的“每问必检”式检索不仅效率低下，还可能引入与模型内部知识冲突的噪声信息，导致性能下降。
*   **核心问题**：现有的自适应RAG方法主要依据模型的输出（如生成概率）来决定何时检索，这种方式较为浅层，容易受到LLM普遍存在的“过度自信”自偏误（self-bias）影响，无法准确反映模型真实的知识需求。同时，如何有效整合检索到的知识也常被忽略。
*   **整体含义**：本文提出了一种新颖的自适应RAG模型——**自感知知识检索（SeaKR）**，它首次探索利用LLM内部状态的“自感知不确定性”来动态决定何时检索以及如何整合检索到的知识，旨在更精准、高效地抑制幻觉。

### 方法论
SeaKR的核心思想是从LLM的内部状态（而非输出层）中提取其对于生成的“不确定性”信号，并将此信号贯穿于检索决策、知识重排和最终推理的全过程。
*   **自感知不确定性估计器**：
    *   **思想**：LLM在生成错误内容时，其内部表征的一致性会降低。
    *   **实现**：对同一输入上下文，让LLM进行多次（k次）独立生成，并提取每次生成结束符（`<EOS>`）在特定Transformer层（取中间层）的前馈网络（FFN）中的隐藏状态。
    *   **量化**：计算这 $k$ 个隐藏状态向量的**正则化格拉姆（Gram）矩阵的行列式**作为自感知不确定性分数。行列式值越低，代表多次生成的内部状态一致性越高，不确定性越低。
*   **自感知检索（何时检索）**：
    *   SeaKR迭代式地进行推理。在每一步生成推理步骤前，它会先进行一轮“伪生成”。
    *   系统评估此轮伪生成的自感知不确定性。若不确定性分数 $U(c_r) > \delta$（$\delta$ 为阈值），则触发外部知识检索。
    *   检索查询由伪生成内容中概率较低、不确定的部份构成。
*   **自感知重排（如何整合知识）**：
    *   对于检索引擎返回的多个知识片段，SeaKR并非选择与查询语义最相关的，而是选择**最能降低LLM自感知不确定性的**片段。
    *   它将每个候选片段分别与问题、历史推理拼接成新的上下文，输入LLM并计算各自的不确定性，最终保留导致不确定性最低的那个知识片段。
*   **自感知推理（多步任务解决）**：
    *   对于需要多步检索的复杂任务，SeaKR在生成最终答案时，会尝试两种策略：1）仅基于历史推理步骤直接生成答案；2）串联所有已重排知识片段，作为上下文进行链式思维（CoT）推理生成答案。
    *   它通过比较两种策略下生成答案的不确定性分数，选择不确定性更低的那个作为最终输出。

### 实验设计
*   **数据集**：
    *   **复杂问答（QA）**：2WikiMultiHopQA、HotpotQA、IIRC（答案子集）。主要评估多跳推理能力。
    *   **简单问答（QA）**：NaturalQuestions、TriviaQA、SQuAD（均为开放域设置）。
*   **基准方法**：
    *   **非自适应检索**：无检索的纯CoT、每步都检索的IRCoT。
    *   **自适应检索**：基于输出概率的**FLARE**和**DRAGIN**、基于微调LLM决策的**Self-RAG**。
*   **实验设置**：使用LLaMA-2-chat（7B）作为骨干LLM，BM25作为搜索引擎，英文维基百科（2018年12月20日版本）作为外部知识源。SeaKR本身是一个免调优方法。

### 资源与算力
*   **硬件配置**：所有实验可在单块**NVIDIA 3090 GPU（24GB显存）**上完成。
*   **推理加速**：为解决多次伪生成带来的计算开销，SeaKR采用**vLLM框架**的并行推理技术，使20次伪生成的延迟与单次生成大致相同。

### 实验数量与充分性
*   **主实验**：在3个复杂QA和3个简单QA数据集上，与5种基线方法进行了对比，使用了Exact Match（EM）和F1指标。
*   **消融实验**：充分验证了各个组件，包括：
    1.  **不确定性估计器**：对比了基于提示、困惑度、长度归一化熵、能量分数的方法。
    2.  **关键组件**：分别移除自感知检索、自感知重排和自感知推理，观察性能变化。
*   **鲁棒性与扩展性分析**：
    *   更换了更强大的骨干模型（LLaMA-3 8B）。
    *   对比了基座模型和对齐模型（chat/instruct版）的影响。
    *   进行了超参数（$N, k, \delta$）搜索。
    *   提供了详细的案例分析。
*   **公平性与充分性判断**：实验设计非常全面且公平。所有基线方法均使用相同的骨干LLM、搜索引擎和知识库。消融实验清晰地揭示了各组件的贡献，特别是对不确定性估计器和知识整合策略的深入分析，使得结论极具说服力。

### 主要结论与发现
1.  **整体优越性**：SeaKR在复杂QA任务上显著优于所有现有的自适应RAG基线方法，在简单QA任务上也展现了有竞争力的表现。
2.  **内部状态至关重要**：从LLM内部状态提取的自感知不确定性，比基于输出概率或提示的感知更准确，更能反映LLM的真实知识需求。
3.  **知识整合不可或缺**：消融研究表明，动态的自感知重排和推理策略对性能的贡献甚至超过了“何时检索”的决策，凸显了在自适应RAG中设计有效知识整合机制的重要性。
4.  **方法泛化性**：SeaKR的表现随着骨干LLM（从LLaMA-2到LLaMA-3）的增强而提升，证明其具有可扩展性。同时，免调优特性使其比微调方法（如Self-RAG）有更好的跨数据集泛化能力。

### 优点
*   **创新性强**：首次将LLM内部状态的“自感知不确定性”系统地应用于自适应RAG的检索决策和知识整合全过程，为RAG领域提供了新视角。
*   **方法务实全面**：SeaKR不仅关注“何时检索”，还通过自感知重排和推理设计了完整的知识整合方案，形成了一个端到端的自适应框架。
*   **可解释性好**：通过案例研究表明，模型确实能识别自身知识盲区并精准检索，选择的知识片段也确为补全盲区的关键信息，决策过程可追溯。
*   **免调优、易部署**：SeaKR无需任何微调，可直接应用于不同LLM和数据集，扩展性强，避免了特定数据分布的偏差风险。

### 不足与局限
*   **适用范围受限**：必须访问LLM的内部状态，因此**仅限于开源的LLM**，无法应用于GPT-4等闭源商业模型。
*   **任务覆盖面窄**：仅在短文本问答任务上进行了验证，在长文本生成、创意写作等更广泛的NLP任务上的有效性未知。
*   **计算开销**：尽管通过vLLM优化，但计算格拉姆行列式仍需进行多次（如20次）伪生成，存在固有计算成本。
*   **骨干模型规模探索不足**：受算力限制，仅在7B和8B参数的模型上进行了实验，未在更大规模的LLM上验证。
*   **检索技术的可替代性风险**：作者承认，随着信息检索（IR）技术的发展，其“自感知重排”模块可能被未来更先进IR方法所超越。
*   **存在被滥用的风险**：不确定性估计器可能被用作对抗信号，训练出更具欺骗性的模型，或结合IR系统实施自动化网络暴力等人肉搜索。

（完）
