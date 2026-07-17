---
title: "Agentic-R: Learning to Retrieve for Agentic Search"
title_zh: "Agentic-R: 学习为智能体搜索进行检索"
authors: "Wenhan Liu, Xinyu Ma, Yutao Zhu (朱余韬), Yuchen Li, Daiting Shi, Dawei Yin, Zhicheng Dou (窦志成)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.785.pdf"
tags: ["query:agentic-rag"]
score: 10.0
evidence: 面向智能体搜索的检索器训练，融合局部与全局效用
tldr: 本文针对智能体搜索中检索器设计未充分探索、传统检索器仅依赖局部相似性而忽略全局答案正确性的问题，提出Agentic-R训练框架。该框架利用局部查询-段落相关性和全局答案正确性共同度量段落效用，并通过迭代数据挖掘训练检索器。实验证明，Agentic-R在多步推理任务上大幅提升了检索质量和最终答案正确率，为智能体搜索提供了专用检索器方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.785/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 687, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.785/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1597, \"height\": 805, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.785/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.785/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 776, \"height\": 591, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.785/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1624, \"height\": 361, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.785/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1637, \"height\": 1016, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.785/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1643, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.785/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1662, \"height\": 938, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.785/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1656, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.785/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1736, \"height\": 581, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.785/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1659, \"height\": 2164, \"label\": \"Table\"}]"
motivation: 智能体搜索中检索器设计未充分探索，传统检索器忽略全局答案正确性。
method: 结合局部相关性与全局正确性度量效用，迭代训练面向智能体搜索的检索器。
result: 多步推理任务上检索质量和最终答案正确率大幅提升。
conclusion: 专用检索器是提升智能体搜索性能的关键组件。
---

## Abstract
Agentic search has recently emerged as a powerful paradigm, where an agent interleaves multi-step reasoning with on-demand retrieval to solve complex questions. Despite its success, how to design a retriever for agentic search remains largely underexplored. Existing search agents typically rely on similarity-based retrievers, while similar passages are not always useful for final answer generation. In this paper, we propose a novel retriever training framework tailored for agentic search. Unlike retrievers designed for single-turn retrieval-augmented generation (RAG) that only rely on local passage utility, we propose to use both local query-passage relevance and global answer correctness to measure passage utility in a multi-turn agentic search. We further introduce an iterative training strategy, where the search agent and the retriever are optimized bidirectionally and iteratively. Different from RAG retrievers that are only trained once with fixed questions, our retriever is continuously improved using evolving and higher-quality queries from the agent. Extensive experiments on seven single-hop and multi-hop QA benchmarks demonstrate that our retriever, termed Agentic-R, consistently outperforms strong baselines across different search agents.

---

## 论文详细总结（自动生成）

好的，以下是对该论文的结构化深入总结。

### 1. 论文的核心问题与整体含义

*   **研究背景**：智能体搜索是一种新兴范式，它允许大语言模型通过多步推理与按需检索交替进行来解决复杂问题。然而，现有研究主要集中于设计更强大的搜索智能体，而对其关键组件——**检索器**——的优化却鲜有关注。
*   **核心问题**：现有智能体搜索系统普遍直接采用基于语义相似度的现成检索器（如 E5、BGE），但这些检索器存在两个根本性缺陷：
    1.  **局部与全局脱节**：语义相似度高的段落（局部相关）未必对生成最终正确答案（全局正确）有贡献，甚至可能包含误导信息将推理引向歧途。
    2.  **训练范式不匹配**：传统的检索增强生成检索器为单轮检索设计，仅基于固定的用户问题和一次性的生成反馈进行训练，无法适应智能体搜索中多轮、演化的查询需求。
*   **整体含义**：本文旨在提出首个专为智能体搜索设计的检索器训练框架，**Agentic-R**，以填补研究与实际应用之间的空白，从检索源头提升整个智能体系统的性能与效率。

### 2. 论文提出的方法论

*   **核心思想**：训练一个能够理解**局部相关性**和**全局答案正确性**的检索器，并通过**智能体-检索器双向迭代优化**策略，让二者协同进化。
*   **关键技术细节：**
    *   **段落效用建模**：从两个维度衡量中间查询返回的候选段落的效用。
        1.  **局部相关性**：设计一个基于大语言模型的列表式评分方法，让大语言模型为同一查询下的多个候选段落打一个0-100的相关性分数。
        2.  **全局答案正确性**：将每个候选段落替换到搜索轨迹中，让智能体基于此前缀继续生成直至给出最终答案，并计算此答案与标准答案的精确匹配度。
    *   **正负例构建**：对所有候选段落，按照“全局答案正确性”优先、“局部相关性”其次的规则降序排列。排名第一且满足阈值条件的段落作为正例，其余排名靠后的段落作为负例。
    *   **检索器训练**：使用对比学习损失训练检索器 Agentic-R。其输入并非单一查询，而是原始问题`Q`与当前轮次查询`q_i`的拼接。训练时使用批内负样本和跨设备负样本扩大负例规模。
    *   **智能体-检索器迭代优化**：
        *   **智能体训练**：采用 PPO 强化学习算法，让智能体与检索器交互产生轨迹，以最终答案是否正确作为奖励信号。
        *   **双向迭代**：该过程在两个组件间交替进行。
            *   **第 1 轮**：用初始检索器（E5）训练搜索智能体 `Agent 1`，然后用 `Agent 1` 生成轨迹数据来训练检索器 `Agentic-R 1`。
            *   **第 2 轮**：用更强的 `Agentic-R 1` 训练出更强的 `Agent 2`，再用 `Agent 2` 生成更高质量的数据训练 `Agentic-R 2`，以此循环。

### 3. 实验设计

*   **数据集与场景**：在 7 个覆盖不同难度的问答基准上评估。
    *   **多跳问答**：HotpotQA， 2WikiMultihopQA， MuSiQue， Bamboogle。
    *   **单跳/通用问答**：Natural Questions (NQ)， TriviaQA， PopQA。
*   **评估指标**：精确匹配度。
*   **对比方法**：与两大类检索器基线进行了比较。
    1.  **通用嵌入模型**：BGE， E5。这些是智能体搜索中广泛使用的现成检索器。
    2.  **专用检索增强生成检索器**：LLM-Embedder, SCARLet, REPLUG。这些检索器专为单轮 RAG 优化，利用生成似然或任务级信号训练。
*   **泛化性测试**：不仅在本文训练的智能体上评估，还在另外两个开源智能体（**R1-Searcher** 和 **SimpleDeepSearcher**）上测试了其泛化能力。

### 4. 资源与算力

*   **硬件环境**：所有实验在配备 **8块NVIDIA A800 (80G)** GPU 的单节点服务器上进行。
*   **检索器训练**：
    *   初始模型为 `e5-base-v2`。
    *   训练轮数为 2，学习率为 `2e-5`，每设备批大小为 32。
*   **智能体训练 (RL)**：
    *   初始化模型为 `Qwen2.5-7B-Base`。
    *   训练步数为 500，总批大小为 512。
    *   为降低显存消耗，启用了梯度检查点和完全分片数据并行。
*   **智能体-检索器迭代**：共进行 2 轮迭代优化，因为实验证明第 3 轮无进一步提升。

### 5. 实验数量与充分性

*   **实验组数量**：实验设计非常充分。
    *   **主实验**：在 **7个数据集 × 3个搜索智能体** 的设定下，对比了 **6种不同检索器**（含 Agentic-R）的性能。结果在对应的表格中有详细报告。
    *   **消融实验**：系统性地移除了框架中的关键组件，包括 `迭代优化`、`全局答案正确性`、`局部相关性`和 `原始问题输入`，以验证各组件的有效性，共约 5 组变体。
    *   **辅助分析**：
        *   **搜索轮次分析**：对比了不同检索器下智能体所需的平均搜索轮次。
        *   **迭代次数分析**：探索了 K=1， 2， 3 轮迭代对性能的影响。
        *   **检索器骨干模型分析**：测试了 Agentic-R 在 E5-base， BGE-base， E5-large 等不同骨干上的表现。
        *   **输入消融实验**：测试了在检索器输入中加入历史查询的影响。
*   **客观性与公平性**：对比基线全面，包含了通用型和任务专用型检索器。所有方法（包括基线的复现）都在相同的数据集和语料库上进行，确保了比较的公平性。所有模型的训练数据构建流程清晰，评估指标客观。

### 6. 论文的主要结论与发现

*   **性能显著领先**：Agentic-R 在所有 7 个数据集和 3 个不同的搜索智能体上，其平均精确匹配度分数均**一致优于**所有强基线方法（包括通用检索器和单轮RAG专用检索器）。
*   **对多跳任务更有效**：Agentic-R 在多跳问答数据集上的性能提升幅度大于单跳问答，表明其对解决复杂推理任务特别有效。
*   **提升搜索效率**：使用 Agentic-R 可以使搜索智能体用**更少的搜索轮次**就能找到正确答案，显著提高了搜索效率。
*   **专用RAG检索器的局限性**：实验揭示，为单轮 RAG 设计的检索器（如 LLM-Embedder）在智能体搜索场景下并不总是优于通用检索器，凸显了为智能体搜索设计专用检索器的必要性。
*   **迭代优化收敛**：智能体-检索器的双向迭代优化在两轮后达到性能瓶颈，不再继续提升。

### 7. 优点

*   **问题新颖，填补空白**：首次系统性地研究并提出了针对智能体搜索的检索器训练框架，解决了该范式下被忽视的关键组件问题。
*   **方法论创新且鲁棒**：
    *   **双维度效用建模**：创新性地结合了局部相关性和全局答案正确性来评估段落价值，更加贴合多步推理场景。
    *   **双向迭代训练**：提出的智能体-检索器协同进化框架，使得检索器能够利用不断进化的智能体生成的高质量查询进行自我提升，形成正向飞轮效应。
    *   **输入设计巧妙**：将原始问题和当前查询拼接作为检索器输入，既提供了任务上下文又不引入历史噪声。
*   **实验扎实全面**：在广泛的数据集和多个异构智能体上进行了测试，充分证明了方法的有效性和泛化能力。深入的消融和分析实验为研究社区提供了宝贵洞见。

### 8. 不足与局限

*   **任务覆盖面有限**：实验仅在问答基准上进行，未在更具挑战性的专家级推理（如 GPQA）、科学推理或其他形式的下游任务上验证。
*   **实验规模限制**：受限于算力，实验使用的搜索智能体（7B）和检索器骨干（base/large 规模）相对中等。方法在更大规模模型（如 70B+）上的扩展性和性能表现尚待验证。
*   **训练范式依赖性**：智能体的训练依赖于强化学习（PPO），检索器的效用评估依赖于大语言模型评判，这些方法本身存在不稳定性或高成本问题，可能限制该框架的直接应用。
*   **数据领域单一**：训练和评估均基于 Wikipedia 构建的知识密集型问答数据集，在其他特定领域语料库上的表现可能有所不同。

（完）
