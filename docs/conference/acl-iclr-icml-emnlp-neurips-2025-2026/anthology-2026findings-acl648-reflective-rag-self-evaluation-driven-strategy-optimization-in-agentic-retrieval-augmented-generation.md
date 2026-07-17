---
title: "Reflective RAG: Self-Evaluation Driven Strategy Optimization in Agentic Retrieval-Augmented Generation"
title_zh: 反思式RAG：基于自我评估的智能体检索增强生成策略优化
authors: "Haiyan Wu, Chenchen Wang, Chaoqun Sun, Chengxiong Lu, Yan-Hong Chen, Zhiqiang Zhang, Xiaoqing Feng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.648.pdf"
tags: ["query:agentic-rag"]
score: 10.0
evidence: 智能体RAG中通过反思标签机制进行自评估驱动的策略优化
tldr: 现有智能体RAG缺乏对检索内容效用的评估，导致决策脆弱。本文提出Reflective RAG，核心创新在于引入反思标签机制，使模型能够批判检索内容的相关性，并据此动态调整检索与生成策略，通过两阶段训练确保稳健学习。结果表明，自我评估驱动的优化显著提升了多轮推理的质量和稳定性，为构建更可靠的智能体RAG系统奠定了基础。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.648/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 794, \"height\": 708, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.648/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1634, \"height\": 1221, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.648/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 783, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.648/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.648/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 798, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.648/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 793, \"height\": 489, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.648/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1625, \"height\": 938, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.648/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1631, \"height\": 443, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.648/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 779, \"height\": 287, \"label\": \"Table\"}]"
motivation: 智能体RAG缺乏检索效用评估，推理决策容易出错。
method: 提出反思标签机制，使模型批判检索内容并动态调整策略。
result: 两阶段训练使多轮推理更加稳健高效。
conclusion: 自我评估是提升智能体RAG决策质量的关键。
---

## Abstract
Retrieval-Augmented Generation (RAG) has emerged as a widely adopted paradigm for grounding Large Language Models (LLMs) in external knowledge. Recent agentic RAG systems introduce multi-turn reasoning, but they often lack the capacity to evaluate the utility of retrieved information, leading to brittle reasoning and suboptimal decision-making. We propose Reflective RAG, an agentic framework that incorporates self-evaluation to dynamically optimize retrieval and generation strategy. At its core, Reflective RAG employs a reflection tagging mechanism that allows the model to critique the relevance of retrieved content, thereby explicitly guiding its subsequent policy. To ensure robust learning, we introduce a two-stage training procedure that partially decouples evaluation semantics from strategy optimization. First, during supervised fine-tuning (SFT), the model learns to generate accurate reflection signals by self-correcting labels based on internal uncertainty. Second, a reinforcement learning (RL) stage optimizes the agent’s strategy using these reflections, stabilized by dynamic KL regularization. Evaluations across five knowledge-intensive QA benchmarks demonstrate that Reflective RAG consistently outperforms strong agentic baselines. Further analysis demonstrates its improved training stability and stronger generalization to complex multi-hop reasoning tasks.

---

## 论文详细总结（自动生成）

# Reflective RAG论文详细总结

## 1. 论文的核心问题与整体含义
- **研究动机**：检索增强生成（RAG）已成为将大语言模型（LLM）与外部知识结合的主流范式。然而，现有的**智能体RAG（Agentic RAG）系统**虽然引入了多轮推理，但普遍缺乏对检索信息效用进行有效评估的能力。
- **核心问题**：这种评估能力的缺失导致推理过程脆弱，容易受到冗余或误导性信息干扰，从而做出**次优决策**，尤其在高不确定性的多跳推理场景中，模型可能过早给出最终答案。
- **整体含义**：论文提出**Reflective RAG框架**，旨在通过引入**自我评估（Self-Evaluation）机制**，让模型能够动态地评判检索内容的质量，并据此显式地优化后续的检索与生成策略，最终构建更可靠、更稳定的智能体RAG系统。

## 2. 论文提出的方法论
- **核心思想**：将检索内容的评估建模为一个可训练的结构化组件——**反思标签（Reflection Tags）**机制。模型在每一步检索后，对返回的信息标注“有用（Useful）”、“冗余（Redundant）”或“混淆（Confusing）”，该标签直接约束后续的策略决策。
- **关键技术细节与流程**（两阶段训练）：
    - **阶段一：监督微调（SFT）**
        - **轨迹采样与过滤**：基座模型生成多轮检索推理轨迹，仅保留格式正确且答案正确的轨迹。
        - **评估标签自校正**：利用**内部困惑度（Perplexity, PPL）变化**信号ΔPPL（即移除某检索信息后生成正确答案的PPL变化量）来评判检索信息的真实效用，并基于分位数分布自动修正初始评估标签。这无需外部专家模型。
        - **评估感知轨迹重建**：根据修正后的标签（有用/冗余/混淆），用不同的提示模板引导模型重新采样后续推理步骤，构建高质量的对齐数据集。
    - **阶段二：强化学习（RL）**
        - **优化算法**：采用**组相对策略优化（GRPO）**。
        - **评估引导的策略约束**：在 rollout 过程中，若检索信息被模型标记为“混淆”但其仍试图直接生成最终答案，则强制执行至少一次额外的检索步骤，防止过早终止。
        - **评估感知的KL正则化**：引入混合KL散度项，对`<evaluation>`段落内的tokens施加更大的初始KL权重（`α0`），以保持评估语义的稳定性，且该权重随训练步数**线性衰减**，逐步放宽约束，增强后期的策略自适应能力。对其他tokens使用较小的固定KL权重β。
        - **奖励设计**：仅使用由答案正确性和格式合规性组成的稀疏轨迹级奖励，避免直接奖励评估标签而导致奖励黑客。

## 3. 实验设计
- **数据集与场景**：在五个知识密集型问答基准上评测，覆盖不同类型的推理场景。
    - **开放域问答**：Natural Questions (NQ), WebQuestions (WebQ)
    - **多跳推理问答**：2WikiMultiHopQA (2WikiMHQ), HotpotQA, MuSiQue
- **评测指标**：主要指标为严格**精确匹配（Exact Match, EM）**，并辅以F1分数提供细粒度评估。
- **基座模型**：Qwen2.5-3B-Instruct 和 Qwen2.5-7B-Instruct。
- **对比方法**：覆盖多种范式的基线模型。
    - **推理基线**：Chain-of-Thought (CoT)
    - **静态RAG基线**：Vanilla RAG
    - **自适应RAG基线**：Self-RAG（使用外部专家模型的反思令牌）、Search-o1（多轮检索但无RL优化）
    - **RL优化的智能体RAG基线**：s3（低数据RL）、Search-R1（基于最终答案正确性的RL训练）

## 4. 资源与算力
- **硬件配置**：所有实验在**单个节点配备4块80GB显存的GPU**上完成。
- **框架与训练细节**：SFT使用LLaMA-Factory，RL使用verl框架。
    - SFT阶段：训练1个epoch，总batch size为256，学习率2e-6。
    - RL阶段：训练300步，使用vLLM进行rollout采样（每条prompt采样5条轨迹），总batch size 256，学习率5e-7。文中未明确提及具体GPU型号（如A100）或总训练时长。

## 5. 实验数量与充分性
实验设计全面，包含多组对照分析，较为充分、客观和公平。
- **主实验**：在不同参数量（3B/7B）、五个数据集上与6个基线模型进行性能对比，生成一张详细的主结果表。
- **消融实验**：完整验证框架内各关键组件的贡献，包括仅SFT、无标签校正与轨迹重建、无RL策略约束、无评估KL正则化等变体。
- **定量分析**：通过多组实验深入分析框架特性，包括推理时策略约束的影响、平均检索步数对比、不同评估KL系数对训练熵和最终性能的影响。
- **训练稳定性**：展示了不同模型规模下RL训练过程中的奖励曲线。

## 6. 论文的主要结论与发现
- **性能优越性**：Reflective RAG在五个基准数据集上**一致地优于所有强基线模型**。在3B和7B参数量下，平均EM和F1相对于最优基线均有稳定提升。
- **RL与内部对齐的重要性**：对于复杂的多跳检索推理，基于RL的优化效果显著优于纯SFT。完全依赖内部信号的自评估机制可以替代昂贵的外部专家模型，实现内部一致的策略学习。
- **组件协同价值**：SFT阶段的标签校正与轨迹重建，与RL阶段的策略约束和动态KL正则化，均为系统稳定性和最终性能的关键贡献因素。三者协同实现了可靠的自评估引导推理。
- **自适应检索行为**：Reflective RAG能够根据自评估信号自适应调节检索频率，而非盲目增加或减少检索次数，在不同模型规模下均实现更优的性能-效率权衡。

## 7. 优点
- **新颖的自监督评估机制**：利用内部PPL变化量校正评估标签，完全自给自足，不依赖外部专家标注。
- **评估与策略的深度耦合**：首次将自我评估显式建模为一个可训练的组件，并作为策略约束直接融入多轮推理的RL优化中，而非作为被动监控信号。
- **稳定训练设计**：提出的评估感知动态KL正则化有效平衡了评估语义的保持与策略的适应性，避免了奖励黑客。
- **理论与实践结合紧密**：通过详尽的消融实验和定量分析，清晰地证明了每个设计选择的必要性和有效性。

## 8. 不足与局限
- **模型规模验证有限**：实验仅在3B和7B的中小规模模型上进行，未在更大规模模型（如13B、30B或更大）上验证框架的泛化性。
- **评估粒度较粗**：反思标签仅分为三类，可能无法处理更细粒度的证据质量差异，尤其是在一步检索返回多个文档时。
- **无法直接优化评估信号**：为避免奖励黑客，评估标签未作为直接奖励项，因此模型优化评估能力的方式是间接的，可能不是最有效的。
- **环境设定简化**：实验设定为每步检索返回单个文档，其结论在更复杂的多文档检索场景下的普适性有待验证。

（完）
