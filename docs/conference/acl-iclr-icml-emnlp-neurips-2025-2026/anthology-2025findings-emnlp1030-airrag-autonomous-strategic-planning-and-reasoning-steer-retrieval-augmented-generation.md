---
title: "AirRAG: Autonomous Strategic Planning and Reasoning Steer Retrieval Augmented Generation"
title_zh: AirRAG：自主战略规划与推理引导的检索增强生成
authors: "Wenfeng Feng, Chuzhan Hao, Yuewei Zhang, Guochao Jiang, Jingyi Song"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1030.pdf"
tags: ["query:agentic-rag"]
score: 10.0
evidence: AirRAG采用自主战略规划和基于MCTS的推理行动实现智能体RAG
tldr: 针对现有迭代或智能体RAG方法常限于单一解空间的问题，提出AirRAG，融合自主战略规划与高效推理行动。设计了五种基本推理行动，并通过蒙特卡洛树搜索扩展特定任务的解空间，激活内在推理能力。在复杂推理任务上，AirRAG表现优于固定路径的RAG方法，为自主RAG推理提供了可扩展的探索框架。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 788, \"height\": 560, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1648, \"height\": 829, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1622, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1555, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1612, \"height\": 1252, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 972, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1611, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1583, \"height\": 379, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1655, \"height\": 1036, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1649, \"height\": 1600, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 714, \"height\": 410, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1246, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1299, \"height\": 966, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1030/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1283, \"height\": 438, \"label\": \"Table\"}]"
motivation: 现有智能体RAG在复杂问题下面临单一解空间约束。
method: AirRAG定义五种推理行动，利用MCTS进行自主战略规划，扩大解空间。
result: 实验表明AirRAG在复杂推理任务上超越了基线智能体RAG方法。
conclusion: 自主规划与MCTS的融合增强了RAG的推理多样性和性能。
---

## Abstract
Leveraging the autonomous decision-making capabilities of large language models (LLMs) has demonstrated superior performance in reasoning tasks. However, despite the success of iterative or agentic retrieval-augmented generation (RAG) techniques, these methods are often constrained to a single solution space when confronted with complex problems. In this paper, we propose a novel thinking pattern in RAG that integrates autonomous strategic planning with efficient reasoning actions, significantly activating intrinsic reasoning capabilities and expanding the solution space of specific tasks via Monte Carlo Tree Search (MCTS), which we refer to as AirRAG. Specifically, our approach designs five fundamental reasoning actions, which are expanded to a broad tree-based reasoning space using MCTS. The approach also incorporates self-consistency verification to explore potential reasoning paths and inference scaling law. Additionally, computationally optimal strategies are employed to allocate more inference resources to key actions, thereby enhancing overall performance. Experimental results demonstrate the effectiveness of AirRAG, showing significant performance gains on complex question-answering datasets. Furthermore, AirRAG is flexible and lightweight, making it easy to integrate with other advanced technologies and models.

---

## 论文详细总结（自动生成）

好的，我们将基于提供的论文内容，对《AirRAG: Autonomous Strategic Planning and Reasoning Steer Retrieval Augmented Generation》一文进行结构化、深入、客观的总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：当前迭代式或智能体式检索增强生成（Iterative/Agentic RAG）在处理复杂推理问题时，虽然利用了大型语言模型（LLMs）的自主决策能力，但往往受限于单一的推理范式（如链式推理），难以有效探索广阔的**解空间**（Solution Space）。这类方法容易陷入低质量的中间推理步骤，或过早收敛于局部最优解。
- **整体含义**：为解决上述局限，本文提出了一种全新的RAG思维模式——**AirRAG**。其核心在于将**自主战略规划**与**蒙特卡洛树搜索（MCTS）** 相结合，通过设计有限的原子化推理动作，并将其组合、扩展为树状的推理路径，从而系统性地激活LLMs的内在推理能力，显著扩大解决特定任务时的探索边界。

### 2. 论文提出的方法论
- **核心思想**：通过定义基本推理动作空间，利用MCTS进行自主规划和路径探索，并结合自洽性验证（Self-Consistency）和推理计算规模法则（Inference Scaling Law）来提升最终答案的质量。
- **关键技术细节**：
    - **五种基础推理动作（Action Space）**:
        1. **系统分析 (System Analysis, SAY)**：全局性地分析或分解问题。
        2. **直接回答 (Direct Answer, DA)**：不依赖外部知识，直接使用LLM内部知识。
        3. **检索回答 (Retrieval-Answer, RA)**：从外部知识库检索相关信息并回答问题。
        4. **查询转换 (Query Transformation, QT)**：通过改写、回退提示、生成子问题等方式优化查询。
        5. **总结回答 (Summary-Answer, SA)**：基于所有中间推理步骤，生成最终答案。
- **MCTS推理过程**:
    - 将每个动作视为MCTS中的一个节点，LLM的策略函数`π(a|s) = LM(a|s)`负责生成动作，状态转移为当前步骤拼接历史动作。
    - 采用**UCT (Upper Confidence Bounds applied to Trees)** 公式进行节点的选择（Selection）与扩展（Expansion），平衡探索（Exploration）与利用（Exploitation）。
    - 通过前向模拟（Simulation）和反向传播（Backpropagation）更新节点的奖励值，直到找到终态节点或达到预设深度。
- **推理计算规模化与优化**:
    - 通过增加每次检索的文档数、扩大有效上下文长度（$L_{max}$）、增加MCTS的模拟次数（Rollouts）和每个动作的输出序列数（$n$）来实现**推理计算规模化**。
    - 提出**计算最优策略**：识别出某些动作（如SAY和QT）对生成多样性更敏感，为其分配更多采样资源（如$n_{a1,a4}=3$），而对其他动作（如RA, DA, SA）的采样输出保持不变，从而高效利用计算资源。
- **灵活架构（Flexible Architecture）**：可插拔式的架构允许将其他先进技术（如IterDRAG）作为额外的动作分支集成到框架中。
- **最优答案选择**：
    - 设计了基于**Jaccard相似度**和**文本嵌入余弦相似度**的自洽性验证方法，从多路径中聚类并评分。
    - 研究了利用**SA动作进行自我精炼**和训练一个**过程监督奖励模型（QwenRM）** 两种方式来选择最优推理轨迹。

### 3. 实验设计
- **数据集**：覆盖**开放域QA**和**多跳QA**，具体包括：
    - 多跳QA：**HotpotQA, MuSiQue, 2WikiMultiHopQA**。
    - 单跳QA：**Natural Questions (NQ), TriviaQA, PopQA, WebQA**。
- **基准方法（Baselines）**：
    - **基础方法**：ZeroShot QA, Vanilla RAG。
    - **迭代/智能体RAG**：IterDRAG, Search-o1, ReSearch, DeepResearcher。
    - **其他RAG优化**：Iter-RetGen, Self-RAG, Auto-RAG。
- **评价指标**：主要使用**F1分数**和**准确率（Acc）**，部分实验报告了召回率（Recall）。
- **基础模型**：Qwen2.5系列（7B, 14B, 32B），Qwen3-235B，以及Llama3-8B-Instruct。

### 4. 资源与算力
- 论文中**未明确提及**所使用的GPU型号、数量或具体的训练/推理时长。
- 文中仅提到训练奖励模型时，从每个数据集采样了8,000个问答对，生成了超过156,000条推理路径（设置：rollouts=32, n=4）。此外，推理阶段通过调整如`Lmax`（最大上下文长度）等参数进行推理计算量的伸缩，但没有给出绝对的计算开销（如GPU小时）。

### 5. 实验数量与充分性
- **实验规模较大且多维度**，可以认为是充分的：
    - **多数据集评估（Main Results）**：在5个大型QA数据集上，与多达9种基线方法对比，并在5种不同规模的LLMs（7B, 14B, 32B, 235B non-thinking/thinking）上验证。
    - **推理计算规模化实验（Scaling Analysis）**：系统地考察了检索文档数、有效上下文长度、MCTS模拟次数、输出序列数等变量对性能的影响，并绘制了缩放曲线。
    - **消融研究（Ablation Studies）**：
        1. **计算最优策略**：对比不同动作分配不同采样数（$n$）及采样超参数调整（$q_{div}$）的效果。
        2. **数据库规模**：探究了文档数据库大小对性能的影响。
        3. **验证方法**：对比了平均法、Jaccard相似度、文本嵌入、SA自我精炼和QwenRM奖励模型这五种答案选择方法的性能。
    - **效率分析**：在HotpotQA上对比了Vanilla RAG、IterDRAG及AirRAG的端到端推理时间和检索时间。
- **客观性与公平性**：对比基线包含了当时最新的迭代和智能体RAG方法，部分结果有复现，比较公平。实验在多个公开数据集上进行，并使用了统一的外部知识库（Wikipedia dump），具有客观性。

### 6. 论文的主要结论与发现
- **性能优越性**：AirRAG在多种规模的LLMs和QA数据集上，均一致且显著地优于现有迭代式或智能体式RAG方法，尤其在复杂的多跳推理任务（如图MuSiQue）上提升明显。
- **推理规模化有效**：随着检索文档数、上下文长度或MCTS角色次数等计算资源的增加，模型性能（F1, Acc）呈现出一致的增益（推断规模化定律）。
- **计算最优分配关键**：通过对SAY和QT等关键动作分配更多样化的采样（增加`n`和使用贪婪采样策略），可以用更少的无效计算获得更好的性能。
- **架构灵活且可扩展**：AirRAG的树状搜索架构和可插拔设计使其能够轻松集成其他现有方法（如AirRAG-Blender），并获得进一步的性能提升。
- **多样化的候选答案选择**：在多个候选推理路径中，使用LLM的精炼能力（SA动作）或训练一个过程监督奖励模型，其效果优于简单的答案平均或相似度聚合方法。

### 7. 优点
- **方法论创新**：巧妙地将MCTS引入RAG的推理过程中，将一次性生成转变为可控的、树状空间的自主探索，有效解决了链式推理解空间狭窄的痛点。
- **动作空间设计**：定义的五种动作简洁、可解释性强，且覆盖了RAG场景下的主要思考模式，具有良好的通用性。
- **全面的实验验证**：从性能对比、缩放规律、消融研究到效率分析，实验设计非常扎实、系统性强，为方法的有效性提供了多维度的证据。
- **实用性强**：方法不依赖于特定模型的微调（训练奖励模型是可选项），可直接应用于不同规模的LLM，并且提供了AirRAG-Lite等简化版本，平衡了性能与效率。

### 8. 不足与局限
- **计算开销未量化**：虽然讨论了相对的计算分配策略和推理效率，但缺少与基线方法的**绝对计算成本（如GPU时/ FLOPs）** 对比，这使得“推理规模化”带来的收益难以从成本角度进行完整的评估。
- **奖励模型训练成本高**：最优的验证方法（QwenRM）需要合成高质量的过程监督数据进行指令微调，这带来了额外的数据构造和模型训练成本，限制了其即时应用。
- **超参数敏感性**：树搜索的深度、模拟次数、UCT中的平衡权重`w`等超参数，以及动作空间的执行逻辑（如哪些动作可并行）均需人工设定，方法的自动化与自适应能力有待提升。
- **应用场景局限**：实验主要在QA数据集上进行的，尽管覆盖了多跳推理，但在更广泛的、需要长程规划和多工具调用的复杂Agent任务上的效果尚待验证。

（完）
