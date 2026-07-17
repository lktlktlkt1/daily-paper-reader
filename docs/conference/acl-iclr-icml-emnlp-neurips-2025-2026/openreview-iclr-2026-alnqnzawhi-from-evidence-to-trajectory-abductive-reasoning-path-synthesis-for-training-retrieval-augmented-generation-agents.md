---
title: "From Evidence to Trajectory: Abductive Reasoning Path Synthesis for Training Retrieval-Augmented Generation Agents"
title_zh: 从证据到轨迹：用于训练检索增强生成代理的溯因推理路径合成
authors: "Muzhi Li, Jinhu Qi, Yihong Wu, Minghao Zhao, Liheng Ma, Yifan Li, Xinyu Wang, Yingxue Zhang, Ho-fung Leung, Irwin King"
date: 2025-09-05
pdf: "https://openreview.net/pdf?id=alNQNzaWhI"
tags: ["query:agentic-rag"]
score: 10.0
evidence: 证据锚定的推理路径合成用于RAG代理训练
tldr: 本文针对RAG代理缺乏过程级监督、现有数据合成方法无法建模环境交互的问题，提出EviPath证据锚定的推理路径合成范式。该范式通过溯因子任务规划将问题分解为子任务，并模拟检索器调用等环境互动，生成带推理轨迹的合成数据。实验表明，使用EviPath合成的数据训练能显著提升RAG代理的任务分解和逐步决策能力，为智能体RAG开发提供了有效的数据生成方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: RAG代理缺乏过程级监督，现有合成数据无法建模环境交互。
method: 通过证据锚定和溯因规划合成推理路径，训练代理的任务分解与检索调用能力。
result: 合成数据训练的RAG代理在多步决策任务上表现显著提升。
conclusion: 证据锚定的推理路径合成为智能体RAG提供了有效训练数据。
---

## Abstract
Retrieval-augmented generation agents development is hindered by the lack of process-level supervision to effectively guide agentic capabilities like task decomposition, retriever invocation, and stepwise decision-making. While reinforcement learning offers a potential solution, it suffers from sparse rewards and the limited reasoning capabilities of large language models (LLMs). Meanwhile, existing data synthesis methods only produce chain-of-thought rationales and fail to model environmental interactions.
In this paper, we propose EviPath, an evidence-anchored reasoning path synthesis paradigm for RAG agent development. EviPath comprises: (i) Abductive Subtask Planning, which decomposes the problem into sub-questions and iteratively plans an optimal solution path based on the dependencies between them; (ii) Faithful Sub-question Answering, which uses supporting evidence to construct a proxy environment to generate reasoning thoughts and answers for each sub-question; and (iii) Conversational Fine-Tuning, which formats the complete agent-environment interaction trajectory into a dialogue format suitable for Supervised Fine-Tuning. EviPath allows LLMs to learn complex reasoning and tool-use capabilities directly from synthesized data. Extensive experiments on widely-used question-answering benchmarks show that an 8B parameter model trained with EviPath-synthesized data significantly and consistently outperforms state-of-the-art baselines with a double-digit absolute EM gain of 14.7% in open-domain question answering.

---

## 论文详细总结（自动生成）

# 论文总结：《From Evidence to Trajectory: Abductive Reasoning Path Synthesis for Training Retrieval-Augmented Generation Agents》

## 1. 核心问题与整体含义
- **研究背景**：检索增强生成 Agent（RAG Agent）需要具备任务分解、检索器调用与逐步决策等复杂能力，但训练这类 Agent 普遍缺乏**过程级监督信号**。
- **核心问题**：
  - 现有方法若使用强化学习，会面临奖励稀疏和 LLM 自身推理能力有限的困境。
  - 现有数据合成方法仅能生成思维链解释（CoT），无法模拟 Agent 与外部环境（如检索器）的真实交互轨迹。
- **整体含义**：论文提出一种**证据锚定的推理路径合成范式（EviPath）**，旨在生成包含完整 Agent-环境交互过程的合成数据，从而通过监督微调直接赋予 LLM 复杂的推理与工具使用能力，绕过强化学习的瓶颈。

## 2. 方法论
EviPath 的核心思想是**以原始问题所依赖的证据为锚点，逆向规划出最优推理轨迹**，包含三个关键步骤：

- **溯因子任务规划（Abductive Subtask Planning）**  
  将原始问题分解为多个子问题（sub-questions），基于子问题之间的逻辑依赖关系，**迭代地规划出一条最优的解决路径**。这里的“溯因”强调从最终需要的证据反推应依次回答哪些子问题。

- **忠实子问题回答（Faithful Sub-question Answering）**  
  利用支持证据构建一个**代理环境**（proxy environment），模拟真实检索器的行为。对每一步子问题，合成出对应的推理思考（thought）和答案，保证回答忠实于所提供的证据，从而生成可信的环境交互步骤。

- **对话式微调（Conversational Fine-Tuning）**  
  将上述完整的 Agent-环境交互轨迹（思维、行动、观察）**格式化为多轮对话**，直接用于 LLM 的监督微调（SFT），使模型学会在对话过程中逐步分解问题、调用检索并整合信息。

**核心算法流程（文字描述）**  
1. 输入：用户问题及参考证据集合。  
2. 规划阶段：分析证据间的支撑关系，将问题拆解为 `[q1, q2, ..., qn]`，按依赖排序形成路径。  
3. 回答阶段：依次处理每个子问题 `qi`，用证据模拟环境给出观察结果，并生成“思考-行动-观察”三元组。  
4. 格式化阶段：将完整序列转化为 `{"role": "user", ...}` `{"role": "assistant", "content": "thought: ..., <TOOL_CALL>..."}` 等标准对话格式。  
5. 使用合成数据对基础 LLM 进行 SFT，得到 EviPath-RAG Agent。

## 3. 实验设计
- **基准场景**：广泛使用的**开放域问答和多跳推理问答基准**（摘要提及 “widely-used question-answering benchmarks”，具体数据集未在给出的文本中列出，但通常包括 Natural Questions、TriviaQA、HotpotQA 等）。
- **对比方法**：与一系列**最先进的基线（state-of-the-art baselines）**进行比较（摘要未列出具体方法名，可能包括标准 RAG、基于 CoT 的合成数据训练方法、强化学习训练的 Agent 等）。
- **评估指标**：开放域问答采用精确匹配（EM）等进行评估，论文报告了 8B 模型在此指标上取得了 **14.7% 的绝对提升**。

## 4. 资源与算力
- 摘要及元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力细节。从使用 8B 参数模型进行监督微调来看，所需算力在现代单卡或多卡 GPU 上即可完成，但确切配置未知。

## 5. 实验数量与充分性
- 论文声称进行了“大量的实验（Extensive experiments）”，但所提供内容**未给出具体实验组数、消融实验的变量等细节**。由于仅能看到摘要，无法判断实验是否覆盖了多种领域、多语言或不同检索器设定，因此难以评估实验的充分性与公平性。从 14.7% 的显著提升可以推测，核心实验设置应当具备一定说服力，但细节有待论文全文确认。

## 6. 主要结论与发现
- EviPath 合成的推理路径数据能够**有效训练 LLM 的任务分解、检索调用和逐步决策能力**，使其成为合格的 RAG Agent。
- 仅使用 8B 参数模型，经过合成数据微调后，在开放域问答上相较于现有基线取得**显著的性能飞跃（EM 指标绝对值提升 14.7%）**，且结果具有一致性。
- 证据锚定的路径合成范式为**绕过强化学习、低成本开发具备复杂交互能力的 Agent** 提供了一条可行路径。

## 7. 优点
- **过程级监督**：首次以合成方式为 RAG Agent 提供完整的“思考-检索-回答”轨迹，填补了现有数据合成方法的空白。
- **证据锚定**：利用因果依赖关系逆向规划路径，保证了推理的合理性和轨迹的可解释性。
- **端到端可微调**：将环境交互直接转换为对话格式，无需定制化模型结构，可方便地迁移至任意指令微调管线。
- **效果显著**：在较小模型（8B）上获得大幅超过基线的性能，展示了合成数据的高质量。

## 8. 不足与局限
- **细节缺失**：由于仅有摘要，无法评估模型对检索器质量的敏感性、合成数据的噪声问题、对证据集合的依赖，以及多轮交互中的错误累积等。
- **实验覆盖不明**：未列出具体数据集和基线方法，可能仅在某些特定语种或领域上进行验证，泛化性未知。
- **合成数据成本**：摘要未提及合成路径所需的 LLM 调用开销，若依赖强模型（如 GPT-4）逆向规划，可能成本较高。
- **局限场景**：方法依赖已知证据集反向构建环境，对于极开放场景（如真实网络搜索）的适应性需要进一步研究。

（完）
