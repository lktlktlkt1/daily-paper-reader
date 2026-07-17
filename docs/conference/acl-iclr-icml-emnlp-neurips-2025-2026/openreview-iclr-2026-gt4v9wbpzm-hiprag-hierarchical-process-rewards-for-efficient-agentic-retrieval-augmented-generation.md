---
title: "HiPRAG: Hierarchical Process Rewards for Efficient Agentic Retrieval Augmented Generation"
title_zh: HiPRAG：面向高效智能体检索增强生成的层次过程奖励
authors: "Peilin Wu, Mian Zhang, Kun Wan, Wentian Zhao, Kaiyu He, Xinya Du, Zhiyu Chen"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=Gt4v9WBPzm"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 引入层次过程奖励训练智能体RAG系统，避免过度搜索与搜索不足
tldr: 智能体RAG系统普遍存在过度搜索和搜索不足等次优行为，传统基于结果奖励的强化学习难以精细调控。HiPRAG提出层次过程奖励机制，将搜索过程细分为多个子步骤并赋予不同粒度的奖励信号，从而引导智能体学会何时应检索、何时可依赖已有知识。实验表明，该方法能显著减少冗余检索动作，同时提升最终答案的准确性与鲁棒性，为高效智能体RAG训练开辟了新路径。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 智能体RAG存在次优搜索行为（过度搜索与搜索不足），现有结果奖励缺乏细粒度控制。
method: 设计层次过程奖励机制，通过强化学习优化智能体RAG的搜索决策。
result: 显著减少不必要的检索开销，提高回答可靠性。
conclusion: 层次过程奖励能有效调控智能体RAG的搜索效率与质量。
---

## Abstract
Agentic Retrieval-Augmented Generation (RAG) is a powerful technique for incorporating external information that Large Language Models (LLMs) lack, enabling better problem solving and question answering. However, suboptimal search behaviors exist widely, such as over-search (retrieving information already known) and under-search (failing to search when necessary), which leads to unnecessary overhead and unreliable outputs. Current training methods, which typically rely on outcome-based rewards in a Reinforcement Learning (RL) framework, lack the fine-grained control needed to address these inefficiencies. To overcome this, we introduce $\textbf{Hi}$erarchical $\textbf{P}$rocess Rewards for Efficient agentic $\textbf{RAG}$ (HiPRAG), a novel training methodology that incorporates a fine-grained, knowledge-grounded process reward into the RL training. Our approach evaluates the necessity of each search decision on-the-fly by decomposing the agent's reasoning trajectory into discrete, parsable steps. We then apply a hierarchical reward function that provides an additional bonus based on the proportion of optimal search and non-search steps, on top of commonly used outcome and format rewards. Experiments on the Qwen2.5 and Llama-3.2 models across seven diverse QA benchmarks show that our method achieves average accuracies of 65.4\% (3B) and 67.2\% (7B), outperforming strong agentic RAG baselines. This is accomplished while dramatically improving search efficiency, reducing the over-search rate from over 27\% in baselines from previous work to just 2.3\% and concurrently lowering the under-search rate. These results demonstrate the efficacy of optimizing the reasoning process itself, not just the final outcome. Further experiments and analysis demonstrate that HiPRAG shows good generalizability across a wide range of RL algorithms, model families, sizes, and types. This work demonstrates the importance and potential of fine-grained control through RL, for improving the efficiency and optimality of reasoning for search agents.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：智能体检索增强生成（Agentic RAG）系统在实际应用中普遍存在两类次优搜索行为——**过度搜索**（检索模型已掌握的知识）和**搜索不足**（需要检索时却做出不搜索的决策）。这些行为不仅造成算力与时间浪费，还会损害最终回答的可信度。
- **研究背景**：当前主流的训练框架通常依赖基于最终结果的强化学习奖励（outcome-based rewards），这种粗粒度的奖惩信号很难对搜索过程中的每一个微观决策进行有效调控，因而难以根治上述问题。
- **整体含义**：本文指出，仅关注“最终答案对不对”是不够的，必须对“思考过程中何时该搜索、何时不该搜索”施加**细粒度、结构化的奖励信号**。由此提出 HiPRAG，意图通过优化推理过程本身，提升搜索智能体的效率与决策最优性。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将智能体的推理轨迹分解为一系列离散、可解析的子步骤，对每一步的搜索必要性进行实时评估，并据此提供层次化的过程奖励（hierarchical process rewards）。在强化学习训练中，除了常用的结果奖励和格式奖励外，额外加入基于**最优搜索步骤比例**的奖励项，从而引导模型学会在“该搜的时候搜，不该搜的时候不搜”。
- **关键技术细节**：
    - **轨迹分解**：将模型的多步推理过程切分为可独立判定“是否需要检索”的原子步骤。
    - **搜索必要性评估**：在每一步根据当前上下文与已有知识（knowledge‑grounded）判断是否应当发起检索。
    - **层次奖励函数**：定义一个层次化奖励，其值取决于整个轨迹中“最优搜索与非搜索步骤”所占的比例（即给那些检索决策正确的步骤更多的鼓励）。该奖励叠加在传统的结果奖励和格式奖励之上。
    - **强化学习训练**：在 RL 框架中综合以上奖励信号，对策略进行优化。该过程不依赖特定 RL 算法，可与多种算法兼容。

## 3. 实验设计：数据集、benchmark 与对比方法

- **评估场景与数据集**：在 **7 个多样化的问答 benchmark** 上进行测试（原文未列出具体数据集名称，但强调覆盖了不同领域和难度的知识密集型问答任务）。
- **使用模型**：主要实验在 **Qwen2.5（3B 和 7B）** 和 **Llama‑3.2（3B 和 7B）** 两个家族的不同规模模型上进行。
- **对比方法**：与 **多个强智能体 RAG 基线** 进行比较（包括先前工作中依赖结果奖励的训练方案）。指标包含**准确率、过度搜索率、搜索不足率**等，以全面衡量最终效果和搜索效率。

## 4. 资源与算力

- 原文未明确说明训练所用的 GPU 型号、卡数或具体训练时长。Meta‑review 与摘要中均无相关算力细节披露。只能推测实验涉及多个 3B/7B 模型的强化学习训练，通常需要一定规模的高性能 GPU 集群，但精确信息缺失。

## 5. 实验数量与充分性

- **主要实验**：在 2 个模型家族 × 2 个规模 × 7 个数据集上进行了核心评估，并与多个强基线对比。至少包含 **28 组主实验**（不同模型‑数据集组合）。
- **补充分析**：文中进一步测试了 HiPRAG 在不同强化学习算法、不同模型家族、不同规模以及不同模型类型上的泛化能力，说明有额外的跨算法、跨模型实验。
- **消融与深入分析**：包含对过度搜索率、搜索不足率的细致度量，以及过程奖励各层次作用的分析（可根据 Abstract 中 “further experiments and analysis” 推断有消融实验）。
- **充分性评价**：整体实验覆盖面较广，对比基线有力，同时兼顾效率与效果指标，具有较强的客观性和公平性。但由于未能看到完整论文，无法确认是否在超参调优、随机种子等方面做到了完全对等，初步判断实验设计较为严谨。

## 6. 论文的主要结论与发现

- HiPRAG 在多个 QA 基准上取得 **平均准确率 65.4%（3B）和 67.2%（7B）**，优于现有强 Agentic RAG 基线。
- **搜索效率大幅提升**：将过度搜索率从先前的 27% 以上 **锐减至 2.3%**，同时降低了搜索不足率，实现了“搜得更准，搜得更少”。
- 该方法不仅提升最终答案质量，也显著减少不必要的检索开销，证明 **优化推理过程本身（而不仅仅是最终结果）** 对于搜索智能体的效率和最优性至关重要。
- HiPRAG 在多种 RL 算法、模型家族、规模和类型上展现出良好的 **泛化能力**，表明细粒度过程控制是一条普适性强的技术路线。

## 7. 优点：方法或实验设计上的亮点

- **直觉清晰且可操作性强**：将搜索决策优化视为一个层次化过程奖励问题，直接针对实际系统中的“过度搜索/搜索不足”痛点。
- **与模型和算法解耦**：奖励设计不绑定特定 RL 算法或特定架构，可以灵活嵌入到现有训练流水线中。
- **多维评价指标**：不仅关注准确率，还引入过度搜索率、搜索不足率，更全面地刻画智能体 RAG 的行为质量。
- **良好的泛化验证**：跨模型家族、跨规模、跨 RL 算法的实验设计，增强了结论的可信度。
- **开创新的优化范式**：从“奖励好答案”转向“奖励好的检索动作序列”，可能推动后续过程监督学习方法在检索智能体上的应用。

## 8. 不足与局限

- **原文内容受限**：仅从摘要和元数据推断，未能查阅完整论文，因此对实验细节（如数据集名称、基线实现、超参设置）的了解不足，可能存在遗漏或偏差。
- **算力成本不明**：没有给出训练资源消耗，无法评估该方法在实际落地中的计算门槛。
- **任务覆盖面**：仅测试了问答类 benchmark，对于多步交互、动态环境或更开放域的任务表现尚不清楚。
- **过程奖励的设计依赖人工分解**：将推理轨迹分解为步骤并判断搜索必要性，可能需要一定的先验知识或启发式规则，在超复杂任务上的自动化和可扩展性有待验证。
- **潜在偏差风险**：未提及奖励函数中 “最优搜索比例” 的阈值是如何确定的，如果阈值设定不当，可能导致模型偏向保守搜索或激进不搜索，存在调参敏感的可能。

（完）
