---
title: "AutoSearch: Adaptive Search Depth for Efficient Agentic RAG via Reinforcement Learning"
title_zh: AutoSearch：基于强化学习的高效代理式RAG自适应搜索深度
authors: "Jingbo Sun, Wenyue Chong, Songjun Tu, Qichao Zhang, Yaocheng Zhang, Jiajun Chai, Xiaohan Wang, Wei Lin, Guojun Yin, Dongbin Zhao"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1399.pdf"
tags: ["query:agentic-rag"]
score: 10.0
evidence: 通过强化学习自适应搜索深度，平衡代理RAG多步交互的准确性与效率
tldr: 针对代理式RAG多步交互中存在冗余搜索的问题，提出AutoSearch框架。首次分析问题复杂度与代理能力共同决定的最小充分搜索深度，并利用强化学习动态决定每题的搜索步数。在多个知识密集任务上实现精度与效率的最佳平衡，显著减少了不必要的检索开销。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1399/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 788, \"height\": 649, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1399/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1521, \"height\": 622, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1399/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1659, \"height\": 950, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1399/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 784, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1399/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 722, \"height\": 423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1399/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1640, \"height\": 1018, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1399/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1542, \"height\": 1393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1399/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 821, \"height\": 718, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1399/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1539, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1399/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1434, \"height\": 426, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1399/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1382, \"height\": 518, \"label\": \"Table\"}]"
motivation: 代理RAG多步搜索常包含冗余步骤，固定步数限制则无法应对难题，需要自适应机制。
method: 建模最小充分搜索深度，并使用强化学习训练智能体自适应决定每题的搜索步数。
result: 在保持高准确率的同时大幅削减了冗余搜索步骤，达到了效率和精度双优。
conclusion: AutoSearch为代理RAG的实际部署提供了成本可控的智能搜索策略，推进了自主代理系统的实用性。
---

## Abstract
Agentic retrieval-augmented generation (RAG) systems enable large language models (LLMs) to solve complex tasks through multi-step interaction with external retrieval tools. However, such multi-step interaction often involves redundant search steps, incurring substantial computational cost and latency. Prior work limits search depth (i.e., the number of search steps) to reduce cost, but this often leads to underexploration of complex questions. To address this, we first investigate how search depth affects accuracy and find a minimal sufficient search depth that defines an accuracy-efficiency trade-off, jointly determined by question complexity and the agent’s capability. Furthermore, we propose AutoSearch, a reinforcement learning framework that evaluates each search step via self-generated intermediate answers. By a self-answering mechanism, AutoSearch identifies the minimal sufficient search depth and promotes efficient search by rewarding its attainment while penalizing over-searching. In addition, reward mechanisms are introduced to stabilize search behavior and improve answer quality on complex questions. Extensive experiments on multiple benchmarks show that AutoSearch achieves a superior accuracy-efficiency trade-off, alleviating over-searching while preserving search quality.

---

## 论文详细总结（自动生成）

好的，这是根据您的要求生成的中文论文总结。

### 1. 论文的核心问题与整体含义

*   **研究背景与动机**：在代理式检索增强生成系统中，大型语言模型需要通过多步与外部工具交互来解决复杂问题。然而，这种多步交互往往包含冗余的搜索步骤，导致高昂的计算成本和延迟。
*   **核心问题**：现有方法通过限制搜索步数来降低成本，但这可能导致对复杂问题探索不足。因此，本文旨在回答一个关键问题：**代理能否在保持答案准确性的同时，自适应地调整到最小的搜索步数？**
*   **整体含义**：本文提出了一种在问题复杂度和模型自身能力之间取得平衡的机制，旨在实现代理式RAG系统的准确性与搜索效率帕累托最优，从而降低实际部署成本。

### 2. 论文提出的方法论

*   **核心思想**：提出**AutoSearch**，一个基于自我决策驱动的强化学习框架。它通过在每一步搜索后生成中间答案来评估当前搜索的有效性，从而自适应地达到“最小充分搜索深度”。
*   **关键技术细节**：
    *   **最小充分搜索深度**：被定义为智能体首次给出完全匹配正确答案时所处的搜索步数。该深度由问题复杂度和智能体能力共同决定。
    *   **中间答案生成机制**：在每个搜索步骤之后，模型会根据已有的所有轨迹信息生成一个中间答案，作为自我评估的信号。
    *   **奖励函数设计**：AutoSearch包含三种互补的奖励信号，用于PPO训练：
        *   **基础奖励**：包含用于约束输出结构的格式奖励，和基于最终答案匹配度的结果奖励，以稳定搜索过程并确保答案正确性。
        *   **搜索效率奖励**：根据中间答案识别的“最小充分搜索深度”，奖励在其之前进行的“有效搜索”步，惩罚在此之后的“过度搜索”步，且给予更短的充分深度以更高的奖励。
        *   **搜索质量奖励**：通过计算当前中间答案与之前最佳中间答案的F1分数增益，来量化每一步搜索带来的边际信息贡献，鼓励有意义的检索。
    *   **训练目标**：模型使用PPO算法进行训练，在计算损失时，会屏蔽掉从外部检索工具获得的观测token，仅对模型自身的推理和决策进行优化。

### 3. 实验设计

*   **数据集与场景**：实验覆盖了两大类共六个广泛使用的问答基准数据集：
    *   **单跳/通用问答**：Natural Questions、TriviaQA、PopQA
    *   **多跳问答**：HotpotQA、2WikiMultiHopQA、Bamboogle
*   **对比基准方法**：与多种基于强化学习的搜索方法进行了比较，包括**Search-R1**、**StepSearch**以及**HIPRAG**。
*   **评估指标**：
    *   **答案质量**：精确匹配和单词级别的F1分数。
    *   **搜索成本与效率**：搜索深度、搜索效率和过度搜索比率。
*   **训练与评估设置**：使用Qwen2.5-3B-Base和Qwen2.5-7B-Base两个基础模型进行实验，训练数据的检索语料库为2018年维基百科快照，使用E5检索器。

### 4. 资源与算力

*   **算力配置**：所有实验均在**单台配备八块NVIDIA H20 GPU**的计算节点上进行。
*   **训练参数**：总优化步数为1005步。Actor网络学习率为1e-6，Critic网络学习率为1e-5。总批次大小为512，PPO小批次大小为256。

### 5. 实验数量与充分性

*   **实验数量**：论文进行了较为全面的实验验证，包括：
    *   **主实验**：在3B和7B两个模型规模、六个数据集上，与三种基线方法进行全面对比。
    *   **分析性实验**：深入研究了搜索深度对性能和过度搜索的影响，并分析了问题复杂度和模型能力的影响。
    *   **消融实验**：在六个数据集上对三个奖励组件进行了消融研究。
    *   **进一步分析**：包括与不同RL算法（GRPO）的对比、训练动态分析以及多个案例研究。
*   **充分性与客观性**：实验设计充分、客观且公平。它覆盖了不同难度的任务和模型规模，使用了标准化的自动评估指标，并重新复现了所有基线方法以保证对比的公平性。消融实验也验证了各模块的必要性。

### 6. 论文的主要结论与发现

*   **准确性-效率权衡的根源**：首次通过实验发现并验证了“最小充分搜索深度”的存在，该深度由**问题复杂度**和**智能体能力**共同决定，是实现准确性-效率权衡的基础。
*   **AutoSearch的有效性**：所提出的AutoSearch框架能够在多种单跳和多跳问答任务中，持续性地以**更少的搜索步数**实现**更高或相当**的答案准确率，获得了最优的准确性-效率权衡。
*   **自适应深度调整**：AutoSearch并非简单地最小化搜索步数。它在简单问题上进行浅层搜索，在复杂问题上进行深层搜索，展现了根据问题特性动态调整搜索策略的能力。
*   **有效抑制过度搜索**：与基线方法相比，AutoSearch显著降低了过度搜索的样本比例，尤其是在模型性能退化明显的多跳任务上。
*   **奖励组件的协同作用**：消融研究证实，基础奖励、搜索效率奖励和搜索质量奖励三个组件对于平衡答案准确性和搜索效率都至关重要，缺一不可。

### 7. 优点

*   **问题洞见深刻**：不只是提出一个模型，而是深入分析了搜索深度与准确性之间的关系，并提出了由问题复杂度和模型能力共同决定的“最小充分搜索深度”这一核心概念。
*   **方法优雅且有效**：通过自我生成的中间答案来驱动学习，无需依赖外部模型或预定义的阈值来判断搜索是否冗余，使整个框架高度自包含。
*   **激励设计精巧**：奖励函数设计直接针对“最小充分深度”，既能激励高效搜索（找到该深度并给予更高奖励），又能惩罚过度搜索，有效引导模型学习到最优的搜索终止策略。
*   **实验全面扎实**：在多种数据集、模型规模和基线方法上进行了详尽的对比、消融和分析实验，结论信服力强。
*   **训练过程稳定**：通过PPO训练，AutoSearch在训练动态上表现出更快的收敛速度和更稳定的搜索行为。

### 8. 不足与局限

*   **搜索步数范围有限**：论文主要关注相对较低的最大搜索步数（例如，实验设置中最多4步）。在更宽泛的搜索深度下，该方法的有效性和平衡性仍有待探索。
*   **任务类型限制**：实验主要在知识密集型的单跳和多跳问答任务上进行。该方法在更开放、长程的代理任务（如多轮对话、需要网页浏览的交互式任务）中的泛化能力尚待验证。
*   **中间答案的噪声**：训练信号高度依赖于中间答案的质量。如果中间答案本身质量较差或不稳定，可能会影响效率奖励和质量奖励的准确性，从而误导学习过程。
*   **计算开销**：虽然减少了推理时的搜索步数，但在训练时，为每一步都生成中间答案会带来额外的计算开销。

（完）
