---
title: "Search Wisely: Mitigating Sub-optimal Agentic Searches By Reducing Uncertainty"
title_zh: 明智搜索：通过降低不确定性缓解次优智能体搜索
authors: "Peilin Wu, Mian Zhang, Xinlu Zhang, Xinya Du, Zhiyu Chen"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.998.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 通过关联模型不确定性来缓解智能体RAG中的过度搜索和搜索不足
tldr: "智能体RAG中时常出现过度搜索与搜索不足的问题，但缺乏系统性的分析与解决方案。本文首次对这两种次优行为进行形式化定义与量化，发现其与模型对自身知识边界的不确定性高度相关。基于此提出一种不确定性感知的搜索策略，通过在生成过程中实时评估置信度并动态调整搜索动作，显著减少了无效检索步骤。在多个问答数据集上的实验表明，该方法可将不必要的搜索降低27.7%，同时维持或提升回答质量。"
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.998/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 810, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.998/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 797, \"height\": 421, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.998/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 794, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.998/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 726, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.998/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 791, \"height\": 1028, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.998/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.998/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1492, \"height\": 506, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.998/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1569, \"height\": 844, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.998/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 807, \"height\": 411, \"label\": \"Table\"}]"
motivation: 智能体RAG存在过度搜索和搜索不足，影响效率和可靠性。
method: 形式化定义次优搜索行为，分析其与不确定性的关联，提出减少不确定性的搜索策略。
result: "在多个QA数据集上，27.7%的搜索步骤本可避免，优化后显著提升效率。"
conclusion: 控制模型不确定性是提升智能体RAG搜索质量的关键。
---

## Abstract
Agentic Retrieval-Augmented Generation (RAG) systems enhance Large Language Models (LLMs) by enabling dynamic, multi-step reasoning and information retrieval. However, these systems often exhibit sub-optimal search behaviors like over-search (retrieving redundant information) and under-search (failing to retrieve necessary information), which hinder efficiency and reliability. This work formally defines and quantifies these behaviors, revealing their prevalence across multiple QA datasets and agentic RAG systems (e.g., one model could have avoided searching in 27.7% of its search steps). Furthermore, we demonstrate a crucial link between these inefficiencies and the models’ uncertainty regarding their own knowledge boundaries, where response accuracy correlates with model’s uncertainty in its search decisions. To address this, we propose β-GRPO, a reinforcement learning-based training method that incorporates confidence threshold to reward high-certainty search decisions. Experiments on seven QA benchmarks show that β-GRPO enable a 3B model with better agentic RAG ability, outperforming other strong baselines with a 4% higher average exact match score.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：当前智能体检索增强生成（Agentic RAG）系统虽然能实现多步推理与动态检索，但普遍存在两类次优搜索行为：
  - **过度搜索（over‑search）**：模型检索了自身参数知识已能回答的信息，造成冗余。
  - **搜索不足（under‑search）**：模型在应当进行外部检索时未检索，导致幻觉或错误。
- **研究动机**：这些行为严重影响系统的效率与可靠性，但缺乏系统化的定义、量化与根因分析。本文旨在补齐这一空白，并通过降低模型在检索决策中的不确定性来缓解问题。

## 2. 论文提出的方法论

- **形式化定义次优搜索**：
  - 将一次推理轨迹划分为若干步骤 \(s_t\)，区分“检索步”与“非检索步”。
  - **过度搜索**：若某检索步的答案可通过仅依靠内部知识和先前上下文得到，则判定为过度搜索。
  - **搜索不足**：若非检索步生成的答案与真实答案不一致，则判定为搜索不足。
- **核心思想**：
  - 实验发现，模型在生成搜索查询时的置信度（最低token概率）与最终答案正确率正相关，表明搜索决策的不确定性是次优搜索的关键因素。
  - 提出 **β‑GRPO**：在 GRPO 训练框架中引入置信度阈值，仅当**搜索调用的置信度超过阈值 β 且最终答案正确**时，才给予正向奖励，从而抑制低置信度的搜索决策，增强模型对知识边界的认知。
- **关键公式**：
  - 奖励函数 \(R(T) = 1\) 当且仅当 \(a_f = a_f^*\) 且 \(C(T) > \beta\)，否则为 0。
  - 置信度 \(C(T) = \min_{s_t^R \in T, w \in q_t} P(w)\)，即轨迹中所有搜索查询 token 的最低生成概率。
- **训练流程**：基于 Qwen2.5‑3B，使用已训练好的 Search‑R1 权重初始化，继续用 β‑GRPO 进行强化学习训练。

## 3. 实验设计

- **数据集与基准**：
  - 训练集：Natural Questions (NQ) 与 HotpotQA 的混合训练集。
  - 评估集：7 个问答基准，包括通用 QA（NQ, TriviaQA, PopQA）和多跳 QA（HotpotQA, 2WikiMultiHopQA, Bamboogle, MuSiQue）。
  - 评价指标：精确匹配（Exact Match, EM）。
- **对比方法**：
  - 无检索方法：直接提示、CoT 提示、SFT、R1（仅 RL 微调）。
  - 非智能体检索：RAG、IRCoT。
  - 智能体检索：Search‑o1、Search‑R1（PPO）、Search‑R1‑GRPO（继续用 GRPO 训练）。
- **消融实验**：比较不同置信度阈值 β = 0.2, 0.4, 0.6 的效果。
- **行为分析实验**：
  - 步骤级过度搜索率与搜索不足率分析（通过提示模型“仅用自身知识回答”以及与强大模型比对）。
  - 搜索次数与数据集标注推理跳数的对比分析。

## 4. 资源与算力

- 训练使用 **两块 A100 GPU**。
- 共训练 **200 个 step**，学习率 1e‑6，批次大小为 512。
- 每道题生成 5 个候选轨迹用于 GRPO 组内比较。
- 检索器基于 2018 Wikipedia dump，使用 E5 模型，每次搜索返回 top‑3 文档。
- 未报告具体训练时长。

## 5. 实验数量与充分性

- **主要实验**：1 套主结果表（7 数据集 × 多组基线），充分覆盖不同任务类型和方法。
- **消融实验**：3 组不同 β 值的对比，验证超参选择。
- **行为分析实验**：
  - 步骤级过度搜索与搜索不足量化分析（R1‑Searcher 和 Search‑R1 在两个模型上的统计）。
  - 搜索次数与标注跳数对比分析（2 个数据集）。
  - 置信度与正确率的相关性表格（4 个数据集 × 4 种模型变体）。
- **案例分析**：展示模型在减少过度搜索和搜索不足上的具体改进。
- **总体评价**：实验设计较为全面，覆盖多种场景和角度，对比基线丰富，消融和分析能够支撑结论；使用统一的检索器和评估协议，具备客观性与公平性。

## 6. 论文的主要结论与发现

- **次优搜索普遍存在**：例如 Search‑R1 有 27.7% 的搜索步可被省略；R1‑Searcher 在非搜索步的错误率高达 63%，指示严重搜索不足。
- **不确定性是根源**：生成搜索查询的最小 token 概率越高，最终答案的正确率也越高，说明搜索决策的不确定性直接影响性能。
- **β‑GRPO 有效**：使 3B 模型在 7 个 QA 基准上平均 EM 提升约 4%，且过度搜索率从 21.10% 降至 19.89%，搜索不足率从 42.04% 降至 34.71%。
- **训练稳定性提升**：β‑GRPO 的奖励曲线比普通 GRPO 更高且更稳定。
- **案例分析证实**：模型能更自信地判断已知事实（避免搜索）和未知实体（主动搜索），减少冗余检索和幻觉。

## 7. 优点

- **首次系统量化**：给出了 over‑search 和 under‑search 的严格定义及自动化检测流程，为该问题提供了分析基准。
- **深入的根因分析**：将行为缺陷与模型置信度关联，洞察到位。
- **改动简洁有效**：仅在 GRPO 奖励中增加置信度阈值，无需额外标注或复杂模型结构，易于实现和迁移。
- **实验设计扎实**：覆盖 7 个数据集、多种强基线、详细的步骤分析、消融和案例，结论可信度高。
- **开源承诺**：已公开代码，有利于复现和后续研究。

## 8. 不足与局限

- **模型规模限制**：仅基于 3B 模型进行实验，未扩展到更大规模模型（如 7B、13B），结论的泛化性有待验证。
- **任务类型单一**：所有评估均为事实型问答，未涉及更开放或需要多轮交互的任务（如深度研究、对话式检索）。
- **置信度度量简单**：仅采用搜索查询的最小 token 概率，可能过于粗糙，无法完全捕捉模型真正的认知不确定性。
- **阈值依赖人工设定**：β 值通过简单搜索确定，缺乏自适应机制，在不同场景下可能需要重新调整。
- **分析依赖外部模型**：步骤提取和答案等价判断使用外部 LLM（如 QwQ‑32B 和 GPT‑4o），可能引入评估偏差。
- **训练代价**：仍需对模型进行 RL 训练，相比直接提示等方法有额外的计算开销。

（完）
