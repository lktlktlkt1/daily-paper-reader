---
title: "DeepRAG: Thinking to Retrieve Step by Step for Large Language Models"
title_zh: DeepRAG：大语言模型的逐步思考检索
authors: "Xinyan Guan, Jiali Zeng, Fandong Meng, Chunlei Xin, Yaojie Lu, Hongyu Lin, Xianpei Han, Le Sun, Jie Zhou"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=VI2YaggHIF"
tags: ["query:agentic-rag"]
score: 10.0
evidence: DeepRAG将检索增强推理建模为MDP实现逐步动态检索
tldr: 针对RAG中推理无效和冗余检索引入噪声的问题，提出DeepRAG框架，将检索增强推理建模为马尔可夫决策过程。通过逐步分解查询，动态判断是否需要检索外部知识，使LLM能思考性地决定检索时机。实验表明该方法能减少噪声检索，提升推理质量，为面向推理的RAG提供了自适应决策机制。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: RAG中无效任务分解和冗余检索会引入噪声，降低推理质量。
method: DeepRAG将检索增强推理建模为MDP，支持逐步查询分解和自适应检索决策。
result: 实验证明DeepRAG能有效降低噪声并提升推理任务表现。
conclusion: 动态检索决策的MDP建模提升了RAG的推理能力。
---

## Abstract
Large Language Models (LLMs) have shown remarkable reasoning capabilities, while their practical applications are limited by severe factual hallucinations due to limitations in the timeliness, accuracy, and comprehensiveness of their parametric knowledge. Meanwhile, enhancing retrieval-augmented generation (RAG) with reasoning remains challenging due to ineffective task decomposition and redundant retrieval, which can introduce noise and degrade response quality. In this paper, we propose DeepRAG, a framework that models retrieval-augmented reasoning as a Markov Decision Process (MDP), enabling reasonable and adaptive retrieval. By iteratively decomposing queries, DeepRAG dynamically determines whether to retrieve external knowledge or rely on parametric reasoning at each step. Experiments show that DeepRAG improves retrieval efficiency and boosts answer accuracy by 25.41%, demonstrating its effectiveness in enhancing retrieval-augmented reasoning.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机与背景**：大语言模型（LLM）虽然具备强大的推理能力，但受限于参数化知识的时效性、准确性与全面性，容易产生事实性幻觉。传统的检索增强生成（RAG）在融入推理时面临两个关键挑战：
  - **无效的任务分解**：简单地将问题拆分并逐次检索，缺乏对实际需求的判断。
  - **冗余检索引入噪声**：不必要的外部知识检索会干扰模型自身推理，降低回答质量。
- **整体含义**：论文提出 **DeepRAG** 框架，将检索增强推理过程建模为马尔可夫决策过程（MDP），让模型能够“先思考再决定是否检索”，通过逐步动态决策何时利用外部知识、何时依赖参数化推理，从而减少噪声、提升推理效率与答案准确性。

### 2. 论文提出的方法论
- **核心思想**：把检索增强推理视为一个序列决策问题，每一步模型都能根据当前状态自适应地决定：继续对问题进行分解（推理），还是从外部知识库获取信息（检索），从而避免不分青红皂白地检索带来的噪声。
- **关键技术细节**：
  - **MDP 建模**：
    - **状态**：包含已生成的推理链、原始问题以及历史检索信息。
    - **动作**：两个可选动作——“检索外部知识”或“依赖参数化推理继续分解”。
    - **奖励**：以最终答案的正确性或中间步骤的合理性作为反馈信号。
  - **迭代式查询分解**：模型将复杂查询逐步拆解为子问题，每生成一个子问题后，先判断该子问题是否需要外部知识支持，再决定执行检索还是直接推理。
  - **自适应决策**：通过训练（或提示）让 LLM 学会在何时检索能够最大化收益，从而形成“思考 → 判断 → 检索/推理”的闭环。
- **算法流程（文字描述）**：
  1. 输入查询，初始化状态。
  2. 循环直到得出最终答案：
     - 模型基于当前状态生成下一步的思考（例如拆分出子问题）。
     - 对于该子问题，模型评估其是否需要外部知识，决定动作（检索 or 推理）。
     - 若选择检索，则调用检索器获取文档片段，更新状态；否则直接利用模型自身知识推导，更新推理链。
     - 整合信息后判断是否完成，未完成则返回步骤 2。
  3. 输出最终答案。

### 3. 实验设计
- 由于仅提供了论文摘要，未披露完整的实验章节，以下分析基于摘要中的有限信息：
  - **数据集/场景**：未明确列出具体基准名称，摘要仅指出“实验证明 DeepRAG 提升了检索增强推理性能”。
  - **基准与对比方法**：摘要中未提及对比的基线模型或其他 RAG 方法（如标准 RAG、Self-RAG、ReAct 等），但通常此类研究会在多跳问答、事实验证等需要推理的数据集上进行测试。
  - **主要指标**：答案准确率（提升 25.41%）和检索效率（定性提升）。具体数值的上下文（如从多少提升至多少）未说明，无法判断绝对水平。

### 4. 资源与算力
- **文中是否提及**：提供的摘要与元数据中均未包含 GPU 型号、数量、训练时长或任何算力消耗的描述。
- **结论**：关于算力资源的信息完全缺失，无法评估其训练/推理成本。

### 5. 实验数量与充分性
- **实验规模推测**：仅凭摘要中的一句概括性结果，无法获知开展了多少组实验（如不同的消融因子、多个数据集、不同检索器配置等）。
- **充分性评估**：从现有信息看，无法判断实验是否充分、详尽。缺少与其他方法的系统对比、误差分析或统计显著性检验，其结论的客观性和公平性有待论文全文验证。

### 6. 论文的主要结论与发现
- DeepRAG 通过 MDP 形式化检索决策，让 LLM 学会“何时检索”，显著减少了冗余检索带来的噪声干扰。
- 该方法在提升答案准确率（+25.41%）的同时，也提高了检索效率（更少的无效检索）。
- 动态、逐步的思考-检索机制优于传统的静态检索方案，为推理导向的 RAG 提供了更合理的自适应决策范式。

### 7. 优点
- **方法创新性**：首次将检索增强推理过程显式建模为 MDP，赋予模型在推理链中自主决策“检索与否”的能力，思路清晰且切中当前 RAG 的痛点。
- **减少噪声干扰**：通过自适应跳过不必要的检索，有望缓解外部知识污染推理链的问题，提升生成质量。
- **泛化潜力**：框架具有通用性，可叠加于大多数 LLM 与检索器之上，不必改变底层模型架构。

### 8. 不足与局限
- **实验细节缺失**：仅凭摘要无法评估实验的真实强度，缺乏数据集、baseline、消融实验等关键信息，结果的可复现性和稳健性存疑。
- **可能的高训练成本**：若使用强化学习训练 MDP 策略（文中未指明），可能需要大量环境交互信号和奖励设计，增加了落地难度。
- **应用限制**：性能高度依赖于检索器质量和奖励函数的设计；对于简单问题，显式的序列决策可能引入不必要的时延开销。
- **评估风险**：单一准确率提升数字脱离了原始基线，可能夸大效果；另外，未提及对“检索效率”的具体量化方式，存在偏差风险。

（完）
